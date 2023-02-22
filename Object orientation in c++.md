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

---
Status: :🌳:
tags: [[C++ Notes.md]]
date: Tue 21 Feb 2023 17:14:10 CET
