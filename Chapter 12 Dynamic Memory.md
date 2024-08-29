The programs we’ve written so far have used objects that have well-defined lifetimes. Global objects are allocated at program start-up and destroyed when the program ends. Local, automatic objects are created and destroyed when the block in which they are defined is entered and exited. Local static objects are allocated before their first use and are destroyed when the program ends.

In addition to supporting automatic and static objects, C++ lets us allocate objects dynamically. Dynamically allocated objects have a lifetime that is independent of where they are created; they exist until they are explicitly freed.

Properly freeing dynamic objects turns out to be a surprisingly rich source of bugs. To make using dynamic objects safer, the library defines two smart pointer types that manage dynamically allocated objects. Smart pointers ensure that the objects to which they point are automatically freed when it is appropriate to do so.

Our programs have used only static or stack memory. Static memory is used for local static objects (§ 6.1.1, p. 205), for class static data members (§ 7.6, p. 300), and for variables defined outside any function. Stack memory is used for nonstatic objects defined inside functions. Objects allocated in static or stack memory are automatically created and destroyed by the compiler. Stack objects exist only while the block in which they are defined is executing; static objects are allocated before they are used, and they are destroyed when the program ends.

In addition to static or stack memory, every program also has a pool of memory that it can use. This memory is referred to as the free store or heap. Programs use the heap for objects that they dynamically allocate—that is, for objects that the program allocates at runtime. The program controls the lifetime of dynamic objects; our code must explicitly destroy such objects when they are no longer needed.

Although necessary at times, dynamic memory is notoriously tricky to manage correctly.
## 12.1 Dynamic Memory and Smart Pointers

In C++, dynamic memory is managed through a pair of operators: new, which allocates and optionally initializes an object in dynamic memory and returns a pointer to that object; and delete, which takes a pointer to a dynamic object, destroys that object, and frees the associated memory.

Dynamic memory is problematic because it is surprisingly hard to ensure that we free memory at the right time. Either we forget to free the memory—in which case we have a memory leak—or we free the memory when there are still pointers referring to that memory—in which case we have a pointer that refers to memory that is no longer valid.

To make using dynamic memory easier (and safer), the new library provides two smart pointer types that manage dynamic objects. A smart pointer acts like a regular pointer with the important exception that it automatically deletes the object to which it points. The new library defines two kinds of smart pointers that differ in how they manage their underlying pointers: shared_ptr, which allows multiple pointers to refer to the same object, and unique_ptr, which "owns" the object to which it points. The library also defines a companion class named weak_ptr that is a weak reference to an object managed by a shared_ptr. All three are defined in the memory header.

### 12.1.1 The shared_ptr Class

Like vectors, smart pointers are templates (§ 3.3, p. 96). Therefore, when we create a smart pointer, we must supply additional information—in this case, the type to which the pointer can point. As with vector, we supply that type inside angle brackets that follow the name of the kind of smart pointer we are defining:

```cpp

 shared_ptr<string> p1; // shared_ptr that can point at a string
shared_ptr<list<int>> p2; // shared_ptr that can point at a list of ints
```

A default-initialized smart pointer holds a null pointer (§ 2.3.2, p. 53). In § 12.1.3 (p. 464), we’ll cover additional ways to initialize a smart pointer.

We use a smart pointer in ways that are similar to using a pointer. Dereferencing a smart pointer returns the object to which the pointer points. When we use a smart pointer in a condition, the effect is to test whether the pointer is null:

```cpp

// if p1 is not null, check whether it’s the empty string
if (p1 && p1->empty())
    *p1 = "hi"; // if so, dereference p1 to assign a new value to that string
```

Table 12.1 (overleaf) lists operations common to shared_ptr and unique_ptr. Those that are particular to shared_ptr are listed in Table 12.2 (p. 453).
#### The make_sharedFunction
### 12.1.2 Managing Memory Directly
### 12.1.3 Usingshared_ptrswithnew 
### 12.1.4 SmartPointersandExceptions 
### 12.1.5 unique_ptr 
### 12.1.6 weak_ptr 
## 12.2 Dynamic Arrays 
### 12.2.1 new and Arrays 
### 12.2.2 The allocator Class 
## 12.3 UsingtheLibrary:AText-QueryProgram
### 12.3.1 DesignoftheQueryProgram
### 12.3.2 DefiningtheQueryProgramClasses
## Chapter Summary