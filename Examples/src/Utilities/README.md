#Various Utilities#
you need to do

    make 
    make install

to install them. `make` will produce a dynamic and a static library, called `libpacs.so` and `libpacs.a`, respectively. `make install` installs the header files in `PACS_ROOT/include` and the libraries into `PACS_ROOT/lib`. Use `make DEBUG=no` if you want the library code to be optimised.


`make` also produces tests for most of the utilities.  *Remember to install the utilities, they are used by other examples!.*

**Note**: some utilities are in a nested namespace of the namespace apsc. Check it out looking at the code or at the examples.

List of the utilities:

* `GetPot`  GetPot command parser<http://getpot.sourceforge.net/>. I have simplified the version available on the given link, so you have just to so `#include <GetPot>` of `#include "GetPot"`, and have it available.

* `chrono`  An utility to take times, built on the chrono utilities of the standard library.

* `extendedAssert`  Asserts with a message. It extends assert macro so that you can insert a message. There are also swithches that can be activated with the `-DXXX` compiler option to change the behaviour of some of them.

* `Factory`  A generic object factory. Inspired by a code by [Andrei Alexandrescu](https://en.wikipedia.org/wiki/Andrei_Alexandrescu). 

* `Proxy`    A proxy to add objects to the generic object factory

* `gnuplot-iostream` A stream to open gnuplot from within a program. Useful for visualization. You need `gnuplot` installed in your system.

* `scientific_precision` A function that sets the precision of a stream to the maximum value for a floating point. It contains also stream manipulators for the same purpose.

* `string_utility` Some extra utilities for strings: trimming (eliminate useless blanks) and lower-upper conversion.

* `cxxversion` To test with which version of C++ you are compiling your code

* `CloningUtilities` Tools for clonable classes (Prototye design pattern). It contains some type traits to test if a class T containes the (usually virtual) method

```
std::unique_prt<B> clone() const;
```

that returns the pointer to a copy of the object wrapped into a
unique_prt.  B can be either T or a base class of T. It also contains
an interesting class, called `PointerWrapper`, which implements an owning pointer with deep copy
semantic! The "pointed" class should be clonable. It means that you can use it to implement composition of a polymorphic object!

* `is_complex`  Type traits to check is a type is `std::complex<T>`

* `is_eigen` Type trait to check if a type is an Eigen vector or matrix

* `SmartSummation` Some tools that implements way of making sums of vectors reducing roundoff error.

* `StatisticsComputations` Some tools to compute basic statistics of a sample.

* `joinVectors.hpp` A poor man implementation of the join() utility in python. It allows to join together standard vectors and iterate on all of them at the same time. Look at `test_joinVector.cpp` to see the possible usage. It is a nice example of variadic templates and iterators. The implementation can be bettered, in particular the design of the iterator. But it works (apparently).


** Note ** `Factory.hpp` and `Proxy.hpp` are in fact links to the same file in the folder `GenericFactory`. If the files are not present for some reason you may safely copy in `Utility/` the files in `GenericFactory/`.

## What you can learn from these examples##
The files in this directory illustrate the advantage of having little general utilities that can be integrated in different codes.
Some utilities are simple to understand, like `Chrono` or `StatisticsComputations`, others make use of more sophisticated generic programming 
techniques, like `Factory`, or template metaprogramming, like `is_complex`, `is_eigen`, `joinVectors` and `CloningUtilities`. 
Finally, some, like `gnuplot_iostream` and `GetPot` are just copies of tools available open source, copied here for simplicity.

In `CloningUtilities` and `joinVectors` you have classes that define a dereferencing operator (`*`) and an access via pointer operator
(`->`). Something you do not find very often.

`SmartSummation` shows techniques that are useful only on machines that
do not respect the IEEE standrd fully, or if you use low precision
arithmetic. But they show also a use of the `volatile` keyword to avoid the compiler to optimise
constructs that should not be optimised to work as expected! The reduction of roundoff error do depend on operations that have to be performed
that way! You cannot let the compiler to change the order of operation or do simplifications, pretending to be smart.
