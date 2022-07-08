# A-Tour-of-C-2nd-Edition-C-In-Depth-Series-
1. C++ 20 support modules instead of include.The differences between headers and modules are not just syntactic.       
+ A module is compiled once only (rather than in each translation unit in which it is used).
+ Two modules can be impor ted in either order without changing their meaning.
+ If you import something into a module, users of your module do not implicitly gain access
to (and are not bothered by) what you imported: impor t is not transitive.
The effects on maintainability and compile-time performance can be spectacular.

2. Error-Handling Alternatives talk about how to deal with exceptions.  
3. Argument Passing(pass-by-reference) and Value Return(by reference if not local and use a move constructor if is a local variable )   
4. auto [n,v] = read_entry(is) The auto [n,v] declares two local variables n and v with their types deduced from
read_entr y()’s return type.
``` c++
struct Entry {
  string name;
  int value;
};
```
``` c++
map<string,int> m;
// ... fill m ...
for (const auto [key,value] : m)
cout << "{" << key "," << value << "}\n";
```
5. The constructor/destructor combination is the basis of many elegant techniques. In particular, it is the basis for most C++ general resource management techniques (§5.3, §13.2). The technique of acquiring resources in a
constructor and releasing them in a destructor, known as Resource Acquisition Is Initialization or
RAII, allows us to eliminate ‘‘naked new operations,’’ that is, to avoid allocations in general code
and keep them buried inside the implementation of well-behaved abstractions. Similarly, ‘‘naked
delete operations’’ should be avoided. Avoiding naked new and naked delete makes code far less
error-prone and far easier to keep free of resource leaks (§13.2).
