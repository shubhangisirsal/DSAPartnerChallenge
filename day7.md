# Day 7 — Arrays & ArrayList

> **DSA Partner Challenge** | Week 2: Arrays + Sorting

---

## 📌 Topic of the Day

**Arrays & ArrayList — the most important data structure. Period.**

Every other structure — stacks, queues, heaps, hash maps — is built on arrays underneath. Most LeetCode problems involve arrays. Get comfortable with them now.

---

## 🎥 Resources

| Language | Resource |
|----------|----------|
| ☕ Java | [Arrays & ArrayList Tutorial](https://youtu.be/n60Dn0UsbEk?si=8EXhPUaa6Gkj4-Pb) |
| 🐍 Python | CampusX — Python for AI playlist (Lists section) |
| ⚙️ C++ | Striver A2Z DSA Sheet — Arrays section |

---

## 🧠 What to Learn Today

### Arrays — Core Concepts

- **Fixed size** — length set at creation, cannot change (Java/C++)
- **Zero-indexed** — first element at index 0, last at index n-1
- **O(1) access** — `arr[i]` is instant regardless of array size
- **Contiguous memory** — elements sit next to each other

---

### Java — Arrays

```java
// Declare and initialise
int[] arr = {10, 25, 3, 47, 8};

// Access
arr[0]        // 10 — first
arr[arr.length - 1]  // 8 — last
arr.length    // 5

// Loop
for (int i = 0; i < arr.length; i++) System.out.print(arr[i]);
for (int x : arr) System.out.print(x);   // for-each

// Useful methods (import java.util.Arrays)
Arrays.sort(arr);              // sort ascending in-place
Arrays.toString(arr);          // "[10, 25, 3, 47, 8]"
Arrays.copyOf(arr, 3);         // [10, 25, 3]
Arrays.fill(arr, 0);           // [0, 0, 0, 0, 0]
```

**ArrayList — dynamic size:**
```java
import java.util.ArrayList;

ArrayList<Integer> list = new ArrayList<>();
list.add(10);           // add to end
list.get(0);            // access — 10
list.set(0, 55);        // update
list.remove(0);         // remove by index
list.size();            // length  ← NOT .length!
Collections.sort(list); // sort
```

| Feature | Array | ArrayList |
|---------|-------|-----------|
| Size | Fixed | Dynamic |
| Primitives | Yes | No (use Integer) |
| Length | `arr.length` | `list.size()` |
| Sort | `Arrays.sort()` | `Collections.sort()` |

---

### Python — Lists

```python
arr = [10, 25, 3, 47, 8]

arr[0]       # 10 — first
arr[-1]      # 8  — last (negative indexing!)
arr[1:4]     # [25, 3, 47] — slicing
len(arr)     # 5

arr.append(99)       # add to end
arr.insert(2, 100)   # insert at index 2
arr.pop()            # remove last
arr.pop(1)           # remove at index 1
arr.remove(25)       # remove first 25

arr.sort()             # ascending in-place
arr.sort(reverse=True) # descending
arr.reverse()          # reverse in-place
sorted(arr)            # new sorted list
sum(arr)               # sum
min(arr) / max(arr)    # min / max
arr[::-1]              # reversed copy
```

---

### C++ — Arrays and Vectors

```cpp
// Static array
int arr[] = {10, 25, 3, 47, 8};
int n = sizeof(arr) / sizeof(arr[0]);   // length

// Vector (prefer this)
#include <vector>
#include <algorithm>

vector<int> v = {10, 25, 3, 47, 8};
v.push_back(99);              // add to end
v.pop_back();                 // remove last
v.size();                     // length
sort(v.begin(), v.end());     // sort ascending
reverse(v.begin(), v.end());  // reverse
```

---

## 💻 Practice Questions

---

**Q1. Find the Smallest Number**
> Initialise `min = arr[0]`, loop from index 1, update if smaller.

**Q2. Find the Largest Number**
> Same as Q1 but track maximum.

**Q3. Second Smallest and Second Largest**
> Approach 1: sort → `arr[1]` is 2nd smallest, `arr[n-2]` is 2nd largest.
> Approach 2 (optimal): track first and second in a single pass.
> ⚠️ Edge case: handle duplicates using `set()` in Python or checking `x != min1` in Java.

**Q4. Reverse a Given Array**
> Two pointer: `left=0`, `right=n-1`, swap and move inward until they meet.
> Python shortcut: `arr[::-1]`

**Q5. Count Frequency of Each Element**
> Use `HashMap` (Java) / `Counter` or dict (Python) / `map` (C++).
> For each element, increment its count.

**Q6. Rearrange in Increasing-Decreasing Order**
> Sort the full array ascending, then reverse the second half.
> Result: `[1,2,3,4,5,6]` → `[1,2,3,6,5,4]`

**Q7. Sum of All Elements**
> Initialise `sum=0`, loop through and add each element.
> Python: `sum(arr)` — C++: `accumulate(v.begin(), v.end(), 0)`

**Q8. Average of All Elements**
> `average = (double) sum / length`
> ⚠️ Java: cast to double before dividing to avoid integer division!
> Java: `7/2 = 3` — Python: `7/2 = 3.5` (auto float in Python 3)

**Q9. Median of the Array**
> Sort first, then:
> - Odd length: `arr[n/2]`
> - Even length: `(arr[n/2-1] + arr[n/2]) / 2.0`

---

## ✅ Checklist Before You Sleep

- [ ] I understand fixed vs dynamic arrays across all 3 languages
- [ ] I know `arr.length` (Java), `len(arr)` (Python), `v.size()` (C++)
- [ ] I implemented smallest/largest in a single traversal
- [ ] I solved 2nd min/max and handled the duplicates edge case
- [ ] I implemented array reversal using two pointers
- [ ] I used HashMap/dict/map for frequency counting
- [ ] I know the median formula for odd and even length arrays
- [ ] Solved at least 7 of the 9 questions

---

## 💬 Community

Drop solutions or doubts in the community.

**Solved all 9? Drop a 🔥 in the community.**

---

*Next up → Day 8: Sorting Algorithms — Bubble Sort, Selection Sort, Insertion Sort*
