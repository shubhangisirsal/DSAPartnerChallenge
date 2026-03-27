# Day 19 — Maths for DSA: Part 2

> **DSA Partner Challenge** | Week 3

---

## 📌 Topic of the Day

**GCD · LCM · Primes · Sieve · Modular Arithmetic · Combinatorics**

---

## 🎥 Resource

[Maths for DSA — Part 2](https://youtu.be/lmSpZ0bjCyQ?si=gPZPUcio513C4lAL)

---

## 🧠 Part 1 — GCD (Greatest Common Divisor)

**Euclidean Algorithm:** `GCD(a, b) = GCD(b, a % b)` → base: `GCD(a, 0) = a`

```
GCD(48, 18):
48 = 2×18 + 12  →  GCD(18, 12)
18 = 1×12 + 6   →  GCD(12, 6)
12 = 2×6  + 0   →  GCD(6, 0) = 6
```

```java
// Java iterative (preferred)
int gcd(int a, int b) {
    while (b != 0) { int t=b; b=a%b; a=t; }
    return a;
}
```
```python
import math
math.gcd(48, 18)   # 6 — built-in
```

**Complexity:** O(log min(a, b))

---

## 🧠 Part 2 — LCM (Least Common Multiple)

**Formula:** `LCM(a, b) = (a / GCD(a, b)) × b`

> ⚠️ Always divide FIRST to avoid overflow: `(a / gcd) * b`, not `(a * b) / gcd`

```java
long lcm(long a, long b) { return (a / gcd(a, b)) * b; }
```
```python
import math; math.lcm(12, 18)   # 36 (Python 3.9+)
```

---

## 🧠 Part 3 — Prime Numbers

### Trial Division — O(√n)
```java
boolean isPrime(int n) {
    if (n<2) return false;
    if (n==2) return true;
    if (n%2==0) return false;
    for (int i=3; i*i<=n; i+=2)   // i*i avoids sqrt()
        if (n%i==0) return false;
    return true;
}
```

### Sieve of Eratosthenes — All primes ≤ n: O(n log log n)
```java
boolean[] sieve(int n) {
    boolean[] isPrime = new boolean[n+1];
    Arrays.fill(isPrime, true);
    isPrime[0] = isPrime[1] = false;
    for (int p=2; p*p<=n; p++)
        if (isPrime[p])
            for (int m=p*p; m<=n; m+=p)
                isPrime[m] = false;
    return isPrime;
}
```
> Start marking from **p²** — all smaller multiples already marked by smaller primes.

---

## 🧠 Part 4 — Modular Arithmetic

| Property | Formula |
|----------|---------|
| Addition | `(a+b)%m = ((a%m)+(b%m))%m` |
| Subtraction | `(a-b+m)%m` (prevents negative) |
| Multiplication | `(a*b)%m = ((a%m)*(b%m))%m` |

**Fast Modular Exponentiation — O(log b):**
```java
long power(long base, long exp, long mod) {
    long result=1; base%=mod;
    while (exp>0) {
        if ((exp&1)==1) result=result*base%mod;
        exp>>=1; base=base*base%mod;
    }
    return result;
}
```
```python
pow(base, exp, mod)   # built-in — always use this in Python!
```

> MOD = `10^9 + 7` (1_000_000_007) — prime, used in competitive programming. Apply at every step.

---

## 🧠 Part 5 — Combinatorics

**nCr = n! / (r! × (n-r)!)** — unordered selection

```python
from math import comb
comb(5, 2)   # 10
```

**Unique Paths formula:** Moving in m×n grid (only right/down) = `C(m+n-2, m-1)`

---

## 💻 Practice Problems — 6 LeetCode Problems

---

**Q1. Integer to Roman** — [LC #12](https://leetcode.com/problems/integer-to-roman/) `Medium`
> Greedy: values table from 1000 down to 1 (include IV=4, IX=9, XL=40, XC=90, CD=400, CM=900).
```python
vals = [1000,900,500,400,100,90,50,40,10,9,5,4,1]
syms = ['M','CM','D','CD','C','XC','L','XL','X','IX','V','IV','I']
res = ''
for v,s in zip(vals,syms):
    while num>=v: res+=s; num-=v
return res
```

---

**Q2. Unique Paths** — [LC #62](https://leetcode.com/problems/unique-paths/) `Medium`
> Combinatorics: `C(m+n-2, m-1)` — choose which moves are "down".
```python
from math import comb
return comb(m+n-2, m-1)
```
> Or DP: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`

---

**Q3. Gray Code** — [LC #89](https://leetcode.com/problems/gray-code/) `Medium`
> Formula: `i ^ (i >> 1)` for each i from 0 to 2^n - 1.
```python
return [i ^ (i>>1) for i in range(1<<n)]
```

---

**Q4. Perfect Squares** — [LC #279](https://leetcode.com/problems/perfect-squares/) `Medium`
> DP: `dp[i] = min(dp[i - j*j] + 1)` for all j where j²≤i.
```python
dp = [float('inf')] * (n+1); dp[0]=0
for i in range(1, n+1):
    j=1
    while j*j<=i: dp[i]=min(dp[i], dp[i-j*j]+1); j+=1
return dp[n]
```
> By Lagrange's theorem, answer is always 1, 2, 3, or 4.

---

**Q5. Next Greater Element III** — [LC #556](https://leetcode.com/problems/next-greater-element-iii/) `Medium`
> Next permutation on the digits. Find rightmost i where d[i]<d[i+1]. Swap with next-greater digit. Reverse suffix.
```python
d = list(str(n)); i = len(d)-2
while i>=0 and d[i]>=d[i+1]: i-=1
if i<0: return -1
j=len(d)-1
while d[j]<=d[i]: j-=1
d[i],d[j]=d[j],d[i]; d[i+1:]=d[i+1:][::-1]
res=int(''.join(d))
return res if res<=2**31-1 else -1
```

---

**Q6. Angle Between Hands of a Clock** — [LC #1344](https://leetcode.com/problems/angle-between-hands-of-a-clock/) `Medium`
> Minute hand: 6°/min. Hour hand: 0.5°/min.
```python
def angleClock(self, hour, minutes):
    min_angle  = 6 * minutes
    hour_angle = 0.5 * (hour%12 * 60 + minutes)
    diff = abs(hour_angle - min_angle)
    return min(diff, 360 - diff)
```

---

## ✅ Checklist Before You Sleep

- [ ] I can implement GCD (Euclidean) — both recursive and iterative
- [ ] I know LCM = (a/GCD) × b — divide first to prevent overflow
- [ ] I can check primality in O(√n) using `i*i <= n`
- [ ] I know the Sieve of Eratosthenes and why we start marking at p²
- [ ] I know the 3 modular arithmetic properties
- [ ] I know fast modular exponentiation O(log b)
- [ ] I know Unique Paths = C(m+n-2, m-1)
- [ ] I solved all 6 LeetCode problems

---

## 💬 Community

Which maths trick surprised you most today? Drop it in the community.

**Solved all 6? Drop a 🔥 in the community.**

---

*Next up → Day 20: Introduction to Hashing — HashMap, HashSet*
