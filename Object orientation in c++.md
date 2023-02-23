### Object initialized on the stack
Say we have something like this
  int main() {
  Game game;
  game.Run();
  return 0
  }
In situations like this we will create a new Game object and it will be put on
the stack and be destroyed as soon as the code leaves this scope. If we had
used the "new" keyword then it would have been put on the heap and not be
destroyed once we leave this scope. 

## Static Methods
Sometimes in c++ we have stuff like

  Logger::Log("some message")

The reason we can do something like this is because the Log method is a static
method defined in the header as public static. For methods like these we do not
need to first instancieate an object and then use the methods that belong to
that class, we can just use them directly using the class scope syntax "Logger::"

## The Const Keyword
It is good practice to add the const keyword to public methods that are only
going to be used as getters so that the compiler acts as a guard for us in case
we try to use a method to modify something that we really should not.

  class Entity {
    private:
      int id;
    public:
      int GetId() const; 
  }

## Class object constructor
If we have a simple constructor that is going to only initialize some variables
and so on we dont need to the whole
  
  class Entity {
    private:
      int id;
    public:
      Entity(int id ) {
        int id = id
        ...
      }
      int GetId() const; 
  }

Instead what we can do is using this list initialzior syntax

  class Entity {
    private:
      int id;
    public:
      Entity(int id ): id(id) {}; // note that we can add multiple comma seperated values here
      int GetId() const; 
  }

Notice that this way of having a private field which we can get from a public
method is just called encapsulation and is very common in the OOP paradigm. 

---
Status: :🌳:
tags: [[C++ Notes.md]]
date: Tue 21 Feb 2023 17:14:10 CET
