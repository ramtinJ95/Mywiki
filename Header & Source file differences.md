## Method definitions
All method definitons should be in the header file. This includes not only the
type of the parameters and return type, but also what kind of access level we
want a method to have. So stuff like if the method is public for a class or if
it is a static method etc all go in the header file. The source file contains
literarly only the implementation code.

Header file:
  class Foo: {
    private:
      
    public:
      static void bar();
  }

Source file:
void bar() {
  implementation of bar
}


## Static variables
So if we declare a static variable in our header file like:

  static std::vector<SomeType> foo

We also have to define this variable in our source file otherwise we will have a
linker error since the linker expects a definiton of this variable that we have
declared in our header. In order to do this we have to have the following in our
source file:

  std::vector<SomeType> ClassName::foo 



---
status: :🌱:
tags: [[030 Software Development.md]] - [[C++ Notes.md]]
date: Wed 22 Feb 2023 16:34:06 CET
