## Template
So the power of templates comes from the fact that they allows us to write one
" template " that we can reuse with different type say for a method instead of
writing that method 10 times with different types for each new variant.

The syntax for a template definition is something along these lines:

``` cpp
template <typename T> void RequireComponent();
```

It is customary to use T as the typename but one can use whatever really, then
the implementation can look something like:

``` cpp
template <typename T> void System::RequireComponent() {
const auto componentID = Component<T>::GetId(); // static method call
componentSignature.set(componentId);
}
```

Templates are defined in a class so they are defined in the header file but
whats unique to templates is that their implementation is also in the header
file. The reason for this is that the compiler needs to know all the types
upfront but we are using this generic type so it would not be able to know all
the types at compile time. And if we wrote the implementation in the cpp file
then it would not be able to inline all the different method definitons, so this
implicit inline defintion of all the functions that we did not write will be
done by the preprocessor, and for this to be possible the implementation of the
template needs to be in the header file. 
