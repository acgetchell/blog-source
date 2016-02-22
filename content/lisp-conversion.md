Title: Lisp Conversion
Date: 2011-12-01 23:32
Author: Adam Getchell
Tags: lisp, tdd, clojure
Slug: lisp-conversion
Category: Programming

A few months and a lot of Lisp later, I find myself convinced/converted
...  

... To [Clojure](http://clojure.org/).  

Rajesh, you were right!  

As far as language ~~snobbery~~ coolness, it has a bunch of features I
like such as:  

-   A [REPL](http://clojure.org/dynamic) for fast development
-   [Functional programming](http://clojure.org/functional_programming)
    with [immutable
    values](http://thinkrelevance.com/blog/2008/09/16/pcl-clojure-chapter-6.html) which
    makes it easy to reason about concurrency
-   [Concurrent programming](http://clojure.org/concurrent_programming)
    via [software transactional memory](http://clojure.org/refs)
-   A
    [Lisp-1](http://hornbeck.wordpress.com/2009/07/05/lisp-1-vs-lisp-2/)
    [dialect](http://clojure.org/lisp)
-   OOP benefits without OOP using [runtime
    polymorphism](http://clojure.org/runtime_polymorphism)
-   Lots of modern libraries by being [hosted on the
    JVM](http://clojure.org/jvm_hosted)
-   A [vibrant community](http://groups.google.com/group/clojure) (my
    [F\# groups](http://groups.google.com/group/fsharp-opensource), by
    contrast, have had barely 2 messages in the past month)

To get an idea of what I mean, here's an anonymous function to find the
odd numbers in a (lazy) [sequence](http://clojure.org/sequences) (which
could be a list, vector, or hash map):  


This idea of [lazy
sequences](http://formpluslogic.blogspot.com/2009/07/clojure-lazy-seq-and-recursion.html)
is powerful, because you can do things like get the [10,001st prime
number](http://clojure-euler.wikispaces.com/Problem+007) without blowing
the stack:  

You can just see the number-crunchy goodness, mixed in with Lispy
functional precision.  

As far as practicality, there is simply too much awesome stuff.  

-   The language itself is available on
    [GitHub](https://github.com/clojure/clojure)
-   It has nice [documentation](http://clojuredocs.org/) to [get you
    started](http://dev.clojure.org/display/doc/Getting+Started) quickly
-   There are great learning
    resources: [4Clojure](http://www.4clojure.com/) [clojure-koans](https://github.com/functional-koans/clojure-koans)
-   Nice examples of algorithms such
    as [Quicksort](http://www.algolist.net/Algorithms/Sorting/Quicksort)
    using [Clojure](http://rosettacode.org/wiki/Sorting_algorithms/Quicksort#Clojure)
-   [Easy
    translation](http://thinkrelevance.com/blog/2008/09/16/pcl-clojure.html)
    from [Practical Common Lisp](http://www.gigamonkeys.com/book/)
-   A [freely
    available](http://www.jetbrains.com/idea/download/index.html)
    [killer IDE](http://www.jetbrains.com/idea/) [supporting
    Clojure](http://plugins.intellij.net/plugin/?id=4050) with [project
    building](https://github.com/technomancy/leiningen) and GitHub
    support
-   [Simple](http://webnoir.org/) to
    [complex](https://github.com/weavejester/compojure/wiki) web
    application support to
    [EC2](http://mmcgrana.github.com/2010/07/develop-deploy-clojure-web-applications.html),
    [Heroku](http://blog.heroku.com/archives/2011/7/5/clojure_on_heroku/),
    [Google App
    Engine](http://googlecode.blogspot.com/2010/05/better-performance-in-app-engine-with.html)
    and others

You can easily do TDD (test driven development), which is really handy
if, say, you've got a bunch of math functions that you want to be sure
are correct when you port/rewrite code.  

Here's a screenshot of [IntelliJ](http://www.jetbrains.com/idea/) with a
typical [Leiningen](https://github.com/technomancy/leiningen) project
open:  


<div class="separator" style="clear: both; text-align: center;">

</div>

<div class="separator" style="clear: both; text-align: center;">

[![](http://4.bp.blogspot.com/-M-dYvAMiipM/TtfPdohU_mI/AAAAAAAA_vE/NeiVEH5OKHs/s640/idea-lein.png)](http://4.bp.blogspot.com/-M-dYvAMiipM/TtfPdohU_mI/AAAAAAAA_vE/NeiVEH5OKHs/s1600/idea-lein.png)

</div>



You can see the typical Leiningen project layout, with /src and /test
folders and subfolders. First, we'll write a ~~function~~ test for a
function we want which sums over all values in a given sequence:  


The test is in C:\\Projects\\CDT\\Newton\\test\\Newton.test\\core.clj,
and the :use [Newton.utilities] tells it to look in the file
C:\\Projects\\CDT\\Newton\\src\\Newton\\utilities.clj for our function.
Note the use of metadata \^{:utilities true} to mark this as a utilities
test, which we'll use later for organization. Our test checks that our
to-be-defined sum test sums correctly over both a list and a vector.  

Now here's the contents of
C:\\Projects\\CDT\\Newton\\src\\Newton\\utilities.clj:  


Finally, Leiningen allows us to choose test selectors so that we can
specify which tests we want to run via project.clj:  


Now by running lein at a command prompt (to save startup time) we can
pick our tests:  


<div class="separator" style="clear: both; text-align: center;">

[![](http://1.bp.blogspot.com/-myffmQYgpC8/TtfWhU5qTQI/AAAAAAAA_vM/uTxhOaHJSO4/s640/lein.png)](http://1.bp.blogspot.com/-myffmQYgpC8/TtfWhU5qTQI/AAAAAAAA_vM/uTxhOaHJSO4/s1600/lein.png)

</div>



Note in the first case, we don't expect any tests to run (test! means
fetch dependencies and then run tests) because our sole test has been
marked as a :utility. In the second case, we tell it to run :utility and
it does, telling us that our test passed. Success!  

If our test had failed, clojure's test suite would give us good
information. Here, I'm going to modify the second assertion to fail.
Watch what happens:  


<div class="separator" style="clear: both; text-align: center;">

[![](http://4.bp.blogspot.com/-CqWRxYR47_Y/TtfXz8Po9GI/AAAAAAAA_vU/RvqznnUbXSk/s640/lein-test-fail.png)](http://4.bp.blogspot.com/-CqWRxYR47_Y/TtfXz8Po9GI/AAAAAAAA_vU/RvqznnUbXSk/s1600/lein-test-fail.png)

</div>


How cool is that?  

I've so far read [Clojure in Action](http://www.manning.com/rathore/)
and [The Joy of Clojure](http://joyofclojure.com/) (both highly
recommended), plus enough daily doses  to actually stop mucking about
and start with the [CDT code](https://github.com/ucdavis/CDT) already.  

So, a modern Lisp with powerful IDEs, modern libraries from the JVM,
interactive REPL/TDD, great documentation, learning resources, and
books -- what's not to like?  


</p>
