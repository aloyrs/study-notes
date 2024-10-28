why OS:

- abstraction
- resource allocation
- control

OS runs in kernel mode (means have complete access to all hardware resources)

3 Functionalities of OS:

- Process management : interleaved execution, concurrency
- Memory management :

  - The program thinks it owns contiguous memory.

  - Paging mechanism : Uses a Page Table to map logical pages to physical frames. Ensures that the program can function as if it has contiguous memory, even though the physical memory might be scattered.

  - Can use virtual memory on secondary storage

- File management:
  - can create symbolic links
