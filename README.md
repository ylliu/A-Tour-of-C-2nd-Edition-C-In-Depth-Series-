# A-Tour-of-C-2nd-Edition-C-In-Depth-Series-
1. C++ 20 support modules instead of include.The differences between headers and modules are not just syntactic.       
+ A module is compiled once only (rather than in each translation unit in which it is used).
+ Two modules can be impor ted in either order without changing their meaning.
+ If you import something into a module, users of your module do not implicitly gain access
to (and are not bothered by) what you imported: impor t is not transitive.
The effects on maintainability and compile-time performance can be spectacular.
