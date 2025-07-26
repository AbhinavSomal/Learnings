Week 1 – Java Basics & Arrays: Theory Q&A
Difference between int[] arr = new int[5]; and int[] arr = {1,2,3,4,5};:
The first allocates an array of size 5 with default values (0 for ints), while the second initializes the array with specified contents. Use the first when the size is known but values will be set later; use the second for literal initialization.

Types of loops in Java:

for (init; cond; update)

while (cond)

do { } while (cond)
for is best when iteration count is known; while for unknown, and do-while for executions at least once.

Primitive vs non-primitive data types:
Primitive include int, boolean, char with default values (e.g. boolean default=false) 
baeldung.com
. Non-primitives include String, arrays, objects—they are references stored on heap.

Stack vs Heap memory for arrays:
Local variable references live in stack; actual arrays (via new) are stored on heap. Stack holds pointers; heap holds the data.

Pass‑by‑value in Java:
Java passes primitive values directly and object references by value (copy of reference). Modifying object fields inside methods affects the original object. Java does not pass by reference.

Time complexity: linear vs binary search:
Linear search scans each element (O(n)); binary search divides sorted array by half per step (O(log n)).

Array edge cases to handle:

Null references

Empty arrays (length == 0)

Index out of bounds

Negative indices or oversized values

Array rotation vs reversal:
Rotation shifts elements circularly (e.g., left-shift), whereas reversal flips the sequence end-to-end.

break vs continue vs return:

break exits a loop

continue skips to next iteration

return exits the current method immediately

Why sorting before two-pointers?
Two-pointer logic often relies on ascending order to increment or decrement pointers toward the target.

📘 Week 2 – Strings, Recursion, Backtracking: Theory Q&A
Immutable vs Mutable objects in Java:
String is immutable—modifications create new objects. StringBuilder is mutable—efficient in-place operations. Thread-safe StringBuffer is slower than StringBuilder.

Performance & thread safety:
String is immutable and inherently thread-safe; StringBuilder is mutable and fast but not thread-safe; StringBuffer is thread-safe but slower due to synchronization.

Character encoding & Unicode:
Java uses UTF-16 internally for char and String types, allowing global character representation beyond ASCII.

Why StringBuilder over String concat in loops:
Using String + inside loops leads to O(n²) time and many intermediate objects. StringBuilder appends in-place efficiently (O(n)).

Why + operator in loops is inefficient:
String concatenation creates new objects each time. Using StringBuilder avoids this overhead.

Define recursion:
Recursion is when a method calls itself. Two essential parts:

Base case (when to stop)

Recursive case (calls itself moving closer to base case)

What causes StackOverflowError in recursion:
Occurs when recursion depth is too deep or infinite. Each call consumes stack space; overshooting limit causes overflow. Avoid by limiting depth, using iteration, memoization, or tail recursion optimization 

**Direct vs indirect recursion:**
Direct: A() calls itself.
Indirect: A() calls B(), which calls A(), and so on.

Backtracking vs brute force:
Backtracking explores possibilities and prunes invalid branches early; brute force tries all permutations regardless of validity. Efficient for problems like N‑Queens.

Time complexity for subsequence generation & N‑Queens:
Generating all subsequences: O(2ⁿ) time and O(n) auxiliary space due to recursion depth 

. N‑Queens also grows exponentially (approx O(n!) or high branching factor dependent).
