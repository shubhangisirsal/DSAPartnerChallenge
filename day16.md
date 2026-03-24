# Day 16 — Recursion

> **DSA Partner Challenge** | Week 3: Strings + Recursion

---

## 📌 Topic of the Day

**Recursion — a function calling itself. Base case stops it. Recursive case shrinks it.**

---

## 🎥 Resource

[Recursion Tutorial](https://youtu.be/M2uO2nMT0Bk?si=gwzV6CeWsbFpCIjC)

---

## 🧠 What is Recursion?

A function that calls **itself** with a smaller version of the same problem, until it reaches a **base case** that stops it.

```
Every recursive function has TWO parts:
  1. Base case   → stopping condition — MUST exist or infinite recursion
  2. Recursive case → call self with SMALLER input
```

### The Template

```java
returnType solve(input) {
    if (base case) return base_value;        // STOP
    return currentStep + solve(smallerInput); // SHRINK + RECURSE
}
```

---

### Call Stack — `sum(5)`

| Call | Expression | Result |
|------|-----------|--------|
| sum(5) | 5 + sum(4) | 5 + 10 = **15** |
| sum(4) | 4 + sum(3) | 4 + 6  = **10** |
| sum(3) | 3 + sum(2) | 3 + 3  = **6** |
| sum(2) | 2 + sum(1) | 2 + 1  = **3** |
| sum(1) | 1 [BASE]   | **1** |

---

### Classic Examples

**Factorial:**
```java
int factorial(int n) {
    if (n == 0) return 1;           // base case
    return n * factorial(n - 1);    // recursive case
}
```

**Fibonacci:**
```java
int fib(int n) {
    if (n <= 1) return n;           // base cases: fib(0)=0, fib(1)=1
    return fib(n-1) + fib(n-2);
}
```
> ⚠️ Naive `fib` is O(2^n) — exponentially slow. Fix with memoisation later.

---

### Key Insight: Print Before vs After Recursive Call

```java
// Print AFTER recursive call → 1 to N (forward)
void print1ToN(int n) {
    if (n==0) return;
    print1ToN(n-1);        // recurse first
    print(n);              // then print (unwinds bottom-up)
}

// Print BEFORE recursive call → N to 1 (backward)
void printNTo1(int n) {
    if (n==0) return;
    print(n);              // print first
    printNTo1(n-1);        // then recurse
}
```

---

## 💻 Practice Problems — 9 Problems

---

### STRING PROBLEMS

**Q1. Split Two Strings to Make Palindrome** — [LC #1616](https://leetcode.com/problems/split-two-strings-to-make-palindrome/) `Medium`
> Split a into prefix + suffix from b (or vice versa) to form a palindrome.
> Two-pointer from both ends matching a[lo] with b[hi]. Middle remaining part must be palindrome itself.
```python
def check(a, b):
    lo, hi = 0, len(b)-1
    while lo<hi and a[lo]==b[hi]: lo+=1; hi-=1
    return a[lo:hi+1]==a[lo:hi+1][::-1] or b[lo:hi+1]==b[lo:hi+1][::-1]
return check(a,b) or check(b,a)
```

---

**Q2. Number of Ways to Split a String** — [LC #1573](https://leetcode.com/problems/number-of-ways-to-split-a-string/) `Medium`
> Split binary string into 3 parts with equal number of 1s.
> Count total 1s. If not divisible by 3 → 0. If 0 ones → C(n-1, 2) = (n-1)(n-2)/2. Otherwise find gaps between split positions.
```python
def numWays(self, s):
    MOD, n = 10**9+7, len(s)
    ones = s.count('1')
    if ones % 3: return 0
    if ones == 0: return (n-1)*(n-2)//2 % MOD
    # count gaps around the each/each*2 boundaries
    each, cnt, gaps = ones//3, 0, []
    for c in s:
        if c=='1': cnt+=1
        if cnt in (each, each*2) and c=='1': gaps.append(0)
        elif gaps and cnt in (each, each*2): gaps[-1]+=1
    return (gaps[0]+1)*(gaps[1]+1) % MOD if len(gaps)==2 else 0
```

---

**Q3. First Uppercase Letter in a String** — GFG `Easy`
> Return the first uppercase letter. '$' if none.
```java
// Recursive approach
char firstUpper(String s, int i) {
    if (i==s.length()) return '$';
    if (Character.isUpperCase(s.charAt(i))) return s.charAt(i);
    return firstUpper(s, i+1);
}
```
```python
def first_upper(s, i=0):
    if i==len(s): return '$'
    if s[i].isupper(): return s[i]
    return first_upper(s, i+1)
```

---

### RECURSION PROBLEMS

**Q4. Sum Triangle from Array** — GFG `Easy`
> Build triangle where each row = adjacent sums of row below. Print top to bottom.

```java
void sumTriangle(int[] arr) {
    if (arr.length==1) { print(arr[0]); return; }
    int[] next = new int[arr.length-1];
    for (int i=0; i<arr.length-1; i++) next[i]=arr[i]+arr[i+1];
    sumTriangle(next);     // recurse first (prints smaller rows)
    println();
    print(arr);            // then print current row (unwinds bottom-up)
}
```

> 💡 Print AFTER the recursive call so the top (single element) prints first.

---

**Q5. Maximum and Minimum in Array using Recursion** — GFG `Easy`
```java
int findMax(int[] arr, int i) {
    if (i==arr.length-1) return arr[i];
    return Math.max(arr[i], findMax(arr, i+1));
}
int findMin(int[] arr, int i) {
    if (i==arr.length-1) return arr[i];
    return Math.min(arr[i], findMin(arr, i+1));
}
```

---

**Q6. Binary Search using Recursion** — GFG `Easy`
```java
int binarySearch(int[] arr, int lo, int hi, int target) {
    if (lo > hi) return -1;
    int mid = lo + (hi-lo)/2;
    if (arr[mid]==target) return mid;
    if (arr[mid]<target) return binarySearch(arr, mid+1, hi, target);
    return binarySearch(arr, lo, mid-1, target);
}
```
```python
def binary_search(arr, lo, hi, target):
    if lo>hi: return -1
    mid=(lo+hi)//2
    if arr[mid]==target: return mid
    if arr[mid]<target: return binary_search(arr, mid+1, hi, target)
    return binary_search(arr, lo, mid-1, target)
```
> Recursion depth = O(log n). Stack space = O(log n).

---

### MIXED PROBLEMS

**Q7. Next Greater Element** — [LC #496](https://leetcode.com/problems/next-greater-element-i/) `Medium`
> For each element in nums1, find next greater element in nums2. Use monotonic stack.
```python
def nextGreaterElement(self, nums1, nums2):
    nge, stack = {}, []
    for n in nums2:
        while stack and stack[-1] < n:
            nge[stack.pop()] = n
        stack.append(n)
    return [nge.get(n, -1) for n in nums1]
```

---

**Q8. Reverse String** — [LC #344](https://leetcode.com/problems/reverse-string/) `Easy`
> Reverse character array in-place using recursion (two-pointer shrinking).
```java
void reverse(char[] s, int lo, int hi) {
    if (lo>=hi) return;
    char tmp=s[lo]; s[lo]=s[hi]; s[hi]=tmp;
    reverse(s, lo+1, hi-1);
}
```
```python
def rev(lo, hi):
    if lo>=hi: return
    s[lo],s[hi]=s[hi],s[lo]
    rev(lo+1, hi-1)
rev(0, len(s)-1)
```

---

**Q9. Print 1 to N Without Loop** — GFG `Easy`
```java
void print1ToN(int n) {
    if (n==0) return;
    print1ToN(n-1);          // recurse first → unwinds in order 1→N
    System.out.print(n+" ");
}
```
```python
def print1_to_n(n):
    if n==0: return
    print1_to_n(n-1)
    print(n, end=' ')
```

---

## ✅ Checklist Before You Sleep

- [ ] Every recursive function has a base case + recursive case — I know both
- [ ] I can trace a call stack on paper for 3-4 levels
- [ ] Print AFTER recursive call = forward order. Print BEFORE = reverse order
- [ ] I implemented Binary Search recursively
- [ ] I reversed a String array recursively (two-pointer shrinking)
- [ ] I printed 1 to N without any loop
- [ ] Recursion uses O(n) call stack space — risk of stack overflow for large n
- [ ] I solved all 9 problems

---

## 💬 Community

Which problem gave you the most trouble today? Drop the number in the community.

**Solved all 9? Drop a 🔥 in the community.**

---

*Next up → Day 17: More Recursion + Backtracking introduction*
