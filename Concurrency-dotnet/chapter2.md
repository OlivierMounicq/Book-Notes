.

#### 1 The function composition

The classical way to aggrega


```csharp
Func <R,S> firstFunction = var1 => return doSometing(var1);

Func<S,T> secondFunction = var2 => return doOtherThing(var2);

S var2 = firstFunction(var1);
T result = secondFunction(var2);

//Or

var result = secondFunction(firstMethod(var1));

```    

But the best way is:

```csharp
static Func<R,T> Compose<R,S,T>(this func<R,S> firstFunction, Func<S,T> secondFunction) 
    => (n) => secondFunction(firstFunction(n));
    
//And then:
Func<R,T> doEverything = firstFunction.Compose(secondFunction);
R var1 = ....;
T result = doEverything(var1);
```


#### 2 The closure

The _closures_ are a more convenient way to five functions access to a local state ad to pass data into background operations.

```csharp
string closureVar = "I am a free variable dedicated to the closure";

Func<string,string> lambda = value => closureVar + " " + value;

```    

#### 3 The captured variables in closure with lambda expression




#### 4 The memoization-cache

The goal is to store all results and their inputs in a cache to avoid to recompute each time the output value.

```csharp
static Func<T,R> Memoize<T,R>(Func<T,R> func)
   where T : IComparable
{
    Dictionary<T,R> cache = new Dictionary<T,R>();
    
    return arg => {
        if(cache.ContainsKey(arg))
            return cache(arg);
        return (cache[arg] = func(arg));    
    };
}
```

__Beware__ : the dictionary is unbounded : the items are only added never removed. To avoid the memory size issue, you can use the collection ``` ConditionalWeakDictionary ``` to add an automatic mechanism to remove the items for which the key has been removing by the GC.

