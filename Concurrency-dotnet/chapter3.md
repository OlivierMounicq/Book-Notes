## Chapter 3

####  Thread contention

A Thread contention is a condition where one thread is waiting for an object, being held by another thread, to be released.  The waiting thread cannot continue until the other thread releases the object (it’s locked).


#### System.Collection.Immutable

The namespace ```System.Collection.Immutable``` hase been added with the .NET 4.5 framework.  
The _immutable collection_ follows the functional paradigm.  

Any operations that change the data strctures don't modify the original instance. Instead, they return a changed copy and leave the original instance unchanged.

 The immutable collections have  been  heavily  tuned  for  maximum  performance  and  use  the  [Structural  Sharing pattern](https://en.wikipedia.org/wiki/Persistent_data_structure) to minimize garbage collector (GC) demands.
 
 ```cs
 var originalDictionary = new Dictionary<int,int>().ToImmutableDictionary();
 var modifiedCollection = originalDictionary.Add(key, value); //Return a new instance of the dictionary
 ```
 
 => Any changes to the collection in one thread are not visible to the other threads.
 
 
 #### Immutable collection
 
 | Immutable collection             | Mutable collection      |
 |----------------------------------|-------------------------|
 | ImmutableList<T>                 | List<t>                 |
 | ImmutableDictionary<TKey,TValue> | Dictionary<TKey,TValue> |
 | ImmutableHashSet<T>              | HashSet<T>              |
 | ImmutableStack<T>                | Stack<T>                | 
 | ImmutableQueue<T>                | Queue<T>                | 
  
  
 
