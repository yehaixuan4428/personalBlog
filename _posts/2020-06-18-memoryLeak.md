# Memory leak and valgrind detection
There are generally two types of definitions of *memory leak*:
- You have a pointer to some memory. After the resource is not needed, you forget to free it **before** the program terminate.
- You have an not-freed memory, and you don't have any pointer or reference to refer to this. (This is a stricter definition of memory leak, which is adopted by valgrind).

The difference between these two definitions is whether you **have access** to the memory if you want to free it

