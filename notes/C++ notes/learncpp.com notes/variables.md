## initialization
examples of the initializations

```C++
int a;         // default-initialization (no initializer)

// Traditional initialization forms:
int b = 5;     // copy-initialization (initial value after equals sign)
int c ( 6 );   // direct-initialization (initial value in parenthesis)

// Modern initialization forms (preferred):
int d { 7 };   // direct-list-initialization (initial value in braces)
int e {};      // value-initialization (empty braces)
```

### default-initialization
this doesn't really initialize anything it just reserves space with a garbage value

### copy-initialization
inherited from C 
`int a = b;` The right variable will be copied into the left one
this is less efficient for complex types and thus fell out of favor. since c++17 most of those issues were fixed and now people are fans of it again.

ALSO older c programmers of some others still do use this

### direct-initialization
originally meant as an efficient initializer, but got superceded by next type
it has come back for niche cases

### list-initialization
The modern and recommended way of init
this was introduced so it worked almost always and consistently
can also use a list of values

ALSO this disallows narrowing conversions AKA it will not round a float to an int thus losing data

### value/zero-initialization
this will implicitly initialize to zero or the zero value
in advanced objects this also inits some values to given defaults

### best practices
Bjarne Stroustrup (creator of C++) and Herb Sutter (C++ expert) also recommend [using list-initialization](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Res-list) to initialize your variables.

use ==direct-list== when actually using the variable ==directly==
use ==value init== when it is temporary and will be ==replaced==
almost always initialize your variables
For more discussion on this topic, Bjarne Stroustrup (creator of C++) and Herb Sutter (C++ expert) make this recommendation themselves [here](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es20-always-initialize-an-object).
## instantiation
this generally means a variable has been allocated (created) and initialized. this object could be called an instance

you can instantiate multiple instances at once

```C++
int a = 5, b = 6;          // copy-initialization
int c ( 7 ), d ( 8 );      // direct-initialization
int e { 9 }, f { 10 };     // direct-list-initialization
int i {}, j {};            // value-initialization
```
THIS IS HIGHLY DISCOURAGED you might still see it tho so important to know
this is why: this is a common mistake that can be annoying to find
```C++
int a = 4, b = 5; // correct: a and b both have initializers
int a, b = 5;     // wrong: a doesn't have its own initializer
```



```cpp
#include <iostream>

int main()
{
    [[maybe_unused]] double pi { 3.14159 };  // Don't complain if pi is unused
    [[maybe_unused]] double gravity { 9.8 }; // Don't complain if gravity is unused
    [[maybe_unused]] double phi { 1.61803 }; // Don't complain if phi is unused

    std::cout << pi << '\n';
    std::cout << phi << '\n';

    // The compiler will no longer warn about gravity not being used

    return 0;
}
```
also the compiler might optimize these out of the program

### unitinitialized variables
in c/c++ a variable that doesnt get a value will contain the value left at that adress
- Initialized = The object is given a known value at the point of definition.
- Assignment = The object is given a known value beyond the point of definition.
- Uninitialized = The object has not been given a known value yet.
not immediatley initializing is faster but only marginally so

this garbage variable creates weird behaviours since we dont know whats in it this is UNDEFINED BEHAVIOR (UB)
this is because c++ does not have a defined behavior when using an unitted var 
Code implementing undefined behavior may exhibit _any_ of the following symptoms:

- Your program produces different results every time it is run.
- Your program consistently produces the same incorrect result.
- Your program behaves inconsistently (sometimes produces the correct result, sometimes not).
- Your program seems like it’s working but produces incorrect results later in the program.
- Your program crashes, either immediately or later.
- Your program works on some compilers but not others.
- Your program works until you change some other seemingly unrelated code.

Or, your code may actually produce the correct behavior anyway.

### naming
recommended
- always start with a lowercase letter
- no numbers
- snake_case or camelCase
- no whitespaces


### takeaways and extras
In modern C++, there are some cases where list-initialization does not work as expected. Because of such quirks, some experienced developers now advocate for using a mix of copy, direct, and list-initialization, depending on the circumstance.

unused initialized variable give warnings with Werror these become errors (like Golang)
we can however deal with this in version 17

Code is read more often than it is written, so any time saved while writing the code is time that every reader, including future you, will waste while reading it. If you’re looking to write code faster, use your editor’s auto-complete feature.

VARIABLES SHOULD BE DEFINED AS CLOSE TO THEIR FIRST USE AS POSSIBLE