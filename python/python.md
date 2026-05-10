# Python Interview Revision Notes

Quick Python 3 notes for technical interviews, LeetCode-style problems, and basic
data science tasks. Prefer clarity first; micro-optimizations come after the
algorithm is correct.

## Table of Contents

- [Mental Model](#mental-model)
- [Syntax Basics](#syntax-basics)
- [Control Flow and Useful Built-ins](#control-flow-and-useful-built-ins)
- [Core Data Types](#core-data-types)
- [Strings](#strings)
- [Lists and Tuples](#lists-and-tuples)
- [Dictionaries and Sets](#dictionaries-and-sets)
- [Comprehensions](#comprehensions)
- [Functions](#functions)
- [Iteration and Generators](#iteration-and-generators)
- [Sorting](#sorting)
- [Useful Standard Library](#useful-standard-library)
- [Complexity Cheat Sheet](#complexity-cheat-sheet)
- [LeetCode Patterns](#leetcode-patterns)
- [Object-Oriented Python](#object-oriented-python)
- [Errors, Files, and Imports](#errors-files-and-imports)
- [Type Hints](#type-hints)
- [Basic Data Science](#basic-data-science)
- [Common Pitfalls](#common-pitfalls)

## Mental Model

- Everything in Python is an object, including integers, strings, functions,
  classes, and modules.
- Names are references to objects. Assignment binds a name to an object; it does
  not copy the object.
- Python is dynamically typed: a name can refer to objects of different types
  over time.
- Python is strongly typed: it will not silently combine unrelated types like
  `"1" + 2`.
- Mutability matters:
  - Immutable: `int`, `float`, `bool`, `str`, `tuple`, `frozenset`, `None`.
  - Mutable: `list`, `dict`, `set`, most class instances.
- Use `==` for value equality and `is` for object identity.
- Use `is None` and `is not None` for `None` checks.
- Python uses a mechanism called pass-by-object-reference. It does not strictly
  follow the traditional "pass-by-value" or "pass-by-reference" models.
- A variable is a reference to an object. When you pass a variable to a
  function, Python passes a reference to the underlying object, but passes that
  reference by value. The function gets a copy of the reference, not a copy of
  the object.
- Depending on the mutability of the object that the reference points to,
  in-function operations may or may not change the original object. If a list
  (mutable) is passed to a function, in-function operations can change the
  original list. If an integer (immutable) is passed, in-function operations
  will not change it.

```python
def add_item(xs):
    xs.append(10)      # mutates caller's list

def reassign(xs):
    xs = [10]          # local name now points elsewhere

nums = [1, 2]
add_item(nums)         # [1, 2, 10]
reassign(nums)         # still [1, 2, 10]
```

Mutate vs rebind in function calls:

```python
def sort_in_place(nums):
    nums.sort()            # mutates the same list object

def caller_sort(nums):
    sort_in_place(nums)
    return nums            # sorted, because list is mutable

def add_all(nums, total):
    for num in nums:
        total += num       # rebinds local int, does not mutate caller value

def caller_sum(nums):
    total = 0
    add_all(nums, total)
    return total           # still 0, int is immutable
```

Quick mutability table:

| Type  | Mutable? | Changes visible outside function? |
| ----- | -------- | --------------------------------- |
| list  | Yes      | Yes                               |
| dict  | Yes      | Yes                               |
| set   | Yes      | Yes                               |
| int   | No       | No                                |
| str   | No       | No                                |
| tuple | No       | No                                |

## Syntax Basics

### Truthiness

Falsy values:

```python
False
None
0
0.0
""
[]
{}
set()
tuple()
```

Use truthiness for emptiness checks:

```python
if nums:
    print("non-empty")

if not name:
    print("empty string or missing value")
```

### Operators

| Expression | Meaning |
| --- | --- |
| `a + b` | addition or concatenation |
| `a - b` | subtraction |
| `a * b` | multiplication or repetition |
| `a / b` | true division, returns `float` |
| `a // b` | floor division |
| `a % b` | remainder |
| `a ** b` | exponentiation |
| `-a` | negation |
| `a == b` | value equality |
| `a != b` | value inequality |
| `a < b <= c` | chained comparison |
| `x in items` | membership |
| `x not in items` | non-membership |

Boolean operators short-circuit:

```python
if i < len(nums) and nums[i] == target:
    ...
```

### Naming Conventions

- `snake_case` for variables, functions, and methods.
- `PascalCase` for classes.
- `_internal_name` means "internal use by convention".
- `__dunder__` names are special methods used by Python.
- `__private` triggers name mangling inside classes; it is not true privacy.

## Control Flow and Useful Built-ins

### `if`, `elif`, `else`

```python
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
else:
    grade = "C"
```

Python has a conditional expression:

```python
label = "even" if x % 2 == 0 else "odd"
```

### Loops

```python
for x in nums:
    print(x)

for i in range(len(nums)):
    print(i, nums[i])

i = 0
while i < len(nums):
    print(nums[i])
    i += 1
```

Prefer direct iteration or `enumerate` over indexing when possible:

```python
for i, value in enumerate(nums):
    print(i, value)
```

Loop helpers:

```python
break       # exit loop
continue    # skip to next iteration
pass        # placeholder that does nothing
```

### Built-ins Worth Remembering

```python
len(xs)
sum(xs)
min(xs)
max(xs)
abs(x)
round(x, 2)
pow(x, y)           # same as x ** y
divmod(17, 5)       # (3, 2)
ord("a")            # 97
chr(97)             # "a"
```

`range(start, stop, step)` excludes `stop`:

```python
list(range(2, 8, 2))    # [2, 4, 6]
```

### Pattern Matching

`match`/`case` is available in Python 3.10+ and is useful for clean branching
on shapes of data.

```text
match command:
    case "quit":
        done = True
    case ("move", x, y):
        position = (x, y)
    case _:
        raise ValueError("unknown command")
```

## Core Data Types

```python
x = 10                  # int
pi = 3.14               # float
ok = True               # bool
name = "Ada"            # str
missing = None          # NoneType

nums = [1, 2, 3]        # list: mutable sequence
point = (2, 3)          # tuple: immutable sequence
seen = {1, 2, 3}        # set: unique hashable values
ages = {"Ada": 36}      # dict: key-value map
```

Conversions:

```python
int("42")
float("3.14")
str(42)
list("abc")             # ["a", "b", "c"]
tuple([1, 2])           # (1, 2)
set([1, 1, 2])          # {1, 2}
```

## Strings

Strings are immutable sequences of Unicode characters.

```python
s = "Sudeepam Pandey"

s[0]                    # "S"
s[-1]                   # "y"
s[0:8]                  # "Sudeepam"
s[::-1]                 # reversed string

s.lower()
s.upper()
s.strip()
s.replace("Pandey", "P.")
s.startswith("Sud")
s.endswith("ey")
"deep" in s
```

Use `find` when absence is allowed; use `index` when absence should raise.

```python
s.find("x")             # -1
s.index("x")            # ValueError
```

Split and join:

```python
line = "1,2,3"
parts = line.split(",")             # ["1", "2", "3"]
nums = list(map(int, parts))        # [1, 2, 3]

words = ["hello", "world"]
" ".join(words)                     # "hello world"
```

Prefer f-strings for formatting:

```python
name = "Ada"
score = 95.1234
print(f"{name}: {score:.2f}")       # Ada: 95.12
```

Multi-line code, single-line string:

```python
message = (
    "This is written across multiple source lines "
    "but becomes one string."
)
```

## Lists and Tuples

Lists are mutable dynamic arrays.

```python
nums = [10, 20, 30, 40]

nums[0]                 # 10
nums[-1]                # 40
nums[1:3]               # [20, 30]
nums[:2]                # [10, 20]
nums[2:]                # [30, 40]
nums[::-1]              # [40, 30, 20, 10]
```

Common list methods:

```python
nums.append(50)         # add one item at end
nums.extend([60, 70])   # add many items at end
nums.pop()              # remove and return last item
nums.pop(0)             # remove first item, O(n)
nums.reverse()          # reverse in place
nums.sort()             # sort in place
```

Use `sorted(nums)` when you want a new sorted list.

```python
a = [3, 1, 2]
b = sorted(a)           # b = [1, 2, 3], a unchanged
a.sort()                # a = [1, 2, 3]
```

Tuples are immutable and useful for fixed records, coordinates, and hashable keys.

```python
point = (3, 4)
x, y = point

seen_edges = set()
seen_edges.add((u, v))
```

Nested lists use repeated indexing, not multi-dimensional comma indexing:

```python
grid = [
    [1, 2, 3],
    [4, 5, 6],
]

grid[1][2]              # 6
```

Be careful when initializing matrices:

```python
bad = [[0] * 3] * 3     # rows share the same inner list
good = [[0] * 3 for _ in range(3)]

bad[0][1] = 7
bad                         # [[0, 7, 0], [0, 7, 0], [0, 7, 0]]

good[0][1] = 7
good                        # [[0, 7, 0], [0, 0, 0], [0, 0, 0]]
```

`[[0] * m] * n` reuses the same row object `n` times.
`[[0] * m for _ in range(n)]` creates `n` independent rows.

## Dictionaries and Sets

Dictionaries preserve insertion order in modern Python and provide average O(1)
lookup, insertion, and deletion.

```python
counts = {"a": 2, "b": 1}

counts["a"]             # 2
counts.get("z", 0)      # 0
counts["c"] = 3
del counts["b"]
```

Keys must be hashable, so strings, numbers, tuples of immutable values, and
`frozenset` can be keys. Lists, dicts, and sets cannot be keys.

```python
locations = {
    (10, 20): "start",
    (30, 40): "finish",
}

locations[(10, 20)]     # "start"
```

Common dictionary views:

```python
scores = {"Ada": 95, "Bob": 82}

scores.keys()           # dict_keys(["Ada", "Bob"])
scores.values()         # dict_values([95, 82])
scores.items()          # dict_items([("Ada", 95), ("Bob", 82)])

for name in scores:     # iterates keys
    print(name)

for name, score in scores.items():
    print(name, score)
```

Useful dictionary methods:

```python
scores = {"Ada": 95, "Bob": 82}

scores.get("Amy", 0)            # 0, does not insert
scores.setdefault("Amy", 0)     # inserts "Amy": 0, returns 0
scores.update({"Bob": 90})      # overwrite/add many keys
scores.update(Cam=88)           # keyword form for string keys

scores.pop("Ada")               # 95, removes key
scores.pop("Zoe", None)         # None, default avoids KeyError
scores.popitem()                # removes and returns last inserted pair
scores.copy()                   # shallow copy
scores.clear()                  # remove all items
```

Build dictionaries from keys or pairs:

```python
dict.fromkeys(["a", "b"], 0)    # {"a": 0, "b": 0}
dict([("a", 1), ("b", 2)])      # {"a": 1, "b": 2}
```

Be careful with mutable defaults in `fromkeys`:

```python
bad = dict.fromkeys(["a", "b"], [])
bad["a"].append(1)
bad                         # {"a": [1], "b": [1]}

good = {key: [] for key in ["a", "b"]}
```

Merge dictionaries:

```python
base = {"host": "localhost", "port": 8000}
override = {"port": 9000, "debug": True}

base | override             # new dict, right side wins
base |= override            # update base in place
```

Set basics:

```python
seen = set()
seen.add(10)
10 in seen              # True
seen.remove(10)         # KeyError if missing
seen.discard(10)        # no error if missing
seen.pop()              # remove and return an arbitrary item
seen.clear()            # remove all items
```

Use `{}` for an empty dict, not an empty set:

```python
type({})                # dict
type(set())             # set
```

Set operations:

```python
a = {1, 2, 3}
b = {3, 4}

a | b                   # union: {1, 2, 3, 4}
a & b                   # intersection: {3}
a - b                   # difference: {1, 2}
a ^ b                   # symmetric difference: {1, 2, 4}
```

Method versions are often clearer in longer code:

```python
a.union(b)              # same as a | b
a.intersection(b)       # same as a & b
a.difference(b)         # same as a - b
a.symmetric_difference(b)

a.update(b)             # add all items from b
a.intersection_update(b)
a.difference_update(b)
a.symmetric_difference_update(b)
```

Subset and disjoint checks:

```python
small = {1, 2}
large = {1, 2, 3}
other = {9}

small.issubset(large)       # True
large.issuperset(small)     # True
small.isdisjoint(other)     # True

small <= large              # subset
small < large               # proper subset
large >= small              # superset
```

Sets are useful for uniqueness and fast membership tests:

```python
nums = [3, 1, 3, 2, 1]
unique = set(nums)          # {1, 2, 3}

if target in unique:
    print("seen")
```

Use `frozenset` when you need an immutable set, for example as a dictionary key
or as a value inside another set.

```python
edge = frozenset({"A", "B"})
weights = {edge: 5}
```

## Comprehensions

```python
nums = [1, 2, 3, 4]

squares = [x * x for x in nums]
evens = [x for x in nums if x % 2 == 0]
parity = ["even" if x % 2 == 0 else "odd" for x in nums]

square_by_num = {x: x * x for x in nums}
unique_remainders = {x % 3 for x in nums}
```

Use a generator expression for streaming values:

```python
total = sum(x * x for x in nums)
```

## Functions

```python
def add(a, b):
    return a + b

def greet(name="friend"):
    return f"Hello, {name}"
```

Arguments:

```python
def f(a, b, *args, debug=False, **kwargs):
    print(a, b)         # required positional
    print(args)         # extra positional as tuple
    print(debug)        # keyword-only after *args
    print(kwargs)       # extra keyword args as dict
```

Avoid mutable default arguments:

```python
def bad_append(x, items=[]):
    items.append(x)
    return items

def good_append(x, items=None):
    if items is None:
        items = []
    items.append(x)
    return items
```

### Lambda Functions

Use `lambda` for short one-expression callbacks.

```python
lambda arguments: expression
```

```python
pairs = [(1, "b"), (2, "a")]
sorted(pairs, key=lambda pair: pair[1])   # [(2, "a"), (1, "b")]
```

Prefer `def` when logic is more than one simple expression.

## Iteration and Generators

Common iteration tools:

```python
for i, value in enumerate(nums):
    ...

for a, b in zip(xs, ys):
    ...

for i in range(5):          # 0, 1, 2, 3, 4
    ...

for i in range(5, 0, -1):   # 5, 4, 3, 2, 1
    ...
```

Useful built-ins:

```python
any(x > 0 for x in nums)
all(x > 0 for x in nums)
sum(nums)
min(nums)
max(nums)
float("inf")                         # positive infinity
float("-inf")                        # negative infinity
```

Generators produce values lazily:

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for x in countdown(3):
    print(x)
```

Iterator protocol:

- An iterable has `__iter__`.
- An iterator has `__iter__` and `__next__`.
- `for` loops call `iter(obj)` and repeatedly call `next(...)` until
  `StopIteration`.

## Sorting

Signatures:
- `list.sort(*, key=None, reverse=False)` (in place)
- `sorted(iterable, key=None, reverse=False)` (returns a new list)

Complexity (Timsort):
- Time: `O(n log n)` average/worst, `O(n)` best on nearly sorted input
- Extra space: `sort()` uses less extra memory than `sorted()` because
  `sorted()` always creates a new list

```python
nums = [3, 1, 2]
sorted(nums)                        # new sorted list
nums.sort()                         # in-place sort

words = ["pear", "apple", "fig"]
sorted(words, key=len)              # ["fig", "pear", "apple"]
sorted(words, reverse=True)
```

`reverse` is `False` by default. `key` is a function that maps each element to
the value Python should compare while sorting.

For lists/tuples of comparable values, Python already sorts lexicographically
(first item, then second, and so on), so `key` is optional:

```python
intervals = [[1, 3], [15, 18], [2, 5], [2, 6], [8, 10]]
sorted(intervals)
# [[1, 3], [2, 5], [2, 6], [8, 10], [15, 18]]
```

`key` with a normal function (no lambda):

```python
def by_start_then_end(interval):
    return (interval[0], interval[1])

intervals = [[1, 3], [15, 18], [2, 5], [2, 6], [8, 10]]
sorted(intervals, key=by_start_then_end)
# [[1, 3], [2, 5], [2, 6], [8, 10], [15, 18]]
```

Example where `key` is necessary for two-parameter custom sorting:
first by start ascending, then by end descending.

```python
def by_start_then_end_desc(interval):
    return (interval[0], -interval[1])

intervals = [[1, 3], [15, 18], [2, 5], [2, 6], [8, 10]]
sorted(intervals, key=by_start_then_end_desc)
# [[1, 3], [2, 6], [2, 5], [8, 10], [15, 18]]
```

## Useful Standard Library

### `collections`

```python
from collections import Counter, defaultdict, deque

Counter("banana")                   # Counter({"a": 3, "n": 2, "b": 1})

graph = defaultdict(list)
graph[u].append(v)

q = deque([1, 2, 3])
q.append(4)
q.appendleft(0)
q.pop()
q.popleft()                         # O(1), good for BFS queues
```

### `heapq`

Python's heap is a min-heap.

```python
import heapq

heap = []
heapq.heappush(heap, 5)
heapq.heappush(heap, 2)
heapq.heappop(heap)                 # 2
```

Max-heap trick:

```python
heapq.heappush(heap, -value)
largest = -heapq.heappop(heap)
```

Top-k:

```python
heapq.nlargest(k, nums)
heapq.nsmallest(k, nums)
```

### `bisect`

Binary search in sorted lists.

```python
import bisect

arr = [1, 2, 2, 4]
bisect.bisect_left(arr, 2)           # 1
bisect.bisect_right(arr, 2)          # 3
bisect.insort(arr, 3)                # arr becomes [1, 2, 2, 3, 4]
```

### `functools`

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n < 2:
        return n
    return fib(n - 1) + fib(n - 2)
```

### `itertools`

```python
from itertools import combinations, permutations, product

list(combinations([1, 2, 3], 2))     # pairs, order does not matter
list(permutations([1, 2, 3], 2))     # arrangements, order matters
list(product([0, 1], repeat=3))      # Cartesian product
```

## Complexity Cheat Sheet

| Operation | Average Complexity |
| --- | --- |
| `list[i]` | O(1) |
| `list.append(x)` | O(1) amortized |
| `list.pop()` | O(1) |
| `list.pop(0)` | O(n) |
| `x in list` | O(n) |
| `dict[key]`, `key in dict` | O(1) average |
| `set.add(x)`, `x in set` | O(1) average |
| `deque.append`, `deque.popleft` | O(1) |
| `heapq.heappush`, `heappop` | O(log n) |
| `sorted(xs)` | O(n log n) |

## LeetCode Patterns

### Input Parsing

```python
nums = list(map(int, input().split()))
n = int(input())
matrix = [list(map(int, input().split())) for _ in range(n)]
```

On LeetCode, methods usually receive already-parsed arguments:

```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        ...
```

### Frequency Counting

```python
from collections import Counter

counts = Counter(nums)
most_common = counts.most_common(1)
```

Manual counting:

```python
counts = {}
for x in nums:
    counts[x] = counts.get(x, 0) + 1
```

### Hash Map Lookup

```python
def two_sum(nums, target):
    seen = {}
    for i, x in enumerate(nums):
        need = target - x
        if need in seen:
            return [seen[need], i]
        seen[x] = i
```

### Two Pointers

Works well on sorted arrays or when shrinking from both ends.

```python
def has_pair_sorted(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        total = nums[left] + nums[right]
        if total == target:
            return True
        if total < target:
            left += 1
        else:
            right -= 1
    return False
```

### Sliding Window

Use when you need the best/valid contiguous subarray or substring.

```python
def max_sum_k(nums, k):
    window = sum(nums[:k])
    best = window
    for right in range(k, len(nums)):
        window += nums[right] - nums[right - k]
        best = max(best, window)
    return best
```

Variable-size window:

```python
def min_len_at_least_target(nums, target):
    left = 0
    total = 0
    best = float("inf")

    for right, x in enumerate(nums):
        total += x
        while total >= target:
            best = min(best, right - left + 1)
            total -= nums[left]
            left += 1

    return 0 if best == float("inf") else best
```

### Prefix Sums

Use when many range-sum queries are needed.

```python
prefix = [0]
for x in nums:
    prefix.append(prefix[-1] + x)

sum_l_to_r = prefix[r + 1] - prefix[l]
```

Count subarrays with sum `k`:

```python
from collections import defaultdict

def subarray_sum(nums, k):
    count_by_prefix = defaultdict(int)
    count_by_prefix[0] = 1
    prefix = 0
    ans = 0

    for x in nums:
        prefix += x
        ans += count_by_prefix[prefix - k]
        count_by_prefix[prefix] += 1

    return ans
```

### Monotonic Stack

Useful for next greater/smaller element problems.

```python
def next_greater(nums):
    ans = [-1] * len(nums)
    stack = []                      # stores indices

    for i, x in enumerate(nums):
        while stack and nums[stack[-1]] < x:
            ans[stack.pop()] = x
        stack.append(i)

    return ans
```

### Intervals

```python
def merge_intervals(intervals):
    intervals.sort()
    merged = []

    for start, end in intervals:
        if not merged or start > merged[-1][1]:
            merged.append([start, end])
        else:
            merged[-1][1] = max(merged[-1][1], end)

    return merged
```

### BFS

```python
from collections import deque

def bfs(start, graph):
    q = deque([start])
    seen = {start}

    while q:
        node = q.popleft()
        for nei in graph[node]:
            if nei not in seen:
                seen.add(nei)
                q.append(nei)
```

Grid BFS:

```python
directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

for dr, dc in directions:
    nr, nc = r + dr, c + dc
    if 0 <= nr < rows and 0 <= nc < cols:
        ...
```

### DFS

```python
def dfs(node, graph, seen):
    if node in seen:
        return
    seen.add(node)
    for nei in graph[node]:
        dfs(nei, graph, seen)
```

Python recursion depth can be a problem on long chains. Consider iterative DFS or:

```python
import sys
sys.setrecursionlimit(10**6)
```

### Binary Search

Search exact value:

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

Search first true in a monotonic boolean space:

```python
def first_true(lo, hi, condition):
    while lo < hi:
        mid = (lo + hi) // 2
        if condition(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

### Heap

```python
import heapq

def k_largest(nums, k):
    heap = []
    for x in nums:
        heapq.heappush(heap, x)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap
```

### Union Find

```python
class DSU:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, a, b):
        ra, rb = self.find(a), self.find(b)
        if ra == rb:
            return False
        if self.rank[ra] < self.rank[rb]:
            ra, rb = rb, ra
        self.parent[rb] = ra
        if self.rank[ra] == self.rank[rb]:
            self.rank[ra] += 1
        return True
```

### Dynamic Programming

Top-down memoization:

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def dp(i, remaining):
    if remaining == 0:
        return True
    if i == len(nums) or remaining < 0:
        return False
    return dp(i + 1, remaining) or dp(i + 1, remaining - nums[i])
```

Bottom-up example:

```python
def climb_stairs(n):
    if n <= 2:
        return n
    prev2, prev1 = 1, 2
    for _ in range(3, n + 1):
        curr = prev1 + prev2
        prev2, prev1 = prev1, curr
    return prev1
```

### Backtracking

```python
def subsets(nums):
    ans = []
    path = []

    def backtrack(i):
        if i == len(nums):
            ans.append(path.copy())
            return

        backtrack(i + 1)

        path.append(nums[i])
        backtrack(i + 1)
        path.pop()

    backtrack(0)
    return ans
```

## Object-Oriented Python

Basic class:

```python
class Student:
    university = "JIIT"              # class attribute

    def __init__(self, name, gpa):
        self.name = name             # instance attribute
        self.gpa = gpa

    def is_eligible(self):
        return self.gpa >= 7.0
```

Use `dataclass` for simple data containers:

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int
```

Special methods:

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

    def __eq__(self, other):
        return isinstance(other, Vector) and (self.x, self.y) == (other.x, other.y)
```

Inheritance:

```python
class Animal:
    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        return "woof"
```

Prefer composition over inheritance unless an actual "is-a" relationship is useful.

## Errors, Files, and Imports

Catch specific exceptions:

```python
try:
    value = int(text)
except ValueError:
    value = 0
```

Use `finally` for cleanup that must always run:

```python
try:
    process()
finally:
    cleanup()
```

Use context managers for files:

```python
from pathlib import Path

path = Path("data.txt")
text = path.read_text()
path.write_text("hello\n")

with path.open("a") as f:
    f.write("more\n")
```

JSON:

```python
import json

data = json.loads('{"name": "Ada"}')
text = json.dumps(data)
```

Imports:

```python
import math
import numpy as np
from collections import Counter
```

Common script entry point:

```python
def main():
    ...

if __name__ == "__main__":
    main()
```

Command-line arguments:

```python
import sys

args = sys.argv[1:]
```

## Type Hints

Type hints improve readability and editor support; Python does not enforce them
at runtime by default.

```python
def two_sum(nums: list[int], target: int) -> list[int]:
    ...

def get_user(user_id: int) -> dict[str, str] | None:
    ...
```

Useful typing imports:

```python
from typing import Iterable, Iterator, Optional

def first_positive(nums: Iterable[int]) -> Optional[int]:
    for x in nums:
        if x > 0:
            return x
    return None
```

## Basic Data Science

### NumPy

NumPy arrays support vectorized operations. Prefer vectorization over Python loops
for numeric workloads.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([10, 20, 30])

a + b                   # array([11, 22, 33])
a * 2                   # array([2, 4, 6])
a.mean()
a.std()
```

Array creation and shape:

```python
np.zeros((2, 3))
np.ones((2, 3))
np.arange(0, 10, 2)
np.linspace(0, 1, 5)

x = np.array([[1, 2, 3], [4, 5, 6]])
x.shape                 # (2, 3)
x.reshape(3, 2)
```

Boolean masks:

```python
x = np.array([1, 5, 10, 15])
x[x > 5]                # array([10, 15])
```

### pandas

```python
import pandas as pd

df = pd.read_csv("data.csv")
df.head()
df.info()
df.describe()
```

Selecting data:

```python
df["age"]                       # one column
df[["name", "age"]]             # multiple columns
df.loc[0, "age"]                # label-based
df.iloc[0, 2]                   # position-based
df[df["age"] >= 18]             # filter rows
```

Missing values:

```python
df.isna().sum()
df = df.dropna()
df["age"] = df["age"].fillna(df["age"].median())
```

Group, sort, join:

```python
df.groupby("city")["salary"].mean()
df.sort_values("salary", ascending=False)

merged = left.merge(right, on="user_id", how="left")
```

Create or update columns:

```python
df["income_k"] = df["income"] / 1000
df["is_adult"] = df["age"] >= 18
```

### Basic ML Workflow

```python
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, mean_squared_error

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
)

model.fit(X_train, y_train)
pred = model.predict(X_test)
```

Classification metric:

```python
accuracy_score(y_test, pred)
```

Regression metric:

```python
mean_squared_error(y_test, pred)
```

## Common Pitfalls

### Aliasing vs Copying

```python
a = [1, 2]
b = a
b.append(3)
print(a)                 # [1, 2, 3]

c = a.copy()             # shallow copy
```

For nested objects:

```python
import copy

deep = copy.deepcopy(nested)
```

### Modifying a List While Iterating

Prefer building a new list:

```python
nums = [1, 2, 3, 4]
odds = [x for x in nums if x % 2 == 1]
```

### Integer Division

```python
5 / 2                    # 2.5
5 // 2                   # 2
-5 // 2                  # -3, floors toward negative infinity
```

### Floating Point

```python
0.1 + 0.2 == 0.3         # False
```

Use tolerance:

```python
import math

math.isclose(0.1 + 0.2, 0.3)
```

### Shadowing Built-ins

Avoid using names like `list`, `dict`, `set`, `str`, `sum`, `min`, and `max` for
variables.

```python
nums = [1, 2, 3]         # good
list = [1, 2, 3]         # bad
```

### Late Binding in Closures

```python
funcs = []
for i in range(3):
    funcs.append(lambda i=i: i)
```

### Interview Habits

- Clarify input size and edge cases before coding.
- State time and space complexity.
- Test empty input, one-element input, duplicates, negative numbers, and already
  sorted or reversed data when relevant.
- Prefer readable variable names unless the loop is very small.
- Use standard library tools like `Counter`, `defaultdict`, `deque`, `heapq`, and
  `bisect` confidently.
