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

6. One simple solution to such problems is to use a standard-library unique_ptr (§13.2.1) rather     
than a ‘‘naked pointer’’ when deletion is required:
```c++
class Smiley : public Circle {
// ...
private:
vector<unique_ptr<Shape>> eyes; // usually two eyes
unique_ptr<Shape> mouth;
};
```
instead of    
```c++
class Smiley : public Circle {
// ...
private:
vector<Shape∗> eyes; // usually two eyes
Shape∗ mouth;
};
```
When to use shared_ptr https://zhuanlan.zhihu.com/p/56874877   

7. copy constructor 
https://www.geeksforgeeks.org/copy-constructor-in-cpp/   
```c++
Vector::Vector(const Vector &a)
        : elem(new double[a.sz]), sz(a.sz) {
    for (int i = 0; i < a.sz; i++) {
        elem[i] = a.elem[i];
    }
}
```
```c++
Vector &Vector::operator=(const Vector &a) // copy assignment
{
    double *p = new double[a.sz];
    for (int i = 0; i != a.sz; ++i)
        p[i] = a.elem[i];
    delete[] elem; // delete old elements
    elem = p;
    sz = a.sz;
    return *this;
}
```
8. move constructor
```c++
class Geometry {
public:
    Geometry(size_t size) : m_data(size) {}

    Geometry(const Geometry &other) : m_data(other.m_data) { std::cout << "Copy constructor" << std::endl; }

    Geometry(Geometry &&other) noexcept: m_data(std::move(other.m_data)) {
        std::cout << "Move constructor" << std::endl;
    }

private:
    std::vector<double> m_data;
};
```
```c++
int main() {
    Geometry geometry(1000000000);
    {
        ScopedTimer scopedTimer("copy constructor");
        {
            Geometry geometry2(geometry);
            scopedTimer.Report();
        }
        scopedTimer.Report();
    }
    {
        ScopedTimer scopedTimer("move constructor");
        {
            Geometry geometry2(std::move(geometry));
            scopedTimer.Report();
        }
        scopedTimer.Report();
    }
    return 0;
}
```
```c++
Copy constructor
copy constructor 28463
copy constructor 29487
Move constructor
move constructor 1
move constructor 511
```
