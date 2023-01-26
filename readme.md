# ICS4U Culminating Portfolio

*By: Faizaan Aslam*

This markdown file contains all the programming knowledge I have learnt from taking the ICS4U0 course. Code examples are all from my past assignments or personal projects and have been included to better elucidate concepts. The bulk of examples are written in C++ and as such, this portfolio will mainly center around this language.

- [Documentation](#documentation)
  * [Class Documentation](#class-documentation)
  * [Extending Objects Documentation](#extending-objects-documentation)
  * [UML Class Diagrams](#uml-class-diagrams)
- [Object-Oriented Programming](#object-oriented-programming)
  * [Objects and Encapsulation](#objects-and-encapsulation)
  * [Classes, Constructors, Deconstructors](#classes--constructors--deconstructors)
  * [Inheritance, Access Modifiers, Polymorphism](#inheritance--access-modifiers--polymorphism)
  * [Abstract Classes and Interfaces](#abstract-classes-and-interfaces)
- [Algorithmic Thinking](#algorithmic-thinking)
  * [Sorting Algorithms](#sorting-algorithms)
    + [Insertion Sort](#insertion-sort)
    + [Bubble Sort](#bubble-sort)
    + [Comparison to Other Sorting Algorithms](#comparison-to-other-sorting-algorithms)
  * [Searching Algorithms](#searching-algorithms)
    + [Linear Search](#linear-search)
    + [Binary Search](#binary-search)
    + [Comparison to Other Searching Algorithms](#comparison-to-other-searching-algorithms)
  * [Recursion](#recursion)
    + [Recursive Algorithms](#recursive-algorithms)
    + [Recursion Types and Pitfalls](#recursion-types-and-pitfalls)
- [File Handling](#file-handling)
  * [File Reading](#file-reading)
  * [File Writing](#file-writing)

---

## Documentation

Even though it can be time-consuming and tedious, writing documentation is a necessity for good code. Simply put, documentation is a useful tool to make code more human readable and understandable for both the code's creator and other programmers. Adding documentation is especially useful when using others' code in your own program, such as when implementing APIs or external libraries.

Documentation is created in the form of comments written in files. Comments are lines of text in code that the compiler ignores when running a program. As such, they exist solely to help humans understand the code when reading it.

Syntax for comments come in many forms depending on the language and can either be single-lined (the comment stays on just one line in the code), or for more descriptive documentation, multi-lined (the comment can take up as many lines as needed in the code). Below is a chart illustrating comment syntax in many common languages...

| Language                            | Single-line Comment | Multi-line Comment |
| ----------------------------------- | ------------------- | ------------------ |
| C++, Java, Dart/Flutter, JavaScript | // ...              | /* ... */          |
| Python                              | # ...               | ''' ... '''        |
| Ruby                                | # ...               | =begin ... =end    |

### Class Documentation

Given how broadly classes can be used and customized, concise and clear documentation about constructors, methods, and parameters is absolutely essential for proper use. Below is an example of good class documentation from my Data Structures assignment... 

```c++
/* 1.
    A class that represents the various colours seen in ink, pens, and pencils. Has a composition relationship with Ink and Pencil.

    @author Faizaan A.
    @since 6-Oct-22
    @version 1.0
*/
class Colour
{
public:
    short red, green, blue;
    short opacity;

    /* 2.
        The constructor for the Colour class.

        @param red: short   The red value of the colour in rgb format.
        @param green: short   The green value of the colour in rgb format.
        @param blue: short   The blue value of the colour in rgb format.
        @param opacity: short   The opacity of the colour.
    */
    Colour(const short &r, const short &g, const short &b, const short &o) : red(r), green(g), blue(b), opacity(o) {}

    /* 3.
        A setter method that allows you to change the opacity of a colour.

        @param newOpacity: short   The new opacity that you want the colour to be.
    */
    inline void opacityChange(const short &newOpacity) { this->opacity = newOpacity; }
};
    
```

1. The comment at the top of a class definition is arguably the most important class documentation. Its description serves as a summary of the use of this class and answers the questions of "What does this class do?", "Why should I use this class?", and "What are the dependencies/prerequirements to use this class?". Important class attributes not specified in the constructor can also be mentioned here. Below that, the @author field indicates the author of a class if need be, @since field indicates how long it has been since this class han been created, and the @version field is the class' version. If you want to document important updates you made to a class, you can add an update log after the @version field.
   
2. The constructor documentation is vital when it comes for others to be able to properly instantiate your class. The description for a class' constructor does not have to be as detailed, unless a class has multiple constructors; in such a case, differentiating between the use case of each constructor is recommended. Below the description are all the parameters, each listed with an @param tag in front, the parameter name, the parameter type, and lastly the parameter description. The description of each parameter should be around one line and able to concisely outline what the parameter really means with respect to the class and its methods as a whole.
   
3. Each method in a class should have a detailed description of what its use is. Much like with the constructor documentation, it should also list each parameter used with an @param tag in front, the parameter name, the parameter type, and  the single-line parameter description at the end. Additionally, should the return type  be non-void, the meaning behind the value returned and its datatype should be stated with a @returns tag.

> To learn more about classes, please see: [Classes, Constructors, Deconstructors](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#classes-constructors-deconstructors)


### Extending Objects Documentation

Beyond just the basics, classes can be further customized with inheritance and abstraction/virtualization. As such, relevant documentation for how these concepts have been incorporated in a class' design is a big must, as shown below...

```c++
/* 1.
    A DoughCrayon object which extends Crayon publicly. DoughCrayons are similar to Crayons for the most part, except that they are very susceptible to heat and turn mushy quickly; this is further explained in the overwritten melt() method. The default mushiness value is still 5.
*/
class DoughCrayon : public Crayon
{
public:
    /* 2.
        The constructor for this DoughCrayon class. Calls its parent Crayon class' constructor.

        @param length: int   The length of the crayon. This is used to help identify the messages written with it in the output.
        @param colour: Colour   The colour of the crayon. Plays a key role to identify the messages written with it in the output.
    */
    DoughCrayon(const int &len, const Colour &clr) : Crayon(len, clr) {}

    /* 3.
        The melt() method for a DoughCrayon object which  overrides its parent's melt() method. Melting a DoughCrayon involves changing its mushiness value by exposing it to a specified amount of heat, which thereby affects its writing abilities.

        @param temperature: int   The temperature in Celsius that the Crayon is exposed to. Unlike a Crayon, however, the temperature will be directly added to the DoughCrayon's mushiness.
    */
    void melt(int temperature) override
    {
        this->mushiness += temperature;
        ;
    }
};
```

1. For the most part, the description for a child class is mainly the same. The one key addition to note is that it is stated which other class this class inherits from and which type of inheritance specifically--either public, private, or protected. Some general similarities between the parent and child class are also noted here.

2. Again the constructor's documentation is mostly the same, however this time, it is noted that that the constructor actually being utilized to instantiate this class is its parent class' constructor.

3. Methods in derived classes should be described with the same documentation standards as before. However, if they are overriding a parent's method or an abstract method, it should be noted as well as the changes in functionality if applicable.

> To learn more about inheritance, please see: [Inheritance, Access Modifiers, Polymorphism](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#inheritance-access-modifiers-polymorphism)

> To learn more about abstraction/virtualization, please see: [Abstract Classes + Interfaces](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#abstract-classes-and-interfaces)

### UML Class Diagrams

Unified Modeling Language (UML) Class Diagrams are a crucial tool in planning out object-oriented programs. Before you start writing code, they allow you to fully organize and lay out ideas about your classes and their functionalities, alongside brainstorm how they should relate to one another such as with composition relationships, inheritance, data shared with access modifiers, or interface implementation. This massively helps save time and energy when developing and debugging classes through giving you a big picture understanding of your program while coding, which is especially useful in low level languages like C++ where classes must be defined in a particular order for the program to run.

*Nuanced UML Class Diagram Example:*
![EDS UML Class Diagram](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio/blob/master/EDS%20UML%20Class%20Diagram%20-%20CS.G12S1%20-%20By%20Faizaan%20Aslam_page-0001.jpg)

* Each class is represented as a rectangle divided into 3 portions:
  * The first portion at the top is the class name.
    * Abstract classes are marked with an italicized title, whereas interfaces simply have `<<interface>>` written above.
  * The middle portion contains the class' attributes and their data types.
  * The end portion contains the class' methods and their return types as well as parameters with data types.
* In front of each attribute and method is either a `+`, `-`, or `#` sign. `+` means that the attribute/method is public, `-` means that it is private, and `#` means that it is protected. To learn more about the difference between these, please see: [Inheritance, Access Modifiers, Polymorphism](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#inheritance-access-modifiers-polymorphism).
* **Black Diamonds** illustrate composite relationships where the class with the diamond beneath it uses the class on the other end in its attributes and/or methods. It is indicated on the other end how many times the class is used, with `1` meaning once, `1..*` meaning at least once, and `1..n` meaning between 1 to *n* times. `1` could be replaced with any other positive integer.
* **White Triangles** indicate inheritance between classes. Specifically, the class with the triangle beneath it is the parent class and the class on the other end is the child class. This same symbol is used for classes that implement interfaces as well as classes that inherit from abstract classes.
---

## Object-Oriented Programming

Object-oriented programming (OOP) is a programming paradigm based on the idea of storing and organizing data into "Objects". It involves several concepts including but not limited to Encapsulation, Classes, Inheritance, Polymorphism, Abstraction/Virtualization, and Interfaces--these will all be explained below...

### Objects and Encapsulation 

Objects are individualized units of code that can store data members as "attributes" and perform reusable functions called "methods". Objects can be customized infinitely in theory and brings flexibility, structure, and reusability to code.

The fundamental concept behind objects is encapsulation. In short, encapsulation is a way to group data members and methods together into a specific object, as well as to restrict direct access to some components of the object. This allows portions of code to remain organized and distinct, which greatly helps programmers write more concise and understandable code.

### Classes, Constructors, Deconstructors

To create a custom object, one must first create its blueprint--this is what a class is. Classes specify what attributes the object will contain, what methods it will have, what can or cannot be accessed outside the object, and much more. After the class is defined, it can be "instantiated", or in other words, brought to life as an object in runtime. Below is an example of a simple class..

```c++
class Point
{
public:.
    int x, y; // 1.

    Point(int userX, int userY) : x(userX), y(userY) { // 2.
        std::cout << "I have been constructed." << std::endl;
    }


    void doStuff() { // 3.
        std::cout << this->x << this->y << std::endl;
    }
 
 
    ~Point() { // 4.
        std::cout << "I have been deconstructed." << std::endl;
    }
};

```

1. This line creates two integer attributes for this class. These attributes (i.e. variables) can be used throughout the class and, when instantiated, each specific object has its own copy of these attributes.

2. This is the class' constructor, a special method (i.e. function) that is called when first instantiating this class as an object. Parameters can be specified in the brackets when instantiating a class, so that the attributes of each created object can be unique and start off with different values.

3. This is one of the class' methods. Methods are just like regular functions with the exception that they belong to a specific object and can be used to modify the object if desired. Object attributes can be accessed inside methods using the prefix `this->`.

4. This is the class' deconstructor, a special method like the constructor that is called when an object made from this class is discarded from memory. They are most useful when it comes to memory garbage collection, as languages like C++ require it to be done manually.

### Inheritance, Access Modifiers, Polymorphism

Extending from the idea of classes, we have inheritance. In simple words, Inheritance lets a "child" class copy attributes and methods from its "parent" class. Looking at the bigger picture, inheritance helps you create a hierarchy of classes in your program, which really helps keep object data organized and increases code reusability. Extending on this, you can specify which attributes and methods can be passed down or generally accessible via Access Modifiers. A simple example of inheritance between an Entity class and Person class with usage of Access Modifiers is demonstrated below...

```c++
class Entity
{
private: // 1.
    double untouchableValue;

public: // 2.
    bool isAlive = true;
    int x, y;
 
    Entity(int userX, int userY) : x(userX), y(userY) { std::cout << "Called Entity constructor." << std::endl; }
 
protected: // 3.
    inline void die() { this->isAlive = false; } 
};
 
class Person : public Entity // 4.
{
public:
    std::string name;
 
    Person(std::string userName, int userX, int userY, bool death) : Entity(userX, userY), name(userName) { std::cout << "Called Person constructor." << std::endl; }
 
    inline void move(const int &x, const int &y) {
        this->x = x;
        this->y = y;
    }
};
```

1. In the Entity class, the double attribute named untouchableValue is marked as "Private" using an Access Modifier. This means that the variable can only be used by methods within the Entity class, and cannot be inherited by child classes nor modified or read by code outside the Entity object.

2. In the Entity class, the boolean attribute named isAlive, the two integers, and the class' constructor are marked as "Public" using an Access Modifier. This means that they can all be accessed/called by external code or by child classes.

3. In the Entity class, the void function named die() is marked as "Protected" using an Access Modifier. This means that only methods within the Entity class or within its derived classes can call this function.

4. The syntax for inheritance is "ChildClass : ParentClass" and there are three types of inheritance: public, private, and protected (not to be confused with Access Modifiers). Of the three, public inheritance is most commonly used and simply takes attributes/methods from its parent class as dictated by the parent class' Access Modifiers. As a result, the Person class now contains a public boolean variable, two public integer variables, and one protected void die() function copied from the Entity class, along with its own public std::string and void move() function.

A big feature when it comes to inheritance is polymorphism. Briefly explained, polymorphism is the concept of treating child classes like their parent classes. As an example from the code above, if there were a function that took in an Entity object as a parameter, I could pass in a Person object instead due to polymorphism.

### Abstract Classes and Interfaces

Abstract classes differ from regular classes given that they cannot be instantiated but only inherited from. This is because abstract classes contain abstract/virtual methods---methods that must be overwritten by a child class (i.e. given its own unique function body for every child class). Nonetheless, abstract classes can still contain some functional methods. Overall though, they are used to group functionality among classes and better layout a program's class hierarchy.

Interfaces, otherwise known as pure abstract classes, are used similarly to abstract classes with the exception that they must contain only abstract methods. Put simply, interfaces are used as guidelines to how a class should behave in design but does not restrict the class like an abstract class does. This is in fact the reason why classes can implement multiple interfaces, but only inherit from one abstract class. Shown below is an example of an interface I made in my Extending Data Structures assignment:

```c++
/*
    An interface that all other classes in this program extends from. This interface outlines all the basic functionality any utility should have if you want to write with it.
*/
class WriteableUtility
{
protected:
    int length;

    /*
    The constructor for this interface.

    @param length: int   Specifies how long this writing utility is. This is used in the program to help identify which messages were written by what utilities in the output file.
    */
public:
    WriteableUtility(const int &num) : length(num) {}

    /*
    The write method which takes a message and outputs it. This method will be overwritten by its descendants, as the output changes according to what utility is writing the message.

    @param msg: std::string   The message you want to write.
    @param paper: std::ofstream   The file output stream that the message goes to.
    */
    virtual void write(std::string msg, std::ofstream &paper) = 0;

    /*
    This method will scribble random letters and output them. This method will be overwritten by its descendants, as the output changes according to what utility is writing the message.

    @param paper: std::ofstream   The file output stream that the scribbled message goes to.
    */
    virtual inline void scribble(std::ofstream &paper) = 0;
};
```

Note that `virtual void function() = 0;` signifies that the function is a pure abstract/virtual function and must be overwritten for the class to be instantiated.

---

## Algorithmic Thinking

Algorithms are a big part of data science and are, in essence, a procedure or formula used to solve a problem. 

Besides objects, a common way to group data is via an array. An array is simply a list of elements, where each element contains its own data and has a specific index (i.e. position) in the array. Because of their widespread use, there are a multitude of algorithms that can sort arrays and search for elements in them.

Each algorithm is measured and compared with one another primarily based on its average time complexity and space complexity. Both of these are indicated using Big-O notation, which outlines the mathematical trend of each complexity as the number of items in the array increases. Attached below is a graph containing illustrations of common complexities with their respective Big-O notations indicated, where ``n`` represents the input size of the array...

![Big O Notation Graph](https://miro.medium.com/max/1400/1*FkQzWqqIMlAHZ_xNrEPKeA.png)
> Credit: https://miro.medium.com/max/1400/1*FkQzWqqIMlAHZ_xNrEPKeA.png

The time complexity is what the trend for how long a specific algorithm will take looks like on average for sorting/searching an array with ``n`` amount of items. For instance, if an algorithm has a linear time complexity (denoted as ``O(n)``) that means that the amount of time the algorithm takes will increase linearly as ``n`` increases (shown in blue on the above graph). On the other hand, if an algorithm has a logarithmic time complexity (``O(log(n))``), the amount of time the algorithm takes will increase but at a continuously slower rate as ``n`` increases (shown in yellow).

Likewise, the space complexity outlines the trend for how much space in memory it will take a computer to run the algorithm on average as ``n`` increases and uses the same Big-O notation. Some common space complexities denoted by Big-O notation include constant space (``O(1)``), meaning as ``n`` increases the amount of space needed stays the same (shown in green), and quadratic space, meaning the space needed will increase exponentially as ``n`` increases (shown in red).

### Sorting Algorithms

As the name implies, sorting algorithms are used to sort elements in an array in accordance to specific criteria. The simplest example is sorting an array of numbers from least to greatest, and will be the sorting criteria used for all the following code examples...

#### Insertion Sort

| Average Time Complexity: O(n^2) | Average Space Complexity: O(1) |
| ------------------------------- | ------------------------------ |

*Iterative Code Implementation:*
```c++
void insertionSort(std::vector<int> &list)
{
    int n = list.size();

    for (int i = 0; i < n; i++)
    {
        for (int j = i; j > 0; j--)
        {
            if (list[j] < list[j - 1])
                std::swap(list[j], list[j - 1]);
        }
    }
}
```

*Implementation Walk-through:*

1. The size of the array is stored as ``n``, and the insertion sort algorithm repeats the below steps ``n`` iterations to ensure that the array is fully sorted.
2. Each iteration, the algorithm starts at a new index (starting at ``0`` and ending at ``n - 1``) and checks to see if the value at that index is greater than the value at the index before it; if it isn't, the algorithm swaps these two values. The algorithm then goes backwards to the beginning of the list while comparing each pair of elements along the way and swapping them if necessary.
3. After each iteration finishes, a sorted list of elements is created from index ``0`` to ``j``, inclusive, and an unsorted list of elements remains from ``j`` to ``n - 1``, inclusive.
4. Once all iterations are completed, the array is fully sorted!

#### Bubble Sort

| Average Time Complexity: O(n^2) | Average Space Complexity: O(1) |
| ------------------------------- | ------------------------------ |

*Recursive Code Implementation:*
```c++
void bubbleSort(int arr[], int n)
{
    if (n == 1)
        return;

    for (int i = 0; i < n-1; i++)
        if (arr[i] > arr[i + 1])
            std::swap(arr[i], arr[i + 1]);
 
    bubbleSort(arr, n-1);
}
```

*Implementation Walk-through:*

1. The bubble sort function is initially called with the full array to be sorted along with its full size as parameters. The algorithm then moves through the entire array while checking each pair of elements and swapping them if the element with index ``i + 1`` is less than the element with index ``i``. This effectively brings the largest item of the array to the end.
2. The recursive function is called again, this time with the last item removed from the list (as it has already been sorted) and the size reduced by 1. The algorithm then brings the next largest item to the end of the list, and the cycle continues to repeat itself.
3. Steps 1 and 2 are repeated ``n`` times and the recursive function eventually stops once ``n = 1``, signifying that the whole array has been sorted!

> To learn more about recursive functions, please see: [Recursion](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#recursion)

#### Comparison to Other Sorting Algorithms

| Algorithm      | Average Time Complexity | Average Space Complexity |
| -------------- | ----------------------- | ------------------------ |
| Insertion Sort | O(n^2)                  | O(1)                     |
| Bubble Sort    | O(n^2)                  | O(1)                     |
| Selection Sort | O(n^2)                  | O(1)                     |
| Quick Sort     | O(n * log(n))           | O(log(n))                |
| Merge Sort     | O(n * log(n))           | O(n)                     |
| Heap Sort      | O(n * log(n))           | O(1)                     |
| Shell Sort     | O((n * log(n))^2)       | O(1)                     |

Looking in terms of just complexities, it seems that quick, merge, and heap sort are the fastest compared to the rest. However, after running my own experiments and doing research, I have come to know that quick sort is fastest for smaller or medium-sized arrays, merge sort is fastest for larger arrays and linked lists, and heap sort is the slowest overall due to the amount of extra computations it needs to do even with the same time complexity as the others. Despite that, when focusing on space complexity, heap sort shines the most due to it being an in-place sorting algorithm requiring a constant amount of space (if done iteratively) and being more time efficient compared to bubble, insertion, and shell sort.

### Searching Algorithms

Searching algorithms have a variety of use cases, not only for arrays but other data structures as well such as linked lists and dynamic vectors. However, one of the most common uses of searching algorithms is to find a specific value in a numeric array, which will be the purpose of the following code examples...

#### Linear Search

| Average Time Complexity: O(n) | Average Space Complexity: O(1) |
| ----------------------------- | ------------------------------ |

*Iterative Code Implementation:*
```c++
int linearSearch(std::vector<int> &list, int target)
{
    int n = list.size();

    for (int i = 0; i < n; i++)
    {
        if (list[i] == target)
            return i;
    }

    return -1;
}
```

*Implementation Walk-through:*

1. The linear search function is called with the array and target value as parameters. The size of array is stored as ``n``.
2. The algorithm iteratively traverses through the array starting at index ``0`` and making its way to index ``n - 1``. For each item it sees, it checks whether it is equal to the target value. If so, then the function immediately breaks the loop and returns the index of the first occurrence of the target value in the array.
3. If the algorithm reaches the end of the array without breaking the loop, it means the target value was not found, and as such, it returns `-1`.

#### Binary Search

| Average Time Complexity: O(log(n)) | Average Space Complexity: O(1) |
| ---------------------------------- | ------------------------------ |

*Recursive Code Implementation:*
```c++
inline int binarySearch(std::vector<int> &arr, int t, int l, int r)
{
    if (r >= l)
    {
        int mid = l + (r - l) / 2;
        if (arr[mid] == t)
            return mid;

        if (arr[mid] > t)
            return binarySearch(arr, t, l, mid - 1);

        return binarySearch(arr, t, mid + 1, r);
    }

    return -1;
}
```

*Implementation Walk-through:*

1. When the binary search function is initially called, the full array and the target value `t` are passed in as parameters. The `l` and `r` variables signify the left and right ends, inclusive, of the range the algorithm should search in; on the initial call, they are `0` and `n - 1` respectively
2. For each call, the index of the midpoint of the array is found. Three possible things can happen next: 
   1. If the midpoint is the target value, its index is returned throughout all the recursive calls and the algorithm is finished. Otherwise the next comparison is made.
   2. If the midpoint is greater than the target value, a new recursive call is made with the array and target value passed in again, but this time the right end of the array is set just before the midpoint and the left end of the array stays the same, effectively narrowing the search range by half. Otherwise the next comparison happens.
   3. If the midpoint is less than the target value, a new recursive call is made with the array and target value passed in again, but this time the left end of the array is set just after the midpoint and the right end of the array stays the same, effectively narrowing the search range by half.
3. Step 2 will continue to repeat until the target value is found as a midpoint and returned, or until the last function call is made with no searching range left (i.e. the right end is less than the left end). If the latter is true, then `-1` will be returned, signifying that the target value could not be found.

> To learn more about recursive functions, please see: [Recursion](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#recursion)

#### Comparison to Other Searching Algorithms

| Algorithm          | Average Time Complexity | Average Space Complexity |
| ------------------ | ----------------------- | ------------------------ |
| Linear Search      | O(n)                    | O(1)                     |
| Binary Search      | O(log(n))               | O(1)                     |
| Jump Search        | O(√n)                   | O(1)                     |
| Exponential Search | O(log(n))               | O(1)                     |
| Sequential Search  | O(n)                    | O(1)                     |

Looking at the chart, it can be seen that in terms of time efficiency binary and exponential search stand out the most with their `O(log(n))` time complexities, with jump search following suit with its `O(√n)` time complexity. The key difference between binary and exponential search, however, is that exponential search is explicitly designed for unbounded lists whereas binary search is for bounded arrays. As for space complexities, all these algorithms are the same for the most part as they all take constant space to run. Lastly, linear search stands out because it does not require the array to be sorted; this could save computational time and resources from being used to first sort the array in order to search in it.

### Recursion

Recursion in a broad sense means defining a problem in terms of itself and is a really powerful tool for writing algorithms, as demonstrated above. 

A recursive function is a function that calls itself within its own body, and continues to do so until a stopping condition is reached in the last call. A recursive function can be used as a recursive loop, which is in direct contrast to an iterative loop made using `while` and/or `for` loops. To illustrate the difference, the following function prints the numbers 1 through 5 iteratively and the function after that does the same but recursively.

```c++
void printNumbersIteratively() {
    for (int i = 1; i <= 5; i++) 
        std::cout << i << std::endl;
}

void printNumbersRecursively(i) {
    std::cout << i << std::endl;
    
    if (i < 5)
        printNumbersRecursively(i + 1);
}
```

#### Recursive Algorithms

Below is a simple but efficient recursive algorithm with memoization, used to calculate any number in the Lucas sequence in reverse using Dart:

```dart
int reverseLucasSequence(int n, var memoizationTable) {
  if (n == 0) return 2;
  else if (n == 1) return 3;

  if (memoizationTable[n] == null)
    memoizationTable[n] =
        reverseLucasSequence(n - 2, memoizationTable) - reverseLucasSequence(n - 1, memoizationTable);
  return memoizationTable[n];
}
```
Having a memoization table saves computational time and resources, as it prevents tree-recursive functions, such as the above, from having to recalculate the same values over multiple function calls.

To see an example of a recursive searching algorithm, please see: [Binary Search](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#binary-search).

To see an example of a recursive sorting algorithm, please see: [Bubble Sort](https://github.com/Nitroblast009/ICS4U-Culminating-Portfolio#bubble-sort).

#### Recursion Types and Pitfalls

Recursion can be generally classified as either direct or indirect recursion. Direct recursion means that only one function is calling itself in its own body, whereas indirect recursion means you have multiple functions calling each other in a cycle.

The three major types of direct recursion are tail recursion (time complexity `O(n)`, space complexity `O(1)`), where the recursive call is made at the very end of the function body; head recursion (time complexity `O(n)`, space complexity `O(n)`), where the recursive call is made at the very beginning of the function body; and tree recursion (time complexity `O(2^n)`, space complexity `O(n)`), where the function call is made multiple times throughout the body. A very common pitfall faced when using direct recursion is stack overflowing, which is when the computer does not have any more memory to use for new function calls. This however can be avoided by using tail recursion, as the function is only called again once the main body has been executed--this is why it has a space complexity of `O(1)`.

Another huge pitfall many new programmers face when it comes to using recursion is being able to write a recursive function with concise stopping logic that works properly the first time it is called, as well as the *n*th time. Given how the code's logic and flow is not spelt out like with an iterative approach, it is hard to internalize the logic behind a recursive procedure. As such, I believe it is important to first solidify your program's logic using a flow chart before you start to code a recursive algorithm or function.

---

## File Handling

File handling is essential when it comes to storing and manipulating data that exists beyond just a runtime environment. There is a myriad of ways data can be stored including text, binary, CSV, JSON, and SQL Database files. Some file types are more useful for inputting data into programs (i.e. reading from files), while others are better with outputting data from programs (i.e. writing to files).

Whether you read or write to a file, it is always important to close it at the end of your program to avoid corrupting data. This is accomplished in C++ with the built-in `.close()` method on both `ifstream` objects (for input files) and `ofstream` objects (for output files).

### File Reading

Below is a JSON file I used to store my data in an organized schema to be inputted as objects in my Data Structures assignment:

```json
{
 {
        "utility": "Pen",
        "length": 10,
        "ink": {
            "erasable": false,
            "lossiness": 5,
            "inkColours": [
                {
                    "red": 214,
                    "green": 38,
                    "blue": 141,
                    "opacity": 84
                }
            ]
        },
        "engraving": "~~+-+~~"
    },
    {
        "utility": "Lead Pencil",
        "length": 15,
        "colours": {
            "bodyColour": {
                "red": 25,
                "green": 72,
                "blue": 244,
                "opacity": 101
            },
            "eraserColour": {
                "red": 234,
                "green": 211,
                "blue": 23,
                "opacity": 49
            }
        },
        "leadSize": 0.7
    },
}
```

To read it in my program, I created an `ifstream` object and used it to open this JSON file with a relative path, which comes courtesy of the C++ standard library for reading/writing to files, `<fstream>`. Next, instead of reinventing the wheel, I used the help of *Nlohmann's JSON for Modern C++ API* to convert the input JSON schema into an object format for convenient data access.

```c++
std::ifstream inputFile;
inputFile.open("./pencil_case.json");
nlohmann::json pencilCase = nlohmann::json::parse(inputFile);
```

### File Writing

For my Data Structures assignment, I just chose to write to an external text file. I first created an `ofstream` object with a relative path to write to it, and used the built-in insertion operator to send my data.

```c++
std::ofstream paper;
paper.open("./paper.txt");

inline void Pencil::scribble(std::ofstream &paper) override { 
    paper << "\n(Pencil length: " << this->length << ", Pencil body: " << this->bodyColour << ", Pencil eraser: " << this->eraserColour << ")\n" << std::endl; 
}
```
