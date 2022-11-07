# MemPools

  - **Goal**: Reduce memory fragmentation and provide detailed
    statistics

  - **Status**: Done.

  - **Version**: 2.0

<!-- end list -->

  - **More**:
    
      - [](http://www.squid-cache.org/Doc/code/namespaceMem.html)
    
      - [](http://www.squid-cache.org/Doc/code/group__MemPoolsAPI.html)

# Details

MemPools is a set of pooled memory allocators running on top of
malloc(). It's purpose is to reduce memory fragmentation and provide
detailed statistics on memory consumption.

Preferably all memory allocations in Squid should be done using MemPools
or one of the types built on top of it (i.e. cbdata).

MemPools are currently half-migrated towards proper C++, having been
converted from C functions to static members of a C++ class. This leaves
some issues open, such as initialization order.

Also, with the current advancements in malloc implementations one may
want to link Squid against an alternaive malloc implementation:

  - [Google
    tcmalloc](http://google-perftools.googlecode.com/svn/trunk/doc/tcmalloc.html)

  - [Wolfram Gloger's ptmalloc3](http://www.malloc.de/en/)

## Public API

See [](http://www.squid-cache.org/Doc/code/namespaceMem.html) and
[](http://www.squid-cache.org/Doc/code/group__MemPoolsAPI.html) for the
public API definitions.

### MEMPROXY\_CLASS Macro

This macro defines pooled *new* and *delete* operators for the class in
which it is used. It should be your first choice of how to integrate a
C++ class in Squid for dynamic allocation. Other API mechanisms are
possible, but are designed for special use cases.

For easy reading and code maintenance it should be placed at the top of
the class definition in the *private* area before any other API details
and followed by an empty line then the 'public:' section definition.

    class Foo
    {
        MEMPROXY_CLASS(Foo);
    
    public:
       ...
    };

Classes which use the CBDATA\_CLASS macro **must not** also use
MEMPROXY\_CLASS. That includes use in the direct line of inheritence
within a class hierarchy.

[CategoryFeature](https://wiki.squid-cache.org/action/show/Features/MemPools/CategoryFeature#)
