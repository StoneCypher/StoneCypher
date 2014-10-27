JavaScript Code Standard
========================

My code standard for JavaScript is as follows:





General form
------------

* All rules are discretionary.  If there's a very good reason to break one, break it.  But, don't do so just because you
  have a different preference, please.
* Code documentation is heavily encouraged.  I use [YUIDoc](http://yui.github.io/yuidoc/) for JS documentation extraction.
  * The best code documentation shows a few basic use cases and expected results
* Testing is heavily encouraged.
  * I use [vows](https://www.npmjs.org/package/vows) as a test runner for headless
  * I use [JsVerify](https://github.com/phadej/jsverify/) for stochastic property testing





Text form
---------

* Lines should be up to 120 characters long.
* Strings should be single quoted
* Horizontals should align, such as the `=` in assignments, the arguments in repeat calls to the same function, etc





Code form
---------

* Code lines end in semicolons
* 1TBS / K&R style blocks (braces are at the end of the preceding line)
* Four space indents; no hard tabs
* No multiline string trickery
* Code in IIFEs (except for node where that's implicit)
* Code that runs in or out of CommonJS where practical
* `'use strict'`
* please use jshint





Vertical whitespace
-------------------

* Five lines should be used between unrelated top level functions, objects, classes, blocks of variables, and other major
  chunks, to keep them visually distinct.
* Three lines between related functions, members of a small class, interior functions, and other things meant to be
  visually clustered.
* Two lines to break up major segments of a large monolithic chunk of code.  *This is usually a warning sign*.
* One line to separate minor pieces, loops, variables from code, etc.
* One buffer line inside blocks