# Purity

Usually discussed in terms of `functional purity`, but also available to `object`s, `expression`s, `procedure`s, and
so on, purity is an important characteristic for code that can make code:

  * easier to safely test, 
  * easier to parallelize (oftentimes automatically,) 
  * easier to compose, 
  * possible to make referentially transparent,
  * possible to memoize,
  * easier to render idempotent,
  * easier to understand,
  * easier to reason about,
  * easier to maintain,
  * easier to reuse,
  * easier to refactor,
  * easier to document,
  * easier to make lazy, and
  * easier to debug.

If these claims are true, then ***purity is very important***.

Also, purity is *easy to achieve*.  It just takes a slight change to your worldview.

Let's next go over why these claims are true.



<br/>

## What is purity?

We'll get back to a technical definition later.  The short version, for `function`s, is "it's pure if it doesn't keep 
or modify any state, and if its return value is solely based on its arguments."

One of the big advantages of `pure function`s is "referential transparency."  A referentially transparent function is
guaranteed to always provide the same result for the same arguments, in any context.  There are a lot of interesting
effects of that guarantee, such as that you can safely replace calls to the function with its result (that is, if
you already know that `cube(3)` is `27`, you (or the compiler or VM) can always safely replace any instances of
`cube(3)` with `27`.) 

That borders on impossible without purity.



<br/>

### Code would help

So, a quick example.

```javascript
var counter_impure = 0,
    counter_pure   = 0;

function impure_inc(by)        { return counter_impure += by; }
function pure_inc(counter, by) { return counter + by; }
```

Here we have two pieces of code which do roughly the same thing - to modify a counter by a distance `by` which is
provided to them.  The first function is not pure; the second function is pure.

The difference is that `impure_inc` uses state that comes from outside the function, in this case in a `downwards 
closure`.  As a result, you can call the function with the same arguments, *and get different results each time*.

By comparison, the pure version will always give the same results, given the same arguments, and does not modify
the arguments given to it.

```javascript
// the impure version changes invisible global state
console.log(impure_inc(3));  // 3
console.log(impure_inc(3));  // 6
console.log(impure_inc(3));  // 9

// the pure version doesn't change
console.log(pure_inc(counter_pure, 3));  // 3
console.log(pure_inc(counter_pure, 3));  // 3
console.log(pure_inc(counter_pure, 3));  // 3

// getting the behavior of the above is straightforward
console.log(counter_pure = pure_inc(counter_pure, 3));  // 3
console.log(counter_pure = pure_inc(counter_pure, 3));  // 6
console.log(counter_pure = pure_inc(counter_pure, 3));  // 9
```

"But," you might say, "that seems like a lot of extra code."

Well, when your function does a single bit of arithmetic, it might look that way. 😁

However, keeping state out of your functions really isn't much work - you just pass it in with args and out with the return value - and the benefits are enormous.

Let's take a look at a real world example.
