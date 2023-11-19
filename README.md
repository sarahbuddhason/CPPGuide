- [1. Memory Management](#1-memory-management)
  - [Memory Management Overview](#memory-management-overview)
  - [Dynamic Memory Allocation](#dynamic-memory-allocation)
  - [Memory Allocation for Arrays](#memory-allocation-for-arrays)
  - [Smart Pointers in C++11](#smart-pointers-in-c11)
  - [RAII (Resource Acquisition Is Initialization)](#raii-resource-acquisition-is-initialization)
  - [Common Pitfalls in Memory Management](#common-pitfalls-in-memory-management)
  - [Best Practices in Memory Management](#best-practices-in-memory-management)
- [2. Object-Oriented Programming (OOP)](#2-object-oriented-programming-oop)
  - [Fundamentals of OOP](#fundamentals-of-oop)
  - [Classes and Objects](#classes-and-objects)
  - [Access Specifiers](#access-specifiers)
  - [Constructors and Destructors](#constructors-and-destructors)
  - [Inheritance](#inheritance)
  - [Polymorphism](#polymorphism)
  - [Abstract Classes and Pure Virtual Functions](#abstract-classes-and-pure-virtual-functions)
  - [Function Overloading and Overriding](#function-overloading-and-overriding)
  - [Operator Overloading](#operator-overloading)
  - [Friend Functions and Classes](#friend-functions-and-classes)
  - [Copy Constructor](#copy-constructor)
  - [Rule of Three/Five](#rule-of-threefive)
- [3. Standard Template Library (STL)](#3-standard-template-library-stl)
  - [Introduction to Templates](#introduction-to-templates)
  - [Overview of STL Components](#overview-of-stl-components)
  - [Commonly Used STL Containers](#commonly-used-stl-containers)
  - [Important STL Algorithms](#important-stl-algorithms)
  - [STL Iterators](#stl-iterators)
  - [Memory Management in STL](#memory-management-in-stl)
  - [Best Practices with STL](#best-practices-with-stl)
- [4. Concurrency and Multithreading](#4-concurrency-and-multithreading)
  - [Processes and Threads](#processes-and-threads)
  - [C++11 Thread Library](#c11-thread-library)
  - [Thread Management](#thread-management)
  - [Synchronization Mechanisms](#synchronization-mechanisms)
  - [Thread-Local Storage](#thread-local-storage)
  - [Best Practices in Multithreading](#best-practices-in-multithreading)
- [5. Advanced Topics](#5-advanced-topics)
  - [Deadlocks](#deadlocks)
  - [RAII in C++](#raii-in-c)
  - [Best Practices with RAII](#best-practices-with-raii)
- [6. Container Details](#6-container-details)
  - [Detailed Overview of STL Containers](#detailed-overview-of-stl-containers)
  - [Key Differences Between Containers](#key-differences-between-containers)
- [7. Input/Output in C++](#7-inputoutput-in-c)
  - [Basic I/O](#basic-io)
  - [File I/O](#file-io)
  - [Error Handling in File I/O](#error-handling-in-file-io)
  - [Manipulators](#manipulators)
  - [String Streams](#string-streams)
- [Database Management](#database-management)
  - [Example: Using SQLite in C++](#example-using-sqlite-in-c)

---

```markdown
# C++ Programming Guide

## Part 1: Memory Management
### Memory Management Overview
- **Stack**: Automatic memory allocation/deallocation. Fast access. Limited size.
- **Heap**: Dynamic memory allocation/deallocation. Managed with `new` and `delete`.

### Dynamic Memory Allocation
#### Using `new` and `delete`
- **new**: Allocates memory on the heap.
  ```cpp
  int* ptr = new int;
  ```
- **delete**: Deallocates memory from the heap.
  ```cpp
  delete ptr;
  ```

### Memory Allocation for Arrays
#### Array-Specific Memory Management
- **new[]**: Allocates array on the heap.
  ```cpp
  int* arr = new int[10];
  ```
- **delete[]**: Deallocates array from the heap.
  ```cpp
  delete[] arr;
  ```

### Smart Pointers in C++11
#### Types and Usage
- **std::unique_ptr**: Owns and manages another object through a pointer and disposes of that object when the `unique_ptr` goes out of scope.
  ```cpp
  std::unique_ptr<int> ptr(new int);
  ```
- **std::shared_ptr**: Maintains reference counting to manage ownership. Object is destroyed when the last `shared_ptr` is destroyed.
  ```cpp
  std::shared_ptr<int> ptr(new int);
  ```
- **std::weak_ptr**: Holds a non-owning reference to an object managed by `shared_ptr`.
  ```cpp
  std::weak_ptr<int> weakPtr = sharedPtr;
  ```

### RAII (Resource Acquisition Is Initialization)
#### Principles and Best Practices
- Ensures resources are wrapped in objects, whose lifetimes are automatically managed.
- Resource is acquired in a constructor and released in the destructor.

### Common Pitfalls in Memory Management
#### Identifying and Avoiding Issues
- **Memory leaks**: Memory that is not deallocated.
- **Dangling pointers**: Pointers that refer to deallocated memory.
- **Double freeing**: Calling `delete` on a pointer that has already been deleted.
- **Improper pairing**: Using `delete[]` with `new` or `delete` with `new[]`.

### Best Practices in Memory Management
#### Guidelines for Effective Use
- Prefer smart pointers over raw pointers.
- Only use `new` if you need control over how and when memory is allocated.
- Always match `new` with `delete` and `new[]` with `delete[]`.
- Avoid using raw pointers for resource management if possible.

---

## Part 2: Object-Oriented Programming (OOP)
### Fundamentals of OOP
1. **Encapsulation**: Bundling data and methods into a class.
2. **Inheritance**: Creating new classes from existing ones.
3. **Polymorphism**: Different classes treated as instances of the same class.
4. **Abstraction**: Hiding complex details, showing only necessary features.

### Classes and Objects
#### Defining and Using Them
- **Class**: Blueprint for objects.
  ```cpp
  class MyClass {
  public:
    int myData;
    void myFunction();
  };
  ```
- **Object**: Instance of a class.
  ```cpp
  MyClass obj;
  ```

### Access Specifiers
#### Controlling Access to Class Members
- **public**: Accessible from outside the class.
- **private**: Accessible only within the class.
- **protected**: Accessible within the class and derived classes.

### Constructors and Destructors
#### Lifecycle Management
- **Constructor**: Called when a new instance is created.
  ```cpp
  MyClass() { /* constructor code */ }
  ```
- **Destructor**: Called when an instance is destroyed.
  ```cpp
  ~MyClass() { /* destructor code */ }
  ```

### Inheritance
#### Deriving New Classes
- Syntax for inheritance:
  ```cpp
  class Derived : public Base { /* ... */ };
  ```

### Polymorphism
#### Overriding Functions
- Achieved through function overriding.
- **Virtual Functions**: Allow derived classes to override a function.
  ```cpp
  class Base {
  public:
    virtual void myFunction();
  };
  ```

### Abstract Classes and Pure Virtual Functions
#### Creating Interfaces
- **Abstract Class**: Can't instantiate objects. Contains pure virtual functions.
  ```cpp
  class AbstractClass {
  public:
    virtual void PureVirtualFunction() = 0;
  };
  ```

### Function Overloading and Overriding
#### Differentiating Functions
- **Overloading**: Same name, different parameters.
- **Overriding**: Redefining a function in a derived class.

### Operator Overloading


#### Customizing Operator Behavior
- Special meanings to operators with class objects.
  ```cpp
  MyClass operator+(const MyClass&);
  ```

### Friend Functions and Classes
#### Accessing Private Members
- **Friend Function**: Access private and protected members.
  ```cpp
  friend void FriendFunction(MyClass&);
  ```

### Copy Constructor
#### Copying Objects
- Initializes an object with another object of the same class.
  ```cpp
  MyClass(const MyClass& obj);
  ```

### Rule of Three/Five
#### Managing Object Copies
- Custom destructor, copy constructor, copy assignment operator.
- Include move constructor and move assignment operator (C++11).

---

## Part 3: Standard Template Library (STL)
### Introduction to Templates
#### Creating Generic Functions and Classes
- **Function Templates**: Generic functions.
  ```cpp
  template <typename T>
  T myFunction(T x) {
    return x;
  }
  ```
- **Class Templates**: Generic classes.
  ```cpp
  template <typename T>
  class MyClass {
  public:
    T myMember;
  };
  ```

### Overview of STL Components
#### Containers, Algorithms, and Iterators
1. **Containers**: Store collections of data.
   - Sequential, Associative, Unordered Associative.
2. **Algorithms**: Sorting, searching, modifying.
   - Examples: `sort`, `find`, `max_element`.
3. **Iterators**: Access elements of containers.
   - Types: Input, Output, Forward, Bidirectional, Random Access.

### Commonly Used STL Containers
#### Types and Their Usage
- **std::vector**, **std::list**, **std::map**, **std::set**, **std::unordered_map**, **std::unordered_set**

### Important STL Algorithms
#### Common Operations
- **sort**, **find**, **for_each**

### STL Iterators
#### Accessing Container Elements
- **begin(), end()**: Iterators to start and end.

### Memory Management in STL
#### Automatic Handling by Containers
- Containers manage their memory automatically.

### Best Practices with STL
#### Effective Use of STL Features
- Prefer STL containers, use algorithms, choose appropriate containers.

---

## Part 4: Concurrency and Multithreading
### Processes and Threads
#### Basics of Parallel Execution
- **Process**: Independent execution, own memory space.
- **Thread**: Smallest unit of processing, shared memory space.

### C++11 Thread Library
#### Managing Threads
- **std::thread**: Represents a thread.
- **Joining and Detaching Threads**: Wait or run independently.
- **Thread ID**: Unique ID for each thread.

### Thread Management
#### Synchronization and Safety
- **std::mutex**, **std::lock_guard**, **std::unique_lock**

### Synchronization Mechanisms
#### Ensuring Safe Concurrency
- **std::condition_variable**, **std::atomic**

### Thread-Local Storage
#### Per-Thread Variables
- **thread_local**: Unique instance for each thread.

### Best Practices in Multithreading
#### Guidelines for Safe and Efficient Threading
- Avoid data races, prefer RAII wrappers, use `std::atomic`, design to avoid deadlocks.

---

## Part 5: Advanced Topics
### Deadlocks
#### Understanding and Avoiding Deadlocks
- Common conditions, strategies to avoid, deadlock detection and recovery.

### RAII in C++
#### Resource Management with Object Lifetimes
- Key principles, managing different resources, examples of usage.

### Best Practices with RAII
#### Effective Resource Management
- Prefer RAII, understand ownership, leverage standard library.

---

Sure, I will merge the additional text on String Streams and Error Handling in File I/O into the existing structure. The updated content will look like this:

---

## Part 6: Container Details
### Detailed Overview of STL Containers
#### Understanding Each Container Type
1. **Sequence Containers**: `std::vector`, `std::list`, `std::deque`
2. **Associative Containers**: `std::set`, `std::multiset`, `std::map`, `std::multimap`
3. **Unordered Associative Containers**: `std::unordered_set`, `std::unordered_multiset`, `std::unordered_map`, `std::unordered_multimap`
4. **Container Adapters**: `std::stack`, `std::queue`, `std::priority_queue`

### Key Differences Between Containers
#### Unique Characteristics and Performance
- Ordered vs Unordered, Unique vs Multiple Keys, Direct Access vs Sequential Access, Performance Characteristics, Stack and Queue Adapters.

---

## Part 7: Input/Output in C++
### Basic I/O
#### Standard Streams and Operations
- **std::cout**, **std::cin**, **std::cerr**, **std::clog**

### File I/O
#### Reading and Writing Files
- Opening files, reading/writing operations, error handling.

### Error Handling in File I/O
- Check if a file stream was successfully opened/processed:
  ```cpp
  std::ifstream file("nonexistent.txt");
  if (!file) {
      std::cerr << "File cannot be opened!" << std::endl;
  }
  ```

### Manipulators
#### Formatting I/O Operations
- **std::endl**, **std::flush**, **setw**, **setfill**, **setprecision**

### String Streams
#### String Manipulation Operations
- **String Stream (`std::stringstream`)**:
  - Used for string manipulation operations.
  ```cpp
  #include <sstream>
  std::stringstream ss;
  ss << 100 << ' ' << 200;
  int foo, bar;
  ss >> foo >> bar;
  ```

---

### Database Management
1. **Install and Include Database Library**: Depending on the database (e.g., MySQL, SQLite), install the appropriate library and include it in your C++ project.

2. **Establish Connection**: Create a connection to the database server.

3. **Execute SQL Commands**:
   - Create, Read, Update, Delete (CRUD) operations.
   - Use SQL queries to interact with the database.

4. **Handle Results**: Process the results returned by the database.

5. **Close Connection**: Always close the database connection when done.

### Example: Using SQLite in C++

#### Setup
- Install SQLite library and include it in your project.
  ```cpp
  #include <sqlite3.h>
  ```

#### Open a Database Connection
```cpp
sqlite3* db;
int res = sqlite3_open("example.db", &db);

if (res) {
    cerr << "Error opening database: " << sqlite3_errmsg(db) << endl;
    return 1;
}
```

#### Execute SQL Query
```cpp
const char* sql = "CREATE TABLE IF NOT EXISTS students(id INT, name TEXT);";
char* errMsg = nullptr;
res = sqlite3_exec(db, sql, nullptr, 0, &errMsg);

if (res != SQLITE_OK) {
    cerr << "SQL error: " << errMsg << endl;
    sqlite3_free(errMsg);
}
```

#### Inserting Data
```cpp
sql = "INSERT INTO students (id, name) VALUES (1, 'John Doe');";
res = sqlite3_exec(db, sql, nullptr, 0, &errMsg);
// Handle errors...
```

#### Querying Data
```cpp
sql = "SELECT * FROM students;";
auto callback = [](void* data, int argc, char** argv, char** colNames) {
    for (int i = 0; i < argc; i++) {
        cout << colNames[i] << ": " << (argv[i] ? argv[i] : "NULL") << endl;
    }
    return 0;
};
res = sqlite3_exec(db, sql, callback, nullptr, &errMsg);
// Handle errors...
```

#### Close Database Connection
```cpp
sqlite3_close(db);
```

### Best Practices
- Always check the return values of database functions for error handling.
- Use prepared statements and parameter binding for security (to prevent SQL injection).
- Close the database connection properly to release resources.
- Manage database resources (like connections) effectively to avoid leaks.
