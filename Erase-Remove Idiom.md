In our gameengine code for removing entities we have the following code:

```cpp 
entities.erase(std::remove_if( 
  entities.begin(), 
  entities.end(),
  [&entity] (Entity otherEntity) { return entity = otherEntity; }),
  entites.end());

```

So the reason we need this type of removing is that if we have a long list and
we are going to remove 1 thing often or even many things often from this list,
then the computer would have to keep resizing the underlying array that these
container objects are built upon, and this is expensive and creates quite a bit
of overhead.

So what we do instead since assignments require memory allocation and a simple
swap is just changing where stuff points, we use a swap.

We know that **vector::erase()** expects two parameters with the start and end
iterators of the elements to remove. So, why are we asking to erase from
**remove_if()** until **entities.end**? Because **remove_if()** does mot remove anything. it
just swaps elements around inside the vector in order to put all elements that
dont match the lambda criteria towards the front of the container. After the
**remove_if()** swapped all the elements around keeping their order, it will
then return an iterator to the first element that matched the lambda criteria.
This means that, to remove all elements that match the criteria, we need to
remove all elements **from** this iterator **until** the end of the vector. This
will effectively remove all elements that matched our lambda conditon.

