# doc-cpp

# C++ Comprehensive Reference Card

## Table of Contents
- [Basic Syntax](#basic-syntax)
- [Data Types](#data-types)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Object-Oriented Programming](#object-oriented-programming)
- [Memory Management](#memory-management)
- [Standard Template Library (STL)](#standard-template-library-stl)
- [Modern C++ Features](#modern-c-features)
- [Templates](#templates)
- [Error Handling](#error-handling)
- [Concurrency](#concurrency)
- [Best Practices](#best-practices)

## Basic Syntax

### Program Structure
```cpp
#include <iostream>  // Header inclusion

// Main function: entry point of program
int main() {
    // Code statements
    std::cout << "Hello, World!" << std::endl;
    return 0;  // Return value to OS
}
```

### Comments
```cpp
// Single-line comment

/* Multi-line
   comment */
```

### Variables and Constants
```cpp
int x = 10;              // Variable declaration and initialization
const double PI = 3.14;  // Constant (immutable)
constexpr int SIZE = 100;  // Compile-time constant
auto value = 42;         // Type inference with auto
```

### Operators
```cpp
// Arithmetic: +, -, *, /, %
int sum = a + b;
int mod = a % b;

// Increment/Decrement
x++;  // Post-increment
++x;  // Pre-increment

// Relational: ==, !=, <, >, <=, >=
if (a == b) { /*...*/ }

// Logical: &&, ||, !
if (a > 0 && b > 0) { /*...*/ }

// Bitwise: &, |, ^, ~, <<, >>
int bits = (1 << 3);  // Bit shift
```

## Data Types

### Primitive Types
```cpp
bool flag = true;            // Boolean (true/false)
char c = 'A';                // Character
int i = 42;                  // Integer
float f = 3.14f;             // Single precision floating point
double d = 3.14159;          // Double precision floating point
long l = 1000000L;           // Long integer
long long ll = 1000000000LL; // Long long integer
unsigned int ui = 42u;       // Unsigned integer
```

### Fixed Width Integer Types
```cpp
#include <cstdint>
int8_t i8 = 127;             // 8-bit signed integer
uint16_t ui16 = 65535;       // 16-bit unsigned integer
int32_t i32 = 2147483647;    // 32-bit signed integer
uint64_t ui64 = 18446744073709551615ULL; // 64-bit unsigned integer
```

### Strings
```cpp
#include <string>
std::string str = "Hello";     // String object
str += " World";               // String concatenation
std::string_view sv = str;     // Non-owning view (C++17)
```

### Arrays
```cpp
int arr[5] = {1, 2, 3, 4, 5};    // Fixed-size array
int matrix[3][4];                // Multi-dimensional array
```

### Enumerations
```cpp
// Classic enum
enum Color { RED, GREEN, BLUE };
Color c = RED;

// Scoped enum (C++11)
enum class Fruit : unsigned int { APPLE, BANANA, ORANGE };
Fruit f = Fruit::APPLE;
```

## Control Flow

### Conditionals
```cpp
// If-else statement
if (x > 0) {
    // Code if true
} else if (x < 0) {
    // Code if first condition false but this one true
} else {
    // Code if all conditions false
}

// Switch statement
switch (value) {
    case 1:
        // Code for value 1
        break;
    case 2:
        // Code for value 2
        break;
    default:
        // Default code
        break;
}

// Ternary operator
int max = (a > b) ? a : b;
```

### Loops
```cpp
// For loop
for (int i = 0; i < 10; i++) {
    // Loop body
}

// Range-based for loop (C++11)
for (const auto& item : container) {
    // Process item
}

// While loop
while (condition) {
    // Loop body
}

// Do-while loop
do {
    // Loop body
} while (condition);
```

### Jump Statements
```cpp
break;      // Exit loop or switch
continue;   // Skip to next iteration
return x;   // Return from function
goto label; // Jump to label (use sparingly)
```

## Functions

### Basic Function
```cpp
// Function declaration
int add(int a, int b);

// Function definition
int add(int a, int b) {
    return a + b;
}
```

### Default Parameters
```cpp
void print(const std::string& message, bool newline = true) {
    std::cout << message;
    if (newline) std::cout << std::endl;
}
```

### Function Overloading
```cpp
int add(int a, int b);
double add(double a, double b);
```

### Inline Functions
```cpp
inline int max(int a, int b) {
    return (a > b) ? a : b;
}
```

### Lambda Expressions (C++11)
```cpp
// Basic lambda
auto sum = [](int a, int b) { return a + b; };
int result = sum(5, 3);

// Lambda with capture
int factor = 2;
auto multiplier = [factor](int x) { return x * factor; };

// Mutable lambda
auto counter = [count = 0]() mutable { return ++count; };
```

### Function Pointers
```cpp
int (*funcPtr)(int, int) = add;  // Function pointer
int result = funcPtr(5, 3);      // Call through pointer
```

### Function Objects (Functors)
```cpp
struct Adder {
    int operator()(int a, int b) const {
        return a + b;
    }
};
Adder add;
int sum = add(5, 3);  // Use like a function
```

## Object-Oriented Programming

### Classes
```cpp
class Person {
private:
    std::string name;
    int age;

public:
    // Constructor
    Person(const std::string& n, int a) : name(n), age(a) {}
    
    // Member function
    void display() const {
        std::cout << name << ", " << age << " years old" << std::endl;
    }
    
    // Accessor (getter)
    const std::string& getName() const { return name; }
    
    // Mutator (setter)
    void setAge(int a) { age = a; }
};
```

### Inheritance
```cpp
class Student : public Person {
private:
    std::string studentId;
    
public:
    // Constructor with base class initialization
    Student(const std::string& name, int age, const std::string& id)
        : Person(name, age), studentId(id) {}
        
    // Override base class method
    void display() const override {
        Person::display();  // Call base class method
        std::cout << "Student ID: " << studentId << std::endl;
    }
};
```

### Polymorphism
```cpp
class Shape {
public:
    virtual double area() const = 0;  // Pure virtual function
    virtual ~Shape() {}               // Virtual destructor
};

class Circle : public Shape {
private:
    double radius;
    
public:
    Circle(double r) : radius(r) {}
    
    double area() const override {
        return 3.14159 * radius * radius;
    }
};

// Usage
Shape* shape = new Circle(5.0);
double a = shape->area();  // Calls Circle::area()
delete shape;
```

### Access Modifiers
```cpp
class MyClass {
public:
    // Accessible from anywhere
    
protected:
    // Accessible from this class and derived classes
    
private:
    // Accessible only from this class
};
```

### Friend Functions and Classes
```cpp
class MyClass {
private:
    int data;
    
public:
    // Friend function declaration
    friend void access(const MyClass& obj);
    
    // Friend class declaration
    friend class Helper;
};
```

## Memory Management

### Dynamic Memory
```cpp
// Single object
int* ptr = new int(10);   // Allocate and initialize
delete ptr;               // Deallocate

// Array
int* arr = new int[100];  // Allocate array
delete[] arr;             // Deallocate array
```

### Smart Pointers (C++11)
```cpp
#include <memory>

// Unique ownership
std::unique_ptr<int> uptr = std::make_unique<int>(10);  // C++14
// uptr = uptr2;  // Error: can't copy

// Shared ownership
std::shared_ptr<int> sptr1 = std::make_shared<int>(42);
std::shared_ptr<int> sptr2 = sptr1;  // Reference count = 2

// Weak reference (doesn't affect reference count)
std::weak_ptr<int> wptr = sptr1;
if (auto locked = wptr.lock()) {
    // Use locked, which is a shared_ptr
}
```

### RAII (Resource Acquisition Is Initialization)
```cpp
class File {
private:
    FILE* handle;
    
public:
    File(const char* filename, const char* mode) {
        handle = fopen(filename, mode);
    }
    
    ~File() {
        if (handle) fclose(handle);
    }
    
    // Prevent copying
    File(const File&) = delete;
    File& operator=(const File&) = delete;
};
```

## Standard Template Library (STL)

### Containers

#### Sequence Containers
```cpp
#include <vector>
std::vector<int> vec = {1, 2, 3};
vec.push_back(4);
vec.pop_back();

#include <list>
std::list<int> lst = {1, 2, 3};
lst.push_front(0);

#include <deque>
std::deque<int> dq;
dq.push_front(1);
dq.push_back(2);

#include <array>
std::array<int, 3> arr = {1, 2, 3};
```

#### Associative Containers
```cpp
#include <set>
std::set<int> s = {3, 1, 4, 1, 5};  // Contains 1, 3, 4, 5

#include <map>
std::map<std::string, int> m;
m["one"] = 1;
m["two"] = 2;

#include <unordered_map>
std::unordered_map<std::string, int> hash;
hash["apple"] = 5;
```

### Iterators
```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};

// Basic iteration
for (auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";
}

// Range-based for (C++11)
for (const auto& val : vec) {
    std::cout << val << " ";
}

// Iterator types
auto it1 = vec.begin();      // Regular iterator
auto it2 = vec.cbegin();     // Const iterator
auto it3 = vec.rbegin();     // Reverse iterator
auto it4 = vec.crbegin();    // Const reverse iterator
```

### Algorithms
```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {5, 3, 1, 4, 2};

// Sorting
std::sort(v.begin(), v.end());  // 1, 2, 3, 4, 5

// Finding
auto it = std::find(v.begin(), v.end(), 3);

// Transforming
std::transform(v.begin(), v.end(), v.begin(),
    [](int x) { return x * 2; });  // Double each element

// Filtering with copy_if
std::vector<int> evens;
std::copy_if(v.begin(), v.end(), std::back_inserter(evens),
    [](int x) { return x % 2 == 0; });
```

### Utilities
```cpp
#include <tuple>
std::tuple<int, std::string, double> t(1, "hello", 3.14);
auto [id, name, value] = t;  // Structured binding (C++17)

#include <optional>  // C++17
std::optional<int> opt;
if (opt) {
    std::cout << *opt;
}
opt = 42;

#include <variant>  // C++17
std::variant<int, std::string> var = "hello";
std::visit([](auto&& arg) {
    using T = std::decay_t<decltype(arg)>;
    if constexpr (std::is_same_v<T, int>)
        std::cout << "int: " << arg;
    else if constexpr (std::is_same_v<T, std::string>)
        std::cout << "string: " << arg;
}, var);
```

## Modern C++ Features

### C++11 Features
```cpp
// Auto type deduction
auto x = 42;

// Range-based for loops
for (const auto& item : container) { /*...*/ }

// Move semantics
std::string str1 = "Hello";
std::string str2 = std::move(str1);  // str1 is now in a valid but unspecified state

// Uniform initialization
std::vector<int> v{1, 2, 3};
int x{42};

// nullptr
int* ptr = nullptr;

// Override and final
virtual void func() override;
virtual void func() final;

// Strongly-typed enums
enum class Color { Red, Green, Blue };

// Right angle brackets
std::vector<std::vector<int>> matrix;  // No space needed between >>
```

### C++14 Features
```cpp
// Generic lambdas
auto lambda = [](auto x, auto y) { return x + y; };

// Return type deduction for functions
auto multiply(int x, int y) { return x * y; }

// Variable templates
template<typename T>
constexpr T pi = T(3.1415926535897932385);
double circleArea = pi<double> * r * r;

// std::make_unique
auto ptr = std::make_unique<int>(42);
```

### C++17 Features
```cpp
// Structured bindings
auto [key, value] = *map.begin();

// if constexpr
template<typename T>
void process(T t) {
    if constexpr (std::is_integral_v<T>) {
        // Integer processing
    } else {
        // Non-integer processing
    }
}

// Inline variables
inline const int GLOBAL_CONST = 42;

// std::optional, std::variant, std::any
std::optional<int> maybeInt;
std::variant<int, std::string> var;
std::any value;
```

### C++20 Features
```cpp
// Concepts
template<typename T>
concept Numeric = std::is_arithmetic_v<T>;

template<Numeric T>
T add(T a, T b) { return a + b; }

// Ranges
#include <ranges>
for (int i : std::views::iota(1, 10) | std::views::filter([](int n) { return n % 2 == 0; })) {
    std::cout << i << ' ';
}

// Coroutines
#include <coroutine>
// (simplified example)
generator<int> range(int start, int end) {
    for (int i = start; i < end; i++) {
        co_yield i;
    }
}

// Three-way comparison (spaceship operator)
auto result = (a <=> b);
```

## Templates

### Function Templates
```cpp
template<typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

auto result = max<int>(5, 10);
auto result2 = max(5.5, 10.5);  // Type deduction
```

### Class Templates
```cpp
template<typename T, int Size = 10>
class Array {
private:
    T data[Size];
    
public:
    T& operator[](int index) {
        return data[index];
    }
    
    int size() const {
        return Size;
    }
};

Array<int, 5> intArray;
Array<double> doubleArray;  // Uses default Size = 10
```

### Template Specialization
```cpp
// Primary template
template<typename T>
struct Serializer {
    static void serialize(const T& obj) {
        // Default serialization
    }
};

// Specialization for std::string
template<>
struct Serializer<std::string> {
    static void serialize(const std::string& str) {
        // String-specific serialization
    }
};
```

### Variadic Templates
```cpp
// Recursion terminator
void print() {
    std::cout << std::endl;
}

// Variadic template function
template<typename T, typename... Args>
void print(T first, Args... args) {
    std::cout << first << " ";
    print(args...);
}

print("Hello", 42, 3.14, 'A');  // Prints: Hello 42 3.14 A
```

### SFINAE (Substitution Failure Is Not An Error)
```cpp
// Enable function only for arithmetic types
template<typename T>
typename std::enable_if<std::is_arithmetic<T>::value, T>::type
square(T value) {
    return value * value;
}

// C++17 if constexpr alternative
template<typename T>
auto square_modern(T value) {
    if constexpr (std::is_arithmetic_v<T>) {
        return value * value;
    } else {
        static_assert(always_false<T>::value, "Type not supported");
    }
}
```

## Error Handling

### Exceptions
```cpp
try {
    // Code that may throw exceptions
    if (value < 0) {
        throw std::invalid_argument("Value cannot be negative");
    }
} catch (const std::invalid_argument& e) {
    // Handle specific exception
    std::cerr << "Invalid argument: " << e.what() << std::endl;
} catch (const std::exception& e) {
    // Handle any standard exception
    std::cerr << "Exception: " << e.what() << std::endl;
} catch (...) {
    // Handle any other exception
    std::cerr << "Unknown exception occurred" << std::endl;
}
```

### Custom Exceptions
```cpp
class DatabaseError : public std::runtime_error {
public:
    DatabaseError(const std::string& message)
        : std::runtime_error(message) {}
};

void saveData() {
    throw DatabaseError("Connection failed");
}
```

### Function Try Blocks
```cpp
class Resource {
public:
    Resource(int id) try : id_(id) {
        // Constructor code
    } catch (...) {
        // Handle exceptions
        throw; // Re-throw
    }
    
private:
    int id_;
};
```

### noexcept Specifier
```cpp
void safeFunction() noexcept {
    // Function guaranteed not to throw
}

void conditionalNoexcept() noexcept(sizeof(int) > 4) {
    // Conditional noexcept
}
```

## Concurrency

### Threads
```cpp
#include <thread>

void task(int id) {
    std::cout << "Thread " << id << " running" << std::endl;
}

std::thread t1(task, 1);
t1.join();  // Wait for thread to finish

// Lambda with thread
std::thread t2([]() {
    std::cout << "Thread with lambda" << std::endl;
});
t2.detach();  // Detach thread (be careful!)
```

### Mutexes
```cpp
#include <mutex>

std::mutex mtx;

void safe_increment(int& counter) {
    std::lock_guard<std::mutex> lock(mtx);  // RAII lock
    counter++;
    // lock automatically released when out of scope
}

// Unique lock (more flexible)
std::unique_lock<std::mutex> ulock(mtx, std::defer_lock);
ulock.lock();
// ... operations ...
ulock.unlock();
```

### Condition Variables
```cpp
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

// Consumer thread
void consumer() {
    std::unique_lock<std::mutex> lock(mtx);
    cv.wait(lock, []{ return ready; });  // Wait until ready
    // Process data
}

// Producer thread
void producer() {
    {
        std::lock_guard<std::mutex> lock(mtx);
        // Prepare data
        ready = true;
    }
    cv.notify_one();  // Notify one waiting thread
}
```

### Futures and Promises
```cpp
#include <future>

// Future from async function
std::future<int> fut = std::async(std::launch::async, []() {
    // Do some computation
    return 42;
});

// Wait for result
int result = fut.get();

// Manual promise/future
std::promise<int> prom;
std::future<int> fut = prom.get_future();

// In another thread
prom.set_value(42);
```

### Atomic Operations
```cpp
#include <atomic>

std::atomic<int> counter(0);
counter++;  // Atomic increment
int value = counter.load();  // Atomic load

// Compare and exchange
int expected = 2;
bool success = counter.compare_exchange_strong(
    expected, 3);
```

## Best Practices

### Resource Management
- Use RAII for resource management (files, memory, locks)
- Prefer smart pointers over raw pointers
- Follow the Rule of Zero/Three/Five for classes
- Use std::unique_ptr for exclusive ownership
- Use std::shared_ptr for shared ownership
- Avoid std::auto_ptr (deprecated in C++11, removed in C++17)

### Code Organization
- Use namespaces to avoid name clashes
- Consider the pimpl idiom for ABI stability
- Keep header files self-contained
- Use forward declarations to minimize include dependencies
- Organize code into appropriate abstraction levels

### Modern C++ Style
- Prefer auto for complex types but use explicit types for primitives
- Use nullptr instead of NULL or 0 for pointers
- Use range-based for loops when possible
- Use constexpr for compile-time computation
- Use enum class over plain enums
- Use std::array instead of C-style arrays
- Use std::string and std::string_view instead of C-strings

### Performance
- Use move semantics to avoid unnecessary copying
- Pass large objects by const reference
- Return by value to enable Return Value Optimization (RVO)
- Use reserve() on containers when size is known
- Use emplace_back() instead of push_back() when possible
- Consider memory alignment for data structures
- Profile before optimizing

### Concurrency
- Prefer high-level concurrency tools (std::async, std::future)
- Be careful with shared mutable state
- Always use proper synchronization mechanisms
- Consider using thread-local storage where appropriate
- Be aware of false sharing for performance
- Design for concurrency from the start

### Error Handling
- Use exceptions for exceptional conditions
- Make functions exception-safe
- Use std::optional for functions that may not return a value
- Use error codes for expected failure modes
- Consider using std::expected (C++23) or Result pattern

### API Design
- Design interfaces that are hard to use incorrectly
- Use strong types to prevent logical errors
- Consider providing both wide and narrow contracts
- Document preconditions, postconditions, and invariants
- Use const correctness throughout your code

### Testing
- Write unit tests for your code
- Use static analyzers and sanitizers
- Enable compiler warnings and treat them as errors
- Consider property-based testing
- Add assertions for invariants and pre/post conditions
