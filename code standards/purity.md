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

We'll get back to a technical definition later.  The short version, for functions, is "it's pure if it doesn't keep or 
modify any state, and if its return value is solely based on its arguments."
