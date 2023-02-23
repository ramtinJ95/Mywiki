## Windowing
when creating a window for the game to run in, there is this concepet of real
fullscreen vs fake fullscreen. For fake fullscreen the window that is created
will simply just fetch the display widht and height and create a window equal to
those dimensions. But this means that 2 players with different sizes of their
displays will see different things and that is not fair. Instead what is usually
done is that there are some options of resolutions say 800x600 and then we set
the rendering mode to fullscreen. In this way the two players will see the exact
same amount of the map for example but the graphics lib will just stretch the
content to match their respective displays. 


## Double-Buffered rendering
The way most rendering is done is that we have 2 buffers, one is the window into
the game world that the user sees, but there is also the same thing going on
behind that window in what is called the second buffer. We draw all the updates
and new objects into that second buffer and once that is done we swap the
buffers. This is so that the user does not see things being rendered and makes
it so that there is much fewer graphical glitches.


## Game Loop Time Step
We cannot couple the update ticks of state of our game/simulation with how often
a frame is updated. Because that will not be controlled by our engine but rather
by how fast the machine that runs the code is.

Also we cannot either just tell the loop to hold for some time by trying to
figure out a how long each frame should have to render etc, because this will
lead to our engine hogging up cpu resources that are doing nothing instead of
releasing the cpu from the current process so it can do something else and we
will notify the cpu when its time to resume with our process. This way we wont
throw away cycles for nothing.

So what we dont want to think about is: How many pixels per frame. Rather we
want to think in terms of: How many pixels per second. This means that the
objects in the game will move and update in the same way for everyone regardless
if the game runs at 500fps or 60fps, since the game tick, i.e the update
frequency of game state will be tied to real world time (well some approximation
that is good enough for our engine anyway).

So in my game engine I will go with the simplest implementation that is robust
enough for a 2d game engine. Since I will not be doing any heavy physics
simulations yet (maybe in the future when i turn the engine into 3d and decide
that I want it to be able to do good physics simulations) I will go with a
Variable Delta-Time approach.

#### Variable Delta-Time
What we do instead of relying on the number of frames per second that we want is
that we will introduce a time dimension. So what we do in this approach is that
we calculate our Delta-time, which is the difference of time between the last
frame and the current one. We will then use this delta-time as a constant
(although it probably is not a constant value since it will change depending on
what is going on with the cpu and how heavy the stuff that we want to calculate
and render actually is) and multiply all movement of objects in our game with
this constant.

I may want to use the semi-variable approach that is mentioned in the link below
if I see that it is needed.

For diving deeper check this link https://gafferongames.com/post/fix_your_timestep/


## Component-Based Design
It may seem like an obvious idea to use a straight up object orienteded
inheritence style for our game engine where we have some proto class that
everyone inherits from and so on. But as I have learned that multiple levels of
inheritence is not ideal, I will go with a Component-Based Design instead. More
specifically it will be what other game engines such as Unity use, which is
called a ECS approch (Entity-Component-System). 

Every object in the game will be called an Entity. Each entity can have any
number of components. So one component could be the tranform-component,
collider-component and so on. Then the Enemy entity will have these components
plugged into it, and this is how we will modify its behaviour. Then we will have
one class which is called the Entity manager which we will use to keep track of
all the entities in the scene. Each component then takes care of its own
behaviour as well and has its own render and update functions. This means that
each entity has a list of components, and it goes and tells all its own
components to run their own render and update methods before it runs its own
render and update methods.

  Entity Manager has a list of entities --> Each entity in this list have their
  own list of each component and their own update and render methods --> Each
  component have their own behaviour, render and update methods.

This is the high level overview/explanation of the Component-System desgin pattern. 

We will still have some level of inhertience though, so for example we will have
an abstract class for Entity and Component, and all implementations of entities
and components will inherit some virtual (c++ version of abstract) methods that
need to be overriden and implemnted, but notice that it will be at most 1 level
of inheritence. 

#### Example of Component-Based Design

  class Entity {
  vector<Component*> components;
  void AddComponent<T>(component);
  void Update(deltaTime);
  void Render();
  }
Entity has a 1 to many relationship to the Component class:
``` cpp
class Component {
  Entity* owner;
  
  virtual Update();
  virtual Render();
}
```

Then the following component classes inherit from our component class:
``` cpp
class TranformComponent: public Component {
  glm::vec2 postion;
  glm::bec2 scale;
  double rotation;

  Update() override {
  }

  Render override {
  }
}
```

And then finally we have the entity manager class or registry, and there is only
one instance of this class:
``` cpp
class Registry {
  vector<Entity*> entities;
    
  void AddEntity(entity);
  void RemoveEntity(entity);
  void Update(deltatime);
  void Render();
  }
```
## Entity-Component-System
As mentioned previously, ECS is what modern game engines use nowdays. This ECS
pattern is a modification of the Component-Based Design that I mentioned
earlier. The modifications are as follows, pay attention to how much simpler
this pattern is compared to the Component-Based Design above.

- Entities
  - Simply an ID
  - They will represent the objects that populate the game sceen. 
- Components
  - Components are pure data so in our case with c++ they will be structs
  - They are organized by the data itself rathar than by entity
    - This organization is the key difference between object oriented and data
      oriented design
- Systems
  - Systems are the logic (code) that transforms components from one state to
    the next state
  - For example a MovementSystem might update the position of moving entities by
    their velocity since the previous frame.

One of the major benefits of having all the components like this is that we can
keep them all in continous block of memory and close to each other in memory.
This means that we can make much better use of the cache compared to the
Component-Based system above which would have us have pointers to a bunch of
objects all over the place in memory. 

#### Example of ECS
``` cpp

class Entity {
  int id;
}

struct TransformComponent {
  glm::vec2 postion;
  gl::vec2 scale;
  double rotation;
}

class MovementSystem {
  public:
    MovementSystem() {
      RequireComponent<TranformComponent>();
    }
    
    void Update(double deltaTime) {
      for (auto entity: GetEntities()){
        TransformComponent& transform =
        entity.GetComponent<TransformComponent>
        
        transform.position.x += rigidbody.velocity.x * deltatime;

```
Here we can see that each system is only going to interact with a subset of the
entities in our scene depending on the components that they have, this adds yet
another performance gain since we could in theory split the work up in threads
and so on

### System Component Signature
In order for us to be able to write a method like RequireComponent and make it
so that certain systems only interact with certain Entities which have certain
components we need to create a sginature for each component.

In my game engine implementation the type for the Signature will be:
``` cpp
MAX_COMPONENT = 32;

typedef std::bitset<MAX_COMPONENTS> Signature;
```
This is basically an array with 32 bits where for each component 1 of the bits
will be 1 for each component. But the trick here is that the index which is 1
will represent which component it is. This also means that each component will
now need to have an ID field. So our parent Component class will have an ID
field.



---
Status: :🌱:
tags: [[030 Software Development.md]]
date: Tue 21 Feb 2023 17:24:01 CET
