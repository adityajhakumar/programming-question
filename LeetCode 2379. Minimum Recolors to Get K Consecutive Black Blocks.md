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
### Notes on **Logic Behind the Solution**

---

#### **Problem Understanding**
The problem requires transforming a string of blocks (`'W'` for white and `'B'` for black) into a string where there are at least `k` consecutive black blocks. The transformation involves recoloring white blocks (`'W'`) to black (`'B'`), and we need to minimize the number of such operations.

---

#### **Core Logic**
1. **Objective**:
   - Find a window of size `k` in the string `blocks` that contains the minimum number of `'W'` characters.
   - The number of `'W'` characters in this window represents the minimum number of recoloring operations needed.

2. **Why Sliding Window?**
   - The problem involves analyzing all possible substrings (windows) of fixed size `k`.
   - A sliding window allows us to efficiently traverse the string and compute the required metric (number of `'W'` characters) for each window without redundant calculations.

3. **Key Observations**:
   - For any window of size `k`, the number of `'W'` characters is the number of operations needed to make all blocks in that window black.
   - We need to find the window with the smallest number of `'W'` characters.

---

#### **Step-by-Step Logic**

1. **Initialize**:
   - Use a variable `min_ops` to store the minimum number of operations required. Initialize it to a large value (e.g., `INT_MAX`).
   - Use a variable `count_W` to count the number of `'W'` characters in the current window.

2. **First Window**:
   - Compute the number of `'W'` characters in the first window of size `k`.
   - Update `min_ops` with this count.

3. **Slide the Window**:
   - Move the window one step at a time:
     - When the window slides, the leftmost character of the previous window leaves, and a new character enters the window.
     - If the leaving character is `'W'`, decrement `count_W`.
     - If the entering character is `'W'`, increment `count_W`.
   - After updating `count_W`, check if it is smaller than `min_ops`. If so, update `min_ops`.

4. **Result**:
   - After processing all windows, `min_ops` will contain the minimum number of operations required.

---

#### **Why This Logic Works**
1. **Efficiency**:
   - By reusing the count of `'W'` characters from the previous window, we avoid recalculating from scratch for each new window. This reduces the time complexity to O(n).

2. **Correctness**:
   - The sliding window ensures that all possible windows of size `k` are considered.
   - By keeping track of the minimum number of `'W'` characters across all windows, we guarantee the optimal solution.

3. **Edge Cases**:
   - If `k = 0` or `k > n`, no operations are needed, and the result is 0.
   - If the string already contains `k` consecutive `'B'` blocks, no operations are needed, and the result is 0.

---

#### **Example Walkthrough with Logic**

**Input**:
```
blocks = "WBBWWBBWBW", k = 7
```

**Step-by-Step Logic**:
1. **First Window (Indices 0 to 6)**:
   - Window: `"WBBWWBB"`
   - Count of `'W'`: 3 (`W` at indices 0, 3, 4)
   - Update `min_ops = 3`.

2. **Second Window (Indices 1 to 7)**:
   - Character leaving: `'W'` (index 0) → Decrement `count_W` to 2.
   - Character entering: `'W'` (index 7) → Increment `count_W` to 3.
   - `min_ops` remains 3.

3. **Third Window (Indices 2 to 8)**:
   - Character leaving: `'B'` (index 1) → No change.
   - Character entering: `'B'` (index 8) → No change.
   - `count_W` remains 3.
   - `min_ops` remains 3.

4. **Fourth Window (Indices 3 to 9)**:
   - Character leaving: `'W'` (index 2) → Decrement `count_W` to 2.
   - Character entering: `'W'` (index 9) → Increment `count_W` to 3.
   - `min_ops` remains 3.

5. **Result**:
   - The minimum number of `'W'` characters in any window of size 7 is **3**.
   - Therefore, the minimum number of operations required is **3**.

---

#### **Key Takeaways**
1. **Sliding Window**:
   - The sliding window technique is ideal for problems involving fixed-size subarrays or substrings.
   - It ensures efficient traversal and computation by reusing results from previous steps.

2. **Optimization**:
   - By maintaining a running count of `'W'` characters, we avoid redundant calculations and achieve optimal performance.

3. **Edge Cases**:
   - Always handle edge cases (e.g., `k = 0`, `k > n`, or already valid strings) to ensure the solution is robust.

---
### **Updated Notes on Sliding Window Technique**

---

#### **What is the Sliding Window Technique?**
The **sliding window** technique is a strategy used to solve problems involving arrays, strings, or sequences by maintaining a "window" (a subarray or substring) and efficiently moving it through the data. It is particularly useful for problems that require analyzing or processing **contiguous subarrays or substrings** of a fixed or variable size.

---

#### **When to Use Sliding Window?**
The sliding window technique is applicable when:
1. The problem involves **subarrays or substrings**.
2. The problem requires finding a **maximum, minimum, or fixed-size window**.
3. The problem can be solved by **reusing computations** from previous steps (to avoid redundant calculations).

Examples of problems where sliding window is used:
- Finding the maximum sum of a subarray of size `k`.
- Finding the smallest substring containing all characters of a pattern.
- Counting the number of subarrays with a specific property.

---

#### **Types of Sliding Windows**
1. **Fixed-Size Window**:
   - The size of the window is fixed (e.g., find the maximum sum of a subarray of size `k`).
   - Example: The problem **2379. Minimum Recolors to Get K Consecutive Black Blocks** uses a fixed-size window.

2. **Variable-Size Window**:
   - The size of the window changes dynamically based on certain conditions.
   - Example: Finding the smallest substring containing all characters of a pattern.

---

#### **How Does Sliding Window Work?**
1. **Initialize the Window**:
   - Define the start and end of the window.
   - For a fixed-size window, the size is predetermined. For a variable-size window, the size changes based on conditions.

2. **Process the Window**:
   - Perform computations (e.g., count elements, calculate sums, etc.) within the current window.

3. **Slide the Window**:
   - Move the window one step at a time by adjusting the start and end pointers.
   - Update the computations based on the new element added to the window and the element removed from the window.

4. **Repeat Until Completion**:
   - Continue sliding the window until the entire array or string is processed.

---

#### **Advantages of Sliding Window**
1. **Efficiency**:
   - Reduces time complexity by reusing computations from previous steps.
   - Avoids redundant calculations by maintaining a running result.

2. **Simplicity**:
   - Easy to implement once the logic is understood.
   - Works well for problems involving contiguous subarrays or substrings.

3. **Optimization**:
   - Often reduces the time complexity from O(n²) (brute force) to O(n).

---

#### **Example: Fixed-Size Window**

**Problem**:
Find the maximum sum of a subarray of size `k`.

**Input**:
```
arr = [2, 1, 5, 1, 3, 2], k = 3
```

**Steps**:
1. **Initialize**:
   - Start with the first window: `[2, 1, 5]`.
   - Calculate the sum: `2 + 1 + 5 = 8`.

2. **Slide the Window**:
   - Move the window one step to the right:
     - Remove the leftmost element (`2`) and subtract it from the sum: `8 - 2 = 6`.
     - Add the new element (`1`) to the sum: `6 + 1 = 7`.
     - New window: `[1, 5, 1]`, sum = `7`.
   - Repeat for the next window:
     - Remove `1`, subtract: `7 - 1 = 6`.
     - Add `3`, update sum: `6 + 3 = 9`.
     - New window: `[5, 1, 3]`, sum = `9`.
   - Repeat for the next window:
     - Remove `5`, subtract: `9 - 5 = 4`.
     - Add `2`, update sum: `4 + 2 = 6`.
     - New window: `[1, 3, 2]`, sum = `6`.

3. **Result**:
   - The maximum sum among all windows is **9**.

---

#### **Example: Variable-Size Window**

**Problem**:
Find the smallest substring containing all characters of a pattern.

**Input**:
```
string = "ADOBECODEBANC", pattern = "ABC"
```

**Steps**:
1. **Initialize**:
   - Use two pointers, `left` and `right`, to represent the window.
   - Use a hashmap to store the frequency of characters in the pattern.

2. **Expand the Window**:
   - Move the `right` pointer to include characters in the window until all characters of the pattern are included.

3. **Shrink the Window**:
   - Move the `left` pointer to shrink the window while still containing all characters of the pattern.

4. **Repeat**:
   - Continue expanding and shrinking the window until the entire string is processed.

5. **Result**:
   - The smallest substring containing all characters of the pattern is **"BANC"**.

---

#### **Key Points to Remember**
1. **Fixed-Size Window**:
   - The window size remains constant.
   - Use a single loop to slide the window and update computations.

2. **Variable-Size Window**:
   - The window size changes dynamically.
   - Use two pointers (`left` and `right`) to expand and shrink the window.

3. **Efficiency**:
   - Sliding window reduces time complexity by reusing computations.
   - Avoids recalculating results for overlapping windows.

4. **Applications**:
   - Maximum/minimum subarray problems.
   - Substring problems (e.g., smallest/largest substring with specific properties).
   - Problems involving contiguous subarrays or substrings.

---

#### **Code Template for Sliding Window**

**Fixed-Size Window**:
```python
def fixed_sliding_window(arr, k):
    n = len(arr)
    window_sum = sum(arr[:k])  # Sum of the first window
    max_sum = window_sum

    for i in range(k, n):
        window_sum += arr[i] - arr[i - k]  # Slide the window
        max_sum = max(max_sum, window_sum)  # Update the result

    return max_sum
```

**Variable-Size Window**:
```python
def variable_sliding_window(s, pattern):
    left = 0
    min_len = float('inf')
    result = ""
    char_count = {}

    # Initialize character count for the pattern
    for char in pattern:
        char_count[char] = char_count.get(char, 0) + 1

    # Sliding window logic
    for right in range(len(s)):
        if s[right] in char_count:
            char_count[s[right]] -= 1

        # Check if all characters in the pattern are included
        while all(count <= 0 for count in char_count.values()):
            # Update the result if the current window is smaller
            if right - left + 1 < min_len:
                min_len = right - left + 1
                result = s[left:right + 1]

            # Shrink the window from the left
            if s[left] in char_count:
                char_count[s[left]] += 1
            left += 1

    return result
```

---

#### **Logic Behind the Code**
1. **Fixed-Size Window**:
   - Compute the sum of the first window.
   - Slide the window one step at a time by subtracting the leftmost element and adding the new element.
   - Update the result (e.g., maximum sum) after each slide.

2. **Variable-Size Window**:
   - Use two pointers (`left` and `right`) to represent the window.
   - Expand the window by moving the `right` pointer until the condition is met.
   - Shrink the window by moving the `left` pointer to find the smallest window that satisfies the condition.

---

#### **Updated Notes**
1. **Sliding Window**:
   - A powerful technique for solving problems involving subarrays or substrings.
   - Efficiently reuses computations from previous steps to avoid redundant calculations.

2. **Fixed vs. Variable Size**:
   - Fixed-size windows are simpler and use a single loop.
   - Variable-size windows require two pointers and dynamic resizing based on conditions.

3. **Applications**:
   - Maximum/minimum subarray sums.
   - Smallest/largest substrings with specific properties.
   - Problems involving contiguous sequences.

4. **Efficiency**:
   - Reduces time complexity from O(n²) to O(n) in many cases.
   - Ideal for optimizing problems with overlapping subproblems.

---

These updated notes provide a comprehensive understanding of the sliding window technique, including its logic, implementation, and applications.
