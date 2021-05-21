# C and C++

- [C and C++](#c-and-c)
  - [C/C++ Learning](#cc-learning)
    - [My Small TODO list for basic C learning](#my-small-todo-list-for-basic-c-learning)
  - [GSoap](#gsoap)
    - [Simple Soap String assignment](#simple-soap-string-assignment)
    - [Vector style assignment](#vector-style-assignment)
    - [GSoap and namespace conflicts](#gsoap-and-namespace-conflicts)
    - [GSoap file generation - splitting files](#gsoap-file-generation---splitting-files)
  - [GTest](#gtest)
    - [TEST, TEST_F, TEST_P](#test-test_f-test_p)
    - [Custom Failure Message in Assertions](#custom-failure-message-in-assertions)
  - [Celero benchmarking](#celero-benchmarking)
  - [Windows compiling C code](#windows-compiling-c-code)
  - [Printing a C String](#printing-a-c-string)
  - [Boost libraries](#boost-libraries)
    - [Installing](#installing)
    - [Date and Time stuff](#date-and-time-stuff)
    - [Boost String manipulation](#boost-string-manipulation)
      - [String Splitting using boost (among others)](#string-splitting-using-boost-among-others)
  - [C++ examples](#c-examples)
    - [auto&& auto - auto type deduction in range based for loops](#auto-auto---auto-type-deduction-in-range-based-for-loops)
    - [References and Pointers](#references-and-pointers)
      - [Pointer Links](#pointer-links)
    - [String Manipulation](#string-manipulation)
      - [Printing integers, appending to strings](#printing-integers-appending-to-strings)
    - [Includes](#includes)
      - [Difference between include "" and include <>](#difference-between-include--and-include-)
    - [cin to read input](#cin-to-read-input)
    - [string::assign vs assignment operator "="](#stringassign-vs-assignment-operator-)
    - [Named Parameters](#named-parameters)
      - [Enums and pointers to enums](#enums-and-pointers-to-enums)
  - [Vectors, Maps etc](#vectors-maps-etc)
    - [Map](#map)
      - [Map with struct as a key](#map-with-struct-as-a-key)
    - [Vectors](#vectors)
    - [Vector initialize](#vector-initialize)
    - [Vector basic operations](#vector-basic-operations)
    - [Vector size - size_type](#vector-size---size_type)
    - [Vector searching](#vector-searching)
    - [Vector (and containers in general) removing things in-place](#vector-and-containers-in-general-removing-things-in-place)
  - [Constructors - default, delete and explicit keywords](#constructors---default-delete-and-explicit-keywords)
    - [Default](#default)
    - [Delete](#delete)
    - [Explicit](#explicit)
    - [Initialization](#initialization)
  - [C++ Stack and Heap](#c-stack-and-heap)
  - [Pragma directive](#pragma-directive)
  - [Macros](#macros)
  - [Static](#static)
  - [Constant tips from Nico](#constant-tips-from-nico)
  - [Standard Template Library](#standard-template-library)
  - [Callbacks and lambdas](#callbacks-and-lambdas)
  - [Forward Declarations](#forward-declarations)
  - [Functions](#functions)
  - [Building C++ projects](#building-c-projects)
    - [Compiler information](#compiler-information)
    - [CMake](#cmake)
    - [Quick summary](#quick-summary)
    - [Build also with Ninja](#build-also-with-ninja)
  - [List of C++ Learning Topics initial](#list-of-c-learning-topics-initial)
  - [C++ Advanced Course Notes](#c-advanced-course-notes)
    - [Topics I need to know better](#topics-i-need-to-know-better)
    - [Course Overview](#course-overview)
    - [Notes](#notes)
      - [References](#references)
      - [see slide 14](#see-slide-14)
    - [Slide 16 NBNBNB VERY IMPORTANT](#slide-16-nbnbnb-very-important)
    - [Working with pointers and references](#working-with-pointers-and-references)
    - [Template Basics](#template-basics)
    - [Function Template](#function-template)
      - [Example](#example)
    - [Smart Pointers](#smart-pointers)
    - [Exceptions](#exceptions)
      - [Rethrowing an exception](#rethrowing-an-exception)
    - [Templates Continued](#templates-continued)
    - [STL Library stuff](#stl-library-stuff)
  - [UBUNTU Suspend notes](#ubuntu-suspend-notes)

- C++ in 21 days - <http://101.lv/learn/C++/>
- <http://www.icce.rug.nl/documents/cplusplus/>

## C/C++ Learning

- Chemno project for C++ learning -
    <https://www.youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb>
- C++ reference - <https://en.cppreference.com/>
- This is one of the best reference guides and tutorial -
    <https://www.learncpp.com/>
- <http://www.cprogramming.com/tutorial/c-tutorial.html>
- <http://www.slideshare.net/EmertxeSlides/c-programming-refresher-part-i>
- <https://github.com/humzashah/c_refresher>
- From DC learnings internal
      - <http://www.worldbestlearningcenter.com/index_files/cpp-tutorial-questions-answers-pointers-partII.htm>
      - <https://openclassrooms.com/fr/courses/1894236-programmez-avec-le-langage-c>
  - Most Vexing parse problem - <https://en.wikipedia.org/wiki/Most_vexing_parse>

### My Small TODO list for basic C learning

TODO - Make a basic C++ learning page - keep this one for interesting
technical features - eventually add/create the advanced stuff too.

- Class declaration
- Instance data members and functions
- class data members and functions
- inheritance virtual functions etc.
- Define compiling, linking etc.
- bibliography

## GSoap

- GSoap Basics: <https://en.wikipedia.org/wiki/GSOAP>
  - Tutorials: <https://www.genivia.com/dev.html>
  - <https://www.genivia.com/tutorials.html>
- Create a String/object for GSoap -
    <https://stackoverflow.com/questions/26397332/how-to-allocate-a-c-object-in-gsoap>
- Also very relevant link directly to the docs for memory allocation
    and management (e.g. how to allocate for a string etc. so GSoap
    looks after creating+destroying)
  - <https://www.genivia.com/doc/databinding/html/index.html#memory2>

### Simple Soap String assignment

```cpp
    // iSoap is the main soap structure object created before
    std::string *name = soap_new_std__string(iSoap);
    std::string  someName = "Mr Name";
    name->assign(someName);
```

### Vector style assignment

```cpp
    std::vector<ParameterType *> &parameters = DEREF(SomeMessage::soap_new_std__vectorTemplateOfPointerToSomeMessage__CurParameterType(iSoap));
    parameters.emplace_back(someParameterType);
```

### GSoap and namespace conflicts

- <https://stackoverflow.com/questions/33097098/gsoap-with-multiple-wsdls-with-same-operations>

### GSoap file generation - splitting files

- <https://www.genivia.com/doc/guide/html/index.html#soapcpp2-f>

**soapcpp2 -f**

This option splits the serialization source code saved to soapC.c and soapC.cpp files into multiple soapC_NNN files as specified by the numeric parameter. This option alleviates compilation issues with very large source code files.

For example:

soapcpp2 -f40 file.h

This generates multiple soapC_NNN.cpp files each with 40 serializers, with NNN counting from 001 onward.

The value of this option must be larger or equal to 10.

## GTest

- Testing in C++
  - From Google a GTest Primer -
        <https://github.com/google/googletest/blob/master/googletest/docs/primer.md>
  - GMock info -
        <https://stackoverflow.com/questions/13696376/what-is-the-difference-between-gtest-and-gmock>
  - Setup and teardown -
        <https://stackoverflow.com/questions/45808171/why-are-setup-teardown-virtual-in-gtest>
        - override vs virtual for an overriden function (use override from C++11 onwards but equivalent)
  - <https://stackoverflow.com/questions/26030700/unit-testing-c-setup-and-teardown>
  - <https://developer.ibm.com/articles/au-googletestingframework/>
  - Alternative to GMock - FSeam -
        <https://www.fluentcpp.com/2019/07/02/fseam-a-mocking-framework-that-requires-no-change-in-code-part-1/>

### TEST, TEST_F, TEST_P

These are different use cases for GTest [Stack Overflow question about the diffs with nice explanation](https://stackoverflow.com/questions/58600728/what-is-the-difference-between-test-test-f-and-test-p) and the docs [Link to TEST_F docs](https://stackoverflow.com/questions/58600728/what-is-the-difference-between-test-test-f-and-test-p)

- TEST - individual tests
- TEST_F - test fixtures if you want tests on the same data
- TEST_P - tests with parameters

### Custom Failure Message in Assertions

When failing a test you can add a custom message like this:

- from Assertions section in -
    <https://github.com/google/googletest/blob/master/googletest/docs/primer.md>

```cpp
  EXPECT_EQ(expected, actual) << "Expected not equal to actual...";
```

## Celero benchmarking

- Main git hub - <https://github.com/DigitalInBlue/Celero>
  - TODO - see how to output in csv

## Windows compiling C code

- <https://arachnoid.com/cpptutor/setup_windows.html>
- <https://sourceforge.net/projects/mingw-w64/>

## Printing a C String

```cpp
  #include<stdio.h>

  void main()
  {
    char name[]="siva";
    printf("%s\n",name);
    printf("%c\n",*name);
  }
```

## Boost libraries

### Installing

- Install the package: sudo apt install libboost-all-dev
- Otherwise it can be included from other dependencies in your projects

### Date and Time stuff

- Boost date time stuff -
    <https://www.boost.org/doc/libs/1_55_0/doc/html/date_time/posix_time.html>

```cpp
  if(today.someTime() == tomorrow.someTime()){ // blah }
  // Instantiate - h, m, s, fs
  boost::posix_time::time_duration departureTime(1, 2, 3, 4);
```

- <https://www.boost.org/doc/libs/1_73_0/doc/html/date_time/gregorian.html>

```cpp
  // Instantiate from a string
  boost::gregorian::date d(boost::gregorian::from_string("2020-03-05"));
```

- Default date time or duration value:
  - **not_a_date_time** is the default value and can check with .is_not_a_date_time() function.

```cpp
 boost::date_time::not_a_date_time
```

### Boost String manipulation

- Boost checking if string starts with -
  - boost::starts_with(argv[1], "--foo="))
- other functions also like that - see Boost for more infos
  - <https://www.boost.org/doc/libs/1_60_0/doc/html/string_algo.html>
  - <https://www.boost.org/doc/libs/1_60_0/doc/html/string_algo/quickref.html#idm45555128584624>

#### String Splitting using boost (among others)

- [Examples of splitting string in multiple ways including boost::split](http://www.martinbroadhurst.com/how-to-split-a-string-in-c.html)

## C++ examples

### auto&& auto - auto type deduction in range based for loops

- <https://blog.petrzemek.net/2016/08/17/auto-type-deduction-in-range-based-for-loops/>
  - Information about using const auto&, auto&& etc. in loops and the different implications.

### References and Pointers

- References are like the difference between primitives and objects in Java
- int a = 4; int& b = a;
  - if **a** changes value **b** does too since it's like another label for **a**
- Can't change the assignment of **b** once applied.
- Also reference can't be null, must be an object
- To pass a pointer to something expecting a ref, we can just deref the pointer
  - e.g. Blah &blah = *somePointerBlah;

TODO -> example from Julien with pointers and addresses...

#### Pointer Links

- Basic introduction to Pointers -
    <https://www.brainstobytes.com/a-gentle-introduction-to-pointers-in-c/>
- [Wikipedia Reference in
    C++](https://en.wikipedia.org/wiki/Reference_(C%2B%2B))
- <https://stackoverflow.com/questions/10172735/how-to-cast-convert-pointer-to-reference-in-c>
- <https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp4_PointerReference.html>
- <https://stackoverflow.com/questions/4955198/what-does-dereferencing-a-pointer-mean>

### String Manipulation

- **Comparing** Should use == comparing for C++ 11 onwards
- Appending number to a string - std::to_string(i)
- Substring -> str.substr (3,5);
- Boost checking if string starts with -
  - boost::starts_with(argv[1], "--foo="))
- other functions also like that - see Boost for more infos
  - <https://www.boost.org/doc/libs/1_60_0/doc/html/string_algo.html>
  - <https://www.boost.org/doc/libs/1_60_0/doc/html/string_algo/quickref.html#idm45555128584624>
- Erase part of a string
  - myString.erase(0, myString.find("\n") + 1);
  - Check for empty string
    - if(myString.empty())
      - <http://www.cplusplus.com/reference/string/string/empty>

#### Printing integers, appending to strings

- [Different ways of having int as string and concatenating](https://www.techiedelight.com/concatenate-integer-string-object-cpp)

``` cpp
#include <iostream>
#include <string>
#include <sstream>
 
std::string toString(auto &i){
   std::stringstream ss;
   ss << i;
 
   return ss.str();
}
 
int main()
{
    int i = 17;
    std::string s = "C++" + toString(i);
 
    std::cout << s << '\n';
 
    return 0;
}
```
 
### Includes

#### Difference between include "" and include <>

On most compilers, using the "" first checks your local
directory, and if it doesn't find a match then moves on to check the
system paths. Using <> starts the search with system headers.

Typical rule of thumb is "" for your own headers, <> for system includes.

### cin to read input

```cpp
// Read a line of text, including spaces etc
getline(cin, theName);

// Read some text, stopping at first whitespace
cin >> theName;
```

### string::assign vs assignment operator "="

Both are basically the same, the only time that .assign() gives an
advantage is if you specify the exact size of the string to be assigned.

- <http://www.cplusplus.com/reference/string/string/assign/>
- <https://stackoverflow.com/questions/34196053/stdstringassign-vs-stdstringoperator>

NB - could be nicer syntax wise for assignment with pointers

```cpp
// Assign vs = (result is the same + speed is the same)
std::string name; std::string temp = "blah";

name.assign(temp); // same as name = temp;

// example with pointer
std::string *name; name->assign(temp);
name = &temp; // Maybe a little less easy to read???

// Example where assign is quicker
test2.assign("Hello again", sizeof("Hello again") - 1); // don't copy the null terminator!
// or
test2.assign("Hello again", 11);
```

### Named Parameters

C++ functions have default parameter values but not named parameters.
Below are two examples of how to implement a solution for this:

- <https://www.fluentcpp.com/2018/12/14/named-arguments-cpp/>
- <https://en.wikibooks.org/wiki/More_C%2B%2B_Idioms/Named_Parameter>

#### Enums and pointers to enums

In the C-style/pre-C++11 style enums here's an example of working with
a GSoap pointer to an enum value:

```cpp
    MyEnumType *getMeAValueOfEnumType(struct soap *iSoap) {

    enum MyEnumType *typeCode = nullptr;

    typeCode = BlahSchemaWebService::soap_new_MyEnumType(iSoap);
    // This is the interesting bit - ref the typeCode value and assign it the value of your enum value.
    *typeCode = MyEnumType::BLUE;

    return typeCode;

}
```

## Vectors, Maps etc

### Map

<http://www.cplusplus.com/reference/map/map/find/>

```cpp
// it is an Iterator
it = mymap.find('b');
if (it != mymap.end())
  mymap.erase (it);
```

- Unordered map vs map -
    <https://www.geeksforgeeks.org/map-vs-unordered_map-c/>
  - If you need guaranteed perf - map is better -> backed by BST
  - If you have no memory constraint and good hashing -
        unordered_map can be faster...

#### Map with struct as a key

If using a map with a key which is a struct or complex key, there needs to be a hash function provided also to handle key collisions

- <https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-user-defined-class-in-cpp/>
- <https://www.techiedelight.com/use-struct-key-std-unordered_map-cpp/>

### Vectors

- Reference - <http://www.cplusplus.com/reference/vector/vector/vector/>

### Vector initialize

- From C++11 you can initialize vector via initializer_list
  - <https://stackoverflow.com/questions/14414832/why-use-initializer-list-instead-of-vector-in-parameters>

```cpp
  std::vector<std::string> v = {"foo", "bar"};
```

- Declaring a vector will initialize an empty vector so can check this with v.empty();

### Vector basic operations

- front() - get the item from the front of the vector
- back() - get the item from the back of the vector
- emplace_back()/push_back() - adding items to the back of the vector - STD way to add to the vector
  - emplace_back can take varadic args
  - in some cases emplace_back might avoid creating extra objects
    - <https://stackoverflow.com/questions/4303513/push-back-vs-emplace-back>
- empty() check if the vector is empty

```cpp
#include <iostream>
#include <vector>

int main () {

    std::vector<int> myvector;

    myvector.push_back(78);
    myvector.push_back(16);

    // now front equals 78, and back 16

    myvector.front() -= myvector.back();

    std::cout << "myvector.front() is now " << myvector.front() << '\n';

    return 0;
}
```

### Vector size - size_type

A vector size is not an int - it's a size_type. The type of the size of
an **std::vector<T>** is **std::vector<T>::size_type**

Be careful with this kind of thing when iterating.

The vector size is:

- NOT int
- NOT unsigned_int
- NOT size_t

TODO - add to this once I discuss with someone more knowledgeable

### Vector searching

Finding elements in a vector in different ways -
<https://thispointer.com/c-how-to-find-an-element-in-vector-and-get-its-index/>

- std::find_if - can take a custom function to use for matching
- C++11 has range based for loop for(auto && blah: blahs)...

TODO - ask/learn more about both approaches

### Vector (and containers in general) removing things in-place

- DON'T use counters and container.size()
- DO USE -  iterator and container.end() with erase/remove functions
  - <https://www.freecodecamp.org/news/how-to-remove-elements-from-a-container-in-c/>
  - <https://www.fluentcpp.com/2018/09/14/how-to-remove-elements-from-a-sequence-container/>

## Constructors - default, delete and explicit keywords

### Default

- Default - <http://www.stroustrup.com/C++11FAQ.html#default>

### Delete

```cpp
class X {

      // ...
      X& operator=(const X&) = delete;  // Disallow copying
      X(const X&) = delete;

};
```

### Explicit

- Should be used with single argument constructors to avoid any
    implicit conversions
- Implicit conversion could be using the constructor as a conversion
    constructor to transform an input to another function into an object
    of that class type (e.g. in the Deitel book (10.13 explicit
    Constructors and Conversion Operators)
- Example shown below:

```cpp
class Account {
  public:
    explicit Account(std::string accountName) : name{accountName} {
      // empty body
    }
};
```

### Initialization

- <https://en.cppreference.com/w/cpp/language/data_members#Member_initialization>
- Plenty of info on construction/intialization -
    <https://en.cppreference.com/w/cpp/language/constructor>
- Info about when to use Intializer lists -
    <https://www.geeksforgeeks.org/when-do-we-use-initializer-list-in-c/>
- Or even -
    <https://www.studytonight.com/cpp/initializer-list-in-cpp.php>

```cpp
#include <iostream>

int x = 0; struct S {

      int n = ++x;
      S() { }                 // uses default member initializer
      S(int arg) : n(arg) { } // uses member initializer

};

int main() {

      std::cout << x << '\n'; // prints 0
      S s1;
      std::cout << x << '\n'; // prints 1 (default initializer ran)
      S s2(7);
      std::cout << x << '\n'; // prints 1 (default initializer did not run)
      std::cout << s2.n << '\n'; // prints 7 - value initialized into n

}
```

- BIG NB - A Reference member variable MUST be initialized in the
    constructor intializer list

``` cpp
          class MyClass {
           public:
             MyClass(int, AnotherClass& a); // NO CAN'T DO THIS
             MyClass(int iAmount, AnotherClass& a): amount(iAmount), myRefMember(a){} // MUST do like this

           private:
            int amount;
            AnotherClass& myRefMember;
           };
```

- This is the type of error you'll see if not
  - “'MyClass::myRefMember' must be initialized in constructor base/member initializer list”.

## C++ Stack and Heap

- Heap
  - anything from a "new" - e.g. new int(5); i.e. dynamic memory
  - If using "new" you MUST HAVE A corresponding "delete"
- Stack
  - anything directly created

## Pragma directive

<https://www.google.com/search?client=ubuntu&channel=fs&q=%23pragma+once&ie=utf-8&oe=utf-8>

If you want something to be included only once in a compilation use the
following in the beginning of the file as a preprocessor directive:

```cpp
#pragma once
```

## Macros

- Macro examples - <https://www.geeksforgeeks.org/cc-preprocessors/>

## Static

Static in C++ means that the code is executed ONCE per application
lifecycle. This could be tricky for example a function local static
might LOOK like it gets executed more than once but only the first
execution is taken into account. Putting inside a function is a way of
having a predictable initialization time for the var.

## Constant tips from Nico

- Never put something as static with a declaration in the header file - it will get duplicated into the including code files so there  will be a duplicate e.g. string in every file
- Instead use extern for the declaration and initialize in the .cpp
    file.

Need to understand more on this....

## Standard Template Library

- <https://en.wikipedia.org/wiki/Standard_Template_Library>
  - <https://en.wikipedia.org/wiki/Standard_Template_Library#Containers>

## Callbacks and lambdas

Idea for me to use for the logging messages:

- <https://www.google.com/search?client=ubuntu&channel=fs&q=C%2B%2B+idea+of+a+callback&ie=utf-8&oe=utf-8>
- <https://stackoverflow.com/questions/2298242/callback-functions-in-c>
- <https://learning.oreilly.com/library/view/c-cookbook/0596007612/ch15s02.html>
- <http://tedfelix.com/software/c++-callbacks.html>

## Forward Declarations

- Forward declaration -
    <https://www.learncpp.com/cpp-tutorial/forward-declarations/>
- <https://en.wikipedia.org/wiki/Forward_declaration>

Used to declare something before it is defined. extern keyword required
if something declared OUTSIDE the same file. I think this can be useful
also for making recompilation more efficient... TODO - expand on this
point.

- <https://stackoverflow.com/questions/4757565/what-are-forward-declarations-in-c>
  - **How forward-declarations can significantly reduce build times -**
    - You can get the declaration of a function into your current
            .cpp or .h file by #including the header that already
            contains a declaration of the function. However, this can
            slow down your compile, especially if you #include a header
            into a .h instead of .cpp of your program, as everything
            that #includes the .h you're writing would end up
            #include'ing all the headers you wrote #includes for too.
            Suddenly, the compiler has #included pages and pages of
            code that it needs to compile even when you only wanted to
            use one or two functions. To avoid this, you can use a
            forward-declaration and just type the declaration of the
            function yourself at the top of the file. If you're only
            using a few functions, this can really make your compiles
            quicker compared to always #including the header. For
            really large projects, the difference could be an hour or
            more of compile time bought down to a few minutes.

```cpp
#include <iostream>

int add(int x, int y); // forward declaration of add() (using a function prototype)

int main() {

      std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n'; // this works because we forward declared add() above
      return 0;
}

// even though the body of add() isn't defined until here 
int add(int x, int y){
      return x + y;
}
```

## Functions

- [Using default in a function declaration (also applies to operators etc.)](https://stackoverflow.com/questions/6502828/what-does-default-mean-after-a-class-function-declaration?noredirect=1&lq=1)

It's a feature introduced in C++11 - it means that you want to use the compiler-generated version of that function, so you don't need to specify a body.

## Building C++ projects

### Compiler information

- How compiler works - <https://www.toptal.com/c-plus-plus/c-plus-plus-understanding-compilation>
- Stackoverflow expl of .a and .so files - <https://stackoverflow.com/questions/9809213/what-are-a-and-so-files>
  - .a is statically linked archive from compile time - if it changes you need to recompile
  - .so is shared object - it can change independently of your code since only linked at runtime (with ln command).

### CMake

This seems like a very good way of handling complex makefiles

- <https://cmake.org/cmake-tutorial/>
- <http://derekmolloy.ie/hello-world-introductions-to-cmake/>
- <https://blog.kitware.com/cmake-building-with-all-your-cores/>
- <https://cliutils.gitlab.io/modern-cmake/chapters/intro/running.html>

### Quick summary

- CMakeLists.txt file contains details of folders and files to build
- § cmake . - builds the makefile
- § make - executes makefile to create binary etc.
- § ./hello - execute your file

### Build also with Ninja

- <https://dmerej.info/blog/post/chuck-norris-part-1-cmake-ninja/>

------------------------------------------------------------------------

## List of C++ Learning Topics initial

- References
- auto auto&&
- rvalue and lvalue
- Copy constructor along with example from Julien
- Data members
  - "Always intialized in order of declaration in class definition
        regardless of order in initialization list" what does this mean
- Syntax of constructor - void print(int i): a1(i).....
- cpp vs hpp - where does the class {} declaration go etc.
- friend functions
  - member/non-member function
  - friend class
- inheritance example
  - constructor + destructor + defaults e.g. non-arg constructor
  - copy constructor
  - access control
- p54 - object conversions - pointers + access violations
- templates
- bibliography
  - Obj oriented prog using C++ 2ed Ira Pohl
  - Thinking in C++ 2ed Bruce Eckel
  - C++ Programming language Bjarne Stroustrup

## C++ Advanced Course Notes

- sudo apt install g++ make cmake vim valgrind

### Topics I need to know better

- Macros
- assert vs static_assert
- Templates
- Overloading operators
- Unique, shared pointers in boost - see where they're used in real projects
    code and slides 64 onwards - also in the exercise 3
  - example unique_pointer here
        <https://en.cppreference.com/book/intro/smart_pointers>
- RAII also
- Virtual functions implementation and vtab
- Name mangling - way of handling overloaded method names in linker
- Friend functions and classes
- extern - different compilation unit not static
- namespaces - using vs using namespace + rules like not having
    "using namespace" in a header file
- Anonymous namespaces and the typedefs for C++11 vs old C/C++03 style
    typedef
- STL overview + look at Container memory allocation scheme -
    allocator
- Containers - deque look at it double ended queue, binary tree in a
    vector impl (i- children are 2\*i, 2\*i+1)
- Function operators

NB - lab mentions CMake Cache removal -> could this be useful for us
too?

### Course Overview

- **1. Basic C++ concepts and mechanisms**
  - Objects, types, and classes
  - Template basics
  - Ownership smart pointers (C++11)
- **2. Advanced C++ mechanisms**
  - Exceptions
  - Templates and overloading
  - RTTI and ISO C++ casts
  - Multiple inheritance
  - Namespaces
- **3. The Standard Template Library (STL)**
  - Containers and iterators
  - Function-objects
  - C++11 lambdas
  - Algorithms, strings, and IO streams
  - Exception safety

### Notes

- C++ compile - error doesn't stop compilation but stop any code
    being generated at the end
- auto is a C keyword but is redundant -> e.g. in a for loop - auto
    int i; and int i; are the same - the variable scope is limited to
    the block where it is declared.
- using auto keyword -> compiler relies only on the expression to
    determine the type for the variable.

- for loops

``` cpp
for (string elem : vs) cout << elem << ‘ ‘; // NB - could end up with a copy here
for (string& elem : vs) elem = "";          // Better to use a reference
for (auto elem : vs) cout << elem << ‘ ‘;
for (auto& elem : vs) elem = "";
for (auto&& elem : vs) elem = “hello”;      // Most efficient way of doing it -> will adapt to all situations but for now I have no idea how it works - need to do the C++ libraries course :)
```

#### References

- used a lot for passing function params.

Allows to modify external objects within a function IMPORTANT - C++
passes parameters by VALUE only so ref allows passing args which can be
used to modify things outside the function

#### see slide 14

- example of refs vs pointers for an integer swap function...
- **const should be used as much as possible** - e.g. if passing a ref
    to a function where we are sure we don't want to modify the obj

``` cpp
 void someFunction( const MyClass &object) {
    // Do stuff using a const ref since you do not want to modify object
 }
```

Slide 15

- references behave as non null constant pointers -> cannot point to NULL with ref, once ref points to some object it must remain pointed there.

Like a java final object - can modify the values of the object via the
ref but cannot change the object pointed to.

### Slide 16 NBNBNB VERY IMPORTANT

- Explains why we need refs vs pointers in C++ -> ambiguity of the & with pointers

Slide 21

- interesting user defined implicit conversion -> r + 2 can be
    converted to r + Rational(2) by compiler due to having an available
    one-arg constructor

Slide 25

- Shows where variables are defined + live (e.g. heap/stack)

Slide 26 - Constructors

- should favour the "member intialization list" -
  - C::C() : A(), b() {}
  - Instead of putting constructor intialization calls inside the {}
        body
  - Some calls e.g. call to parent class constructor can ONLY be
        done there
  - Also reference assignment/init can ONLY be done in member
        initialization list

Destructors

- IOStreams - nearly last things to be destroyed by destructors ->
    e.g. cin, cout - allow them to be available as long as possible

Slide 31

- Order of declaration + instantiation in member intialization list is
    REALLY IMPORTANT, especially for inheritance etc.

``` cpp
class B : public A1, public A2 { // A1 then A2
private:
string _s; // initialized first
int _dim; // initialized second
public:
B(const string& s) : _dim(_s.size()), A1(_dim), _s(s) // WRONG - A1 called before _dim is intialized
{...}
// CORRECT - respect the order and use input to constructor instead of mixing with member vars (i.e. s instead of _s)
B(const string& s) : A1(s.size(), _s(s), _dim(s.size())
```

Slide 36

- RVO - return value optimisation -> for a simple copy the C++11
    compiler onwards will allocate the memory directly at caller level
    to avoid doing a temp object which could be expensive (e.g. a = b
    does a simple copy - in effect it's like a call to a function with
    a temp object created then the value returned and copied into the a
    variable. Now the temp object is not created, instead a is allocated
    directly)

### Working with pointers and references

- accessing properties using reference - dog.name
- accessing properties using pointer - dog->name

**Returning a reference:**

``` cpp
  return *this;
```

  *Slide 41
      * Shows use of **default** and **delete** to indicate default functions and to prevent using functions like destructor etc.

Better than defining a class with private constructor, copy constructor
etc.

### Template Basics

- **Slide 47 Templates**
  - template function is a SET of functions - one for every single
        possible type
  - template class is a SET of classes
  - The mechanisms for functions and classes are different

### Function Template

#### Example

```cpp
template <typename T>
const T& Min(const T& a, const T& b) {
    return a < b ? a : b;
}
```

- Using function template
  - parameterized overloaded function:

```cpp
  int x, y, z; z = Min(x, y);
```

- explicit instantiation (if effective params cannot be deduced):
        int x; double m = Min<double>(x, 5.7);

TODO add my Template notes here...

### Smart Pointers

- unique pointers
- shared pointers
- weak pointers

------------------------------------------------------------------------

**TODO -> Review slides 60-80 for shared pointers since I missed this
bit**

------------------------------------------------------------------------

- Smart pointers and performance overheard -
    <https://www.modernescpp.com/index.php/memory-and-performance-overhead-of-smart-pointer>
- MS docs -
    <https://docs.microsoft.com/en-us/cpp/cpp/smart-pointers-modern-cpp?view=vs-2019>
- Cherno video - <https://www.youtube.com/watch?v=UOB7-B2MfwA>
- Nice example of smart pointers and memory allocation plus discussion
  - <https://www.reddit.com/r/cpp_questions/comments/fckt3h/why_this_line_of_code_causes_2_heap_allocations/>

### Exceptions

- link to std::exceptions -
    <https://en.cppreference.com/w/cpp/error/exception>
- Slide 85 - exceptions
  - destructor is automatic once an exception stops being
        propagated
  - C and C++ -> cannot call main() directly - forbidden by
        language but in any case would miss the necessary context to run

- Example of catch BY REFERENCE -> this is preferred way since it
    avoids a copy of the exception object

```cpp
catch (Stack::exception& e) {
  cout << e.what();
}
```

#### Rethrowing an exception

Exceptions can be rethrown if not handled by a particular piece of code by using "throw;" i.e. without any argument.

```cpp
try {
  mayThrowMyErr();
} catch (myErr &err) {
  err.append("Add to my message here");
  throw; // this throws the same object
  throw err; // this throws a copy of the object -> might lose the appended messages etc. if using inheritance - you will lose derived-class-specific data
}

```

- <https://stackoverflow.com/questions/2360597/c-exceptions-questions-on-rethrow-of-original-exception>
- <https://caligari.dartmouth.edu/doc/ibmcxx/en_US/doc/language/ref/rnrethro.htm>

From above link:

> Rethrowing an Exception
>
> If a catch block cannot handle the particular exception it has caught , you can rethrow the exception. The rethrow expression > (throw with no argument) causes the originally thrown object to be rethrown.
>
> Because the exception has already been caught at the scope in which the rethrow expression occurs, it is rethrown out to the next > dynamically enclosing try block. Therefore, it cannot be handled by catch blocks at the scope in which the rethrow expression > occurred. Any catch blocks following the dynamically enclosing try block have an opportunity to catch the exception.
>
> The rethrow expression can be caught by any catch whose argument matches the argument of the exception originally thrown. 

- Slide 92

```cpp
  // Top level exception class - defined in ISO standard
  class exception {
       public:
          virtual const char *what() const noexcept;
          };
```

- what() should return a string describing the message
  - NB - char instead of std::string because a std::string could throw an exception.
  - last const means it will not modify the containing class
  - noexcept means it doesn't throw an exception (C++11 onwards, C++03 used throw() i.e. an empty list of thrown exceptions)

- around slide 96 -
  - no finally clause in C++
  - destructor is more or less equiv to finalize() in java
  - BUT destructor **guaranteed** to be called in C++.
  - In java finalize() only called if GC decides it.

- Slide 99
  - In a constructor can add a try + catch but it's not pretty

```cpp

B(const string& s) try : A(s) {
  // constructor code
} catch(Exc_A) {
  // clean up after exception
  // IMPLICIT THROW ADDED by C++ compiler so you don't think the object is correctly created,
  // the catch only allows you to cleanup
  throw;
}
```

TODO - look more at this

- Slide 100
  - Exception safe code
  - book suggestions - Herb Sutter - exceptional C++ and more exceptional C++
    - <https://www.oreilly.com/library/view/more-exceptional-c/020170434X/ch01.html>

- Slide 132
  - TypeInfo - size increases with number of virtual functions and
        dynamic type identification.
  - Reduced use in today's programs due to template use - can even
        use compiler option if sure not to use it

- Slide 137
  - Details of dynamic_cast and static_cast

### Templates Continued

- Slide 104
  - C++ / other static type languages, class template instances are
        not implicitly convertible - e.g. set of French people is
        implicitly part of set of humans but not for C++

This is necessary to preserve static type checking - e.g. refer to a set
of French as a set of Humans but without being able to add an English
person via the set of Humans i.e. a Set<int> is not implicitly
convertible to Set<double>

- Slide 107

Shows an example of our exercise from yesterday where we wanted to have
a parent-child conversion via template parameter

- Slide 108

vtab example to explain why member templates can never be virtual one
vtab per class (need to understand more about vtab and virtual
functions)

- article explaining vtables - <https://pabloariasal.github.io/2017/06/10/understanding-virtual-tables/>

- Slide 156

Namespaces - never put "using namespace" in the header file since it
will end up including namespace and any includes within....can be very
big

- Slide 157

Backward compatibility and ISO standards #include <utility> -> C++
way to include a standard library #include <cstdio> and not #include
<stdio.h> - makes ANSI C functions available in the std namespace

- Slide 160

Anonymous namespace and the using BLAH = std::string; that we use to
have a nice way to refer to stuff NB - removes need for typedef
std::string BLAH that was used in C

- Slide 165 - 168

Namespaces and function hiding + inheritance - worth reviewing

NB - access control in C++ is "Software engineering" control so you
can always "cheat" by working around private etc. e.g. in the
namespaces you can abuse "using A::f" in a child class to expose
private methods of A as public.

- Slide 173
  - Also the overloading of java doesn't exist in the same way for
        C++ -
    - see the example where f(int) of child class B hides f(char)
            of parent class A unless you have using A::f in the child
            class B
    - This is because compiler sees "f" as a property -
      - i.e. same in A and B so B is taken - unless you have
                "using" statement to bring the def down to class B
                level.

### STL Library stuff

- Slide 181 STL library stuff - template container with Allocator

- Slide 186
  - Collections Algorithms of STL - no idea about objects it
        manipulates.
  - Results in super fast efficient code but no safety -
    - e.g. pointer to BEGIN and END are expected to be part of
            same collection, if not then undefined behaviour.

STL uses no inheritance and has no object orientation...

- Slide 189
  - STL Containers from C++11 on can initialize like C aggregate ->

  ```cpp
     vector<int> v = {2, 3, 4, 5};
  ```

  - Also for example, maps can use this

- Slide 192
  - Collections example showing map using iterator with ->first and
      ->second to have key and value.

- Slide 193
  - Container value_types must have copy operations to allow copying
        value into element of the container.

- Slide 198
  - STL Algorithms don't ever change the size of a container (even
        algos which modify elements of container) - due to using simple
        pointers as iterators.

- Slide 202
  - Function objects - functor - class that defines operator()

```cpp
            class is_gt_4 {
            public:
              bool operator()(int i) {return i > 4;}
            };

```

- Slide 206
  - Lambda calculus - 1936 alonso church prof of turing

- Slides 206-220
  - lambda examples ->
  - NB I'm using C++11 so some C++14 features are not available.

- Slide 223
  - Insert algorithms to add new elements with special iterators.
  - Work around the fact that the algorithm will not modify size of
        a container.

- Slide 225
  - Remove algorithms -> DONT remove anything - instead will return
        a pointer to the end of a new sublist.
  - Then can use this to call for example

  ```cpp
    li.erase(xxx, li.end)
  ```

  which really does remove the elements.
  - See the slide for example.

## UBUNTU Suspend notes

- <https://askubuntu.com/questions/1164371/suspend-issue-on-kernel-5-0>
- hibernate vs suspend -
    <https://www.addictivetips.com/ubuntu-linux-tips/restore-hibernate-mode-on-ubuntu/>
- Troubleshooting -
    <https://ubuntuforums.org/showthread.php?t=2395562>
- <https://www.dell.com/community/Inspiron/Suspend-resume-problems-on-Ubuntu-18-04/td-p/6072410>
- <https://askubuntu.com/questions/1062369/how-to-disable-auto-sleep-in-ubuntu-18-04>
- <https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1801743> -
    this has some interesting notes from Nadi 2018-12-09 -- finally NO
    NOT really
- <http://iam.tj/prototype/enhancements/Windows-acpi_osi.html>
- <https://bugzilla.redhat.com/show_bug.cgi?id=1196943#c10> - here a
    mention of disabling usb autosuspend which looks promising
- <https://logfile.ch/linux/2017/06/15/disable-usb-autosuspend-linux/> -
    took a script from here for usb autosuspend disable + stored in
    dev/util scripts and ran with sudo

  - didn't work at all - seems perhaps a red herring in this case....
  - Discussion on pm-suspend vs systemctl suspend differences <https://unix.stackexchange.com/a/485056/350516>
  - Trying to add slock to pm-suspend based on this - <https://bbs.archlinux.org/viewtopic.php?id=96983>
  - Help with permissions issue for sleep hooks in pm-suspend -> make sure it's root:root for owner:group
  - <https://www.linuxsecrets.com/archlinux-wiki/wiki.archlinux.org/index.php/Pm-utils.html>
  - <http://iam.tj/prototype/enhancements/Windows-acpi_osi.html>
