# Memory Allocation System

## Overview

This project implements a memory allocation system using `sbrk` and `mmap` syscalls. It manages dynamic memory allocation through custom versions of `malloc`, `calloc`, `realloc`, and `free` functions. The system organizes memory blocks in a doubly linked list, coalesces adjacent free blocks, and splits large blocks when needed. It also handles large memory requests by utilizing `mmap`.

## Key Features

- **Custom malloc**: Allocates memory by either finding a best-fit block or extending the heap with `sbrk` or `mmap`.
- **Custom calloc**: Allocates and zeroes memory, finding a suitable block or creating a new one.
- **Custom realloc**: Resizes previously allocated memory, extending or reallocating as needed.
- **Custom free**: Marks blocks as free and merges adjacent free blocks.
- **Heap preallocation**: Preallocates a large chunk of memory with `sbrk` to optimize small memory allocations.

## Key Files

- `osmem.h`: Header file containing function declarations.
- `block_meta.h`: Defines the metadata structure for memory blocks.
  
## Main Functions

1. `os_malloc(size_t size)`: Allocates memory of the requested size, coalescing free blocks and splitting large ones if necessary.
2. `os_calloc(size_t nmemb, size_t size)`: Allocates and zeros memory for an array of `nmemb` elements, each of `size` bytes.
3. `os_realloc(void *ptr, size_t size)`: Resizes an existing memory block to the new size, either by expanding or moving the block.
4. `os_free(void *ptr)`: Frees a memory block and coalesces adjacent free blocks.
5. `heap_preallocation()`: Preallocates a large memory block using `sbrk` for efficient small memory allocations.
6. `memory_mapping(size_t size, int is_calloc)`: Allocates large blocks using `mmap` for memory sizes exceeding a threshold.

## Memory Management Strategies

- **Best-fit Allocation**: Searches for the smallest free block that can satisfy the allocation request.
- **Coalescing Free Blocks**: Adjacent free blocks are merged to prevent fragmentation.
- **Block Splitting**: Large blocks are split into smaller ones to minimize memory waste.

## License

This project is licensed under the BSD 3-Clause License.
