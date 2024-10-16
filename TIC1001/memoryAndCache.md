![alt text](image-2.png)
![alt text](image-1.png)

- volatile memory = RAM
- non-volatile memory = HDD,SSD
- dynamic RAM (RAM stick on motherboard)
- static RAM (in CPU, acts as cache , eg. L1,L2,L3 cache)
- when there's not enough RAM for an operation, the system uses part of the hard drive or SSD as virtual memory to extend the available memory

# Cache

- Principle of Locality

  - Temporal locality: If an item is referenced, likely to be referenced again
  - Spatial locality: If an item is referenced, likely to be referenced nearby items as well

- cache line : smallest unit of data that can be transferred between the cache and main memory (respect the Principle of Locality , often 32 to 128 bytes)

## Types of cache mapping

- Direct-Mapped: Simple, fast, but more prone to conflicts.
- Fully Associative: Flexible, fewer misses, but complex and costly.
- Set-Associative: Balanced approach, reducing conflicts while managing complexity.
