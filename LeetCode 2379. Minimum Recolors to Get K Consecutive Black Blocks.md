### **LeetCode 2379. Minimum Recolors to Get K Consecutive Black Blocks**
![image](https://github.com/user-attachments/assets/890bbde0-28c5-40d6-96e8-b87bdb928232)

---

#### **Problem Statement**
- You are given a string `blocks` of length `n`, where each character is either `'W'` (white) or `'B'` (black).
- You are also given an integer `k`, representing the desired number of consecutive black blocks.
- In one operation, you can recolor a white block (`'W'`) to black (`'B'`).
- Return the **minimum number of operations** needed to get at least `k` consecutive black blocks.

---

#### **Key Insights**
1. **Sliding Window Technique**:
   - The problem requires finding a window of size `k` with the minimum number of `'W'` characters.
   - A sliding window of size `k` is used to efficiently count the number of `'W'` characters in each window.

2. **Optimization**:
   - Instead of recalculating the number of `'W'` characters in each window from scratch, we can update the count by sliding the window one step at a time.

3. **Edge Cases**:
   - If `k` is 0 or greater than the length of `blocks`, return 0.
   - If the string already contains `k` consecutive `'B'` blocks, return 0.

---

#### **Solution Approach**
1. **Initialize**:
   - Use a variable `min_ops` to store the minimum number of operations required. Set it to a large value initially (e.g., `INT_MAX`).
   - Use a variable `count_W` to count the number of `'W'` characters in the current window.

2. **First Window**:
   - Count the number of `'W'` characters in the first window of size `k`.

3. **Slide the Window**:
   - Move the window one step at a time:
     - If the character leaving the window is `'W'`, decrement `count_W`.
     - If the character entering the window is `'W'`, increment `count_W`.
   - Update `min_ops` if the current window has fewer `'W'` characters than the previous minimum.

4. **Return Result**:
   - After processing all windows, return `min_ops`.

---

#### **Code Explanation**
```c
#include <limits.h>
#include <string.h>

int minimumRecolors(char* blocks, int k) {
    int n = strlen(blocks); // Length of the string
    int min_ops = INT_MAX; // Initialize minimum operations to a large value
    int count_W = 0; // Count of 'W' in the current window

    // Count 'W' in the first window
    for (int i = 0; i < k; i++) {
        if (blocks[i] == 'W') {
            count_W++;
        }
    }
    min_ops = count_W; // Update minimum operations

    // Slide the window across the string
    for (int i = k; i < n; i++) {
        // Remove the leftmost character of the previous window
        if (blocks[i - k] == 'W') {
            count_W--;
        }
        // Add the new character to the window
        if (blocks[i] == 'W') {
            count_W++;
        }
        // Update minimum operations
        if (count_W < min_ops) {
            min_ops = count_W;
        }
    }

    return min_ops; // Return the minimum number of operations
}
```

---

#### **Example Walkthrough**

**Input**:
```
blocks = "WBBWWBBWBW", k = 7
```

**Step-by-Step Execution**:
1. **First Window (Indices 0 to 6)**:
   - Window: `"WBBWWBB"`
   - Count of `'W'`: 3 (`W` at indices 0, 3, 4)
   - Update `min_ops = 3`.

2. **Second Window (Indices 1 to 7)**:
   - Window: `"BBWWBBW"`
   - Character leaving: `'W'` (index 0) → Decrement `count_W` to 2.
   - Character entering: `'W'` (index 7) → Increment `count_W` to 3.
   - `min_ops` remains 3.

3. **Third Window (Indices 2 to 8)**:
   - Window: `"BWWBBWB"`
   - Character leaving: `'B'` (index 1) → No change.
   - Character entering: `'B'` (index 8) → No change.
   - `count_W` remains 3.
   - `min_ops` remains 3.

4. **Fourth Window (Indices 3 to 9)**:
   - Window: `"WWBBWBW"`
   - Character leaving: `'W'` (index 2) → Decrement `count_W` to 2.
   - Character entering: `'W'` (index 9) → Increment `count_W` to 3.
   - `min_ops` remains 3.

5. **Result**:
   - The minimum number of `'W'` characters in any window of size 7 is **3**.
   - Therefore, the minimum number of operations required is **3**.

---

#### **Complexity Analysis**
1. **Time Complexity**:
   - O(n), where `n` is the length of the string `blocks`.
   - We traverse the string once using the sliding window.

2. **Space Complexity**:
   - O(1), as we use only a few variables for counting and storing results.

---

#### **Key Takeaways**
- The sliding window technique is highly efficient for problems involving subarrays or substrings of fixed size.
- By maintaining a running count of `'W'` characters, we avoid redundant calculations and achieve optimal performance.
- Edge cases (e.g., `k = 0` or `k > n`) should always be handled to ensure correctness.

---
