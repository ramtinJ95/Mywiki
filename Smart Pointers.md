Smart pointers are the c++ answer to programmers forgetting to deallocate
memory, instead the compiler will take care of it for us.

## Types of smart pointers
There are several different types of smart pointers that are best used in
different scenarios.

This code example below is just a reference example of what a raw pointer looks
like:

```cpp 
Void SomeFunction() {
  Enemy* enemy = new Enemy: // remember that new keyword is allocation on heap

  enemy->Jump();
  ...

  delete enemy; // to deallocate memory from heap
}
``` 
#### Unique smart pointers
Unique pointers are best used when we know that this pointer that we are
creating is going to be the only thing that will point to whatever object we are
pointing to and that the ownership of that object will never change. The
recommendation when using smart pointers is to not use the "new" keyword.
Actually some projects have guidelines where they dont allow for any pointers to
be created with the new keyword.

```cpp 
void SomeFunction() {

  std::unique_ptr<Enemy> enemy = std::make_unique<Enemy>();
  enemy->Jump();
}
``` 
Notice how we dont need to destroy the object manually. The smart pointer ends
its scope, i.e the scope of whatever owns that smart pointer is out of scope
then the object that it pointed to and by extension the scope had ownership over
will be destroyed automatically.


#### Shared smart pointers
Shared pointers on the other hand are best used when we know that we will need
to share the ownership over some resource.

```cpp
void SomeFunction() {

  std::shared_ptr<Enemy> enemy = std::make_shared<Enemy>();
  enemy->Jump();
}

```
The shared pointer is smart enough to only delete the object when the last owner
is out of scope. So in other words it keeps a counter of references to some
resource or object and will only destroy that object once that reference counter
is 0.

#### Weak smart pointers
// TODO
