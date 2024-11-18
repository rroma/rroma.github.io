# Hash Indexes

The hash index is an index based on a data structure called a hash map. It utilizes a hash function to transform column values into hash keys (typically numbers). Based on the key, the item is placed into a specific bucket. Normally, values are distributed evenly across buckets. When new elements are added to the hash map, it needs to be rehashed, but only if the load factor exceeds a certain threshold. The load factor is usually defined as the ratio of the number of items in the hash map to the number of buckets.

## Pros
- Select, update, insert, delete complexity O(1)
- Perform well in case single row select, update, insert, delete with strict condition match: 
```sql
SELECT FROM books WHERE id = 100;
```
## Cons
- Relatively high RAM usage
- Performance degrade in case there are lots of duplicated values in indexed column. Duplicated values cause hash collisions
- Doesn't make sense to use with range conditions like:
```sql
SELECT FROM books WHERE year BETWEEN 1990 AND 2010;
```

## Hash vs btree 

In general, B-trees are a more universal type of index and have broader use cases. However, there are situations where a hash index may outperform a B-tree. Popular RDBMS systems may load an index fully into RAM or only the necessary parts of the index if that suffices. Unfortunately, to perform efficiently, hash indexes often need to be loaded entirely into RAM.

For values that are close to each other, hash keys are completely different, causing them to be stored in separate buckets. These buckets are typically located in different areas of persistent storage (HDD or SSD). If you need to access many elements (e.g., during a join operation) in a hash index stored on a hard drive, you will face random memory access, which is relatively slow on hard drives. To improve performance, you need to load the hash index into RAM, as RAM provides random access with nearly the same speed as sequential access. This is why hash indexes tend to consume a significant amount of memory.

Unlike hash indexes, B-trees are stored primarily in a sequential manner on hard drives, enabling faster reading. Considering the specific characteristics of hash indexes, their ideal usage scenario is for single-row operations based on exact matches.
