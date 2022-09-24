# mulle-dlmalloc

Doug Lea's malloc.c extended for shared memory use.

**mulle-dlmalloc** assumes you compile it with `-DMSPACE_ONLY`.

mulle-dlmalloc is used by the [mulle-mmapallocator](//github.com/mulle-core/mulle-mmapallocator) to manage shared memory and seperate memory arenas.


## Changes

The changes are fairly small.

The `create_mspace_with_base` and `create_mspace` have been modified, so
that the "locked" parameter is now called "mode" and can take on additional
values.

You OR the desired bits together to form the "mode":

| Bit | Description
|-----|------------------------------------------------------------|
| 1   | "locked" as before, the allocator is protected by locks    |
| 2   | "inflexible" the initially allocated memmory is never grown but stays stable |


So `create_mspace( 0x1000, 2 | 1)` will create "mspace" of size 4KB (of which
approximately 2K will be used for housekeeping.

