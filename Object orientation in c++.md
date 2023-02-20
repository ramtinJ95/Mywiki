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
