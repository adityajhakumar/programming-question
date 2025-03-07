### **LeetCode 2523: Closest Prime Numbers in a Range**  

---

## **Problem Statement**
You are given two integers `left` and `right`, where `left ≤ right`.  
Find the **two closest prime numbers** in this range.  

- If there are **multiple pairs** with the smallest difference, return the **first** pair found.
- If there are **less than two primes**, return `[-1, -1]`.

### **Example 1**
#### **Input**
```
left = 10, right = 20
```
#### **Output**
```
[11, 13]
```
#### **Explanation**
The prime numbers in the range `[10, 20]` are **[11, 13, 17, 19]**.  
The closest pair is **(11, 13)** with a difference of `2`.

---

### **Example 2**
#### **Input**
```
left = 4, right = 6
```
#### **Output**
```
[-1, -1]
```
#### **Explanation**
There are no prime numbers in the range `[4, 6]`.

---

# **Approach 1: Brute Force (Checking Each Number)**
## ✅ **Idea**
1. Iterate from `left` to `right`, checking whether each number is **prime**.
2. If a number is prime, compare it with the previous prime to find the **closest pair**.

## ⏳ **Time Complexity**
- Checking each number takes **O(√N)**.
- Iterating through the range takes **O(N√N)**.
- **Overall Complexity: O(N√N)** (not efficient for large `right` values).

---

## 💻 **Code (Brute Force)**
```java
class Solution {
    public int[] closestPrimes(int left, int right) {
        int prev = -1, p1 = -1, p2 = -1;
        int minDiff = Integer.MAX_VALUE;

        for (int i = left; i <= right; i++) {
            if (i < 2) continue;
            boolean isPrime = true;
            for (int j = 2; j * j <= i; j++) {
                if (i % j == 0) {
                    isPrime = false;
                    break;
                }
            }
            
            if (isPrime) {
                if (prev != -1 && (i - prev) < minDiff) {
                    minDiff = i - prev;
                    p1 = prev;
                    p2 = i;
                }
                prev = i;
            }
        }
        return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};
    }
}
```

---

## 📌 **Walkthrough of Brute Force Approach**
#### **Input:** `left = 10, right = 20`
- **Prime numbers found**: `[11, 13, 17, 19]`
- **Checking closest pair**:
  - `(11, 13)` → Difference = `2`
  - `(13, 17)` → Difference = `4`
  - `(17, 19)` → Difference = `2`
- **Smallest difference** is `2`, first found at `(11, 13)`.
- **Output:** `[11, 13]`

---

# **Approach 2: Optimized Using Sieve of Eratosthenes**
## ✅ **Idea**
1. Instead of checking each number separately, **precompute all primes** using the **Sieve of Eratosthenes**.
2. Once primes are known, **finding the closest pair** is **O(N)**.

## ⏳ **Time Complexity**
- **Sieve of Eratosthenes** runs in **O(N log log N)**.
- **Finding closest pair** is **O(N)**.
- **Overall Complexity: O(N log log N) → much faster!**

---

## 💻 **Code (Optimized with Sieve)**
```java
import java.util.Arrays;

class Solution {
    public int[] closestPrimes(int left, int right) {
        // Step 1: Use Sieve of Eratosthenes to find all primes up to 'right'
        boolean[] isPrime = new boolean[right + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false; // 0 and 1 are not prime
        
        for (int i = 2; i * i <= right; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= right; j += i) {
                    isPrime[j] = false; // Mark multiples as non-prime
                }
            }
        }

        // Step 2: Find the closest pair of primes
        int prev = -1, p1 = -1, p2 = -1;
        int minDiff = Integer.MAX_VALUE;

        for (int i = left; i <= right; i++) {
            if (isPrime[i]) {
                if (prev != -1 && (i - prev) < minDiff) {
                    minDiff = i - prev;
                    p1 = prev;
                    p2 = i;
                }
                prev = i;
            }
        }

        return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};
    }
}
```

---

## 📌 **Walkthrough of Sieve Approach**
#### **Input:** `left = 10, right = 50`
#### **Step 1: Compute Prime Numbers Using Sieve**
**Prime numbers found in `[10, 50]`:**  
`[11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]`

#### **Step 2: Find the Closest Pair**
- **Checking closest pairs**:
  - `(11, 13)` → Difference = **2** (smallest found first)
  - `(13, 17)` → Difference = `4`
  - `(17, 19)` → Difference = `2`
- **Output:** `[11, 13]`

---

# **Comparison of Approaches**
| Approach | Time Complexity | Space Complexity | Suitable For |
|----------|---------------|----------------|--------------|
| **Brute Force** | `O(N√N)` | `O(1)` | Small Ranges (e.g., `N ≤ 10⁵`) |
| **Sieve of Eratosthenes** | `O(N log log N)` | `O(N)` | Large Ranges (e.g., `N ≥ 10⁶`) |

---

 **detailed explanation** of both approaches, with **line-by-line breakdowns** of the code.

---

# **Approach 1: Brute Force (Checking Each Number)**
## ✅ **Idea**
- Iterate through each number in the range `[left, right]`.
- Check if the number is **prime** using a loop up to `√N`.
- Keep track of the **previous prime** found.
- If a new prime is found, compare it with the previous prime to **update the closest pair**.

---

## 💻 **Code (Brute Force)**
```java
class Solution {
    public int[] closestPrimes(int left, int right) {
        int prev = -1, p1 = -1, p2 = -1;  // Stores previous prime and closest prime pair
        int minDiff = Integer.MAX_VALUE;  // Keeps track of the minimum difference

        for (int i = left; i <= right; i++) {  // Iterate through the range
            if (i < 2) continue;  // Ignore numbers less than 2 (not prime)
            boolean isPrime = true;  // Assume current number is prime

            for (int j = 2; j * j <= i; j++) {  // Check divisibility up to sqrt(i)
                if (i % j == 0) {  // If divisible, it's not prime
                    isPrime = false;
                    break;
                }
            }
            
            if (isPrime) {  // If current number is prime
                if (prev != -1 && (i - prev) < minDiff) {  // If previous prime exists and difference is smaller
                    minDiff = i - prev;
                    p1 = prev;
                    p2 = i;
                }
                prev = i;  // Update previous prime
            }
        }

        return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};  // Return result
    }
}
```

---

## 📌 **Line-by-Line Explanation**
### **Initialization**
```java
int prev = -1, p1 = -1, p2 = -1;
int minDiff = Integer.MAX_VALUE;
```
- `prev`: Stores the **previous prime** found.
- `p1, p2`: Stores the **closest prime pair**.
- `minDiff`: Stores the **smallest difference** between primes.

### **Looping Through the Range**
```java
for (int i = left; i <= right; i++) {
```
- Iterate over **each number** from `left` to `right`.

### **Checking if the Number is Prime**
```java
if (i < 2) continue;
boolean isPrime = true;
for (int j = 2; j * j <= i; j++) {
    if (i % j == 0) {
        isPrime = false;
        break;
    }
}
```
- Skip numbers **less than 2**.
- Assume `i` is **prime** (`isPrime = true`).
- Check if `i` is divisible by any number from `2` to `√i`:
  - If **divisible**, mark `isPrime = false` and **exit the loop**.

### **Updating the Closest Prime Pair**
```java
if (isPrime) {
    if (prev != -1 && (i - prev) < minDiff) {
        minDiff = i - prev;
        p1 = prev;
        p2 = i;
    }
    prev = i;
}
```
- If `i` is **prime**:
  - Check if `prev` (previous prime) exists.
  - If the **difference** between `i` and `prev` is **smaller than minDiff**, update `p1` and `p2`.
  - Update `prev` to `i` (store the last prime found).

### **Returning the Result**
```java
return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};
```
- If **no prime pair** found, return `[-1, -1]`.
- Otherwise, return **the closest prime pair**.

---

## ⏳ **Time Complexity**
- **Checking primality** of `N` numbers → `O(N√N)`
- **Overall Complexity:** `O(N√N)`

---

## 🚀 **Optimized Approach: Sieve of Eratosthenes**
### ✅ **Idea**
1. **Precompute all primes up to `right`** using the **Sieve of Eratosthenes**.
2. **Use a single scan** over the range `[left, right]` to find the closest prime pair.

---

## 💻 **Code (Optimized with Sieve)**
```java
import java.util.Arrays;

class Solution {
    public int[] closestPrimes(int left, int right) {
        boolean[] isPrime = new boolean[right + 1];  // Boolean array to mark primes
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;  // 0 and 1 are not prime

        for (int i = 2; i * i <= right; i++) {  // Run sieve
            if (isPrime[i]) {
                for (int j = i * i; j <= right; j += i) {
                    isPrime[j] = false;  // Mark multiples as non-prime
                }
            }
        }

        int prev = -1, p1 = -1, p2 = -1;
        int minDiff = Integer.MAX_VALUE;

        for (int i = left; i <= right; i++) {  // Iterate through the range
            if (isPrime[i]) {
                if (prev != -1 && (i - prev) < minDiff) {
                    minDiff = i - prev;
                    p1 = prev;
                    p2 = i;
                }
                prev = i;
            }
        }

        return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};
    }
}
```

---

## 📌 **Line-by-Line Explanation**
### **Step 1: Create an Array to Mark Primes**
```java
boolean[] isPrime = new boolean[right + 1];
Arrays.fill(isPrime, true);
isPrime[0] = isPrime[1] = false;
```
- Create an **array** to store prime numbers.
- Initialize all numbers as **prime**.
- Mark **0 and 1** as **not prime**.

### **Step 2: Run the Sieve of Eratosthenes**
```java
for (int i = 2; i * i <= right; i++) {
    if (isPrime[i]) {
        for (int j = i * i; j <= right; j += i) {
            isPrime[j] = false;
        }
    }
}
```
- Start from `2`, mark **multiples of each prime** as **not prime**.
- **Optimized sieving**: Start marking from `i * i` instead of `2 * i`.

### **Step 3: Find the Closest Prime Pair**
```java
int prev = -1, p1 = -1, p2 = -1;
int minDiff = Integer.MAX_VALUE;

for (int i = left; i <= right; i++) {
    if (isPrime[i]) {
        if (prev != -1 && (i - prev) < minDiff) {
            minDiff = i - prev;
            p1 = prev;
            p2 = i;
        }
        prev = i;
    }
}
```
- **Iterate through `[left, right]`** and find prime numbers.
- Track **previous prime (`prev`)** and **update closest pair (`p1, p2`)**.

### **Step 4: Return the Result**
```java
return (p1 == -1) ? new int[]{-1, -1} : new int[]{p1, p2};
```
- If **no prime pair found**, return `[-1, -1]`.
- Otherwise, return **the closest prime pair**.

---

## ⏳ **Time Complexity**
- **Sieve of Eratosthenes:** `O(N log log N)`
- **Finding closest pair:** `O(N)`
- **Overall Complexity:** `O(N log log N)`

---

## **Comparison of Approaches**
| Approach | Time Complexity | Space Complexity | Suitable For |
|----------|---------------|----------------|--------------|
| **Brute Force** | `O(N√N)` | `O(1)` | Small Ranges (e.g., `N ≤ 10⁵`) |
| **Sieve of Eratosthenes** | `O(N log log N)` | `O(N)` | Large Ranges (e.g., `N ≥ 10⁶`) |

---

**🚀 Conclusion:**  
✔ Use **Brute Force** for **small `right` values**.  
✔ Use **Sieve of Eratosthenes** for **large `right` values**.  
✔ **Sieve is the best approach** for large constraints.
