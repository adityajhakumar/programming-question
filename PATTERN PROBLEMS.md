Here is a list of Java solutions for the 25 pattern design problems 

---

### 1. **Solid Rectangle**  
```
*****
*****
*****
```

**Solution:**  
```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 5; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 2. **Hollow Rectangle**  
```
*****
*   *
*****
```

**Solution:**  
```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 5; j++) {
        if (i == 1 || i == 3 || j == 1 || j == 5) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

---

### 3. **Right-Angled Triangle**  
```
*
**
***
****
```

**Solution:**  
```java
for (int i = 1; i <= 4; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 4. **Inverted Right-Angled Triangle**  
```
****
***
**
*
```

**Solution:**  
```java
for (int i = 4; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 5. **Pyramid**  
```
   *
  ***
 *****
*******
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 6. **Inverted Pyramid**  
```
*******
 *****
  ***
   *
```

**Solution:**  
```java
int n = 4;
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 7. **Diamond**  
```
   *
  ***
 *****
*******
 *****
  ***
   *
```

**Solution:**  
```java
int n = 4;
// Upper half
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
// Lower half
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 8. **Hollow Diamond**  
```
   *
  * *
 *   *
*     *
 *   *
  * *
   *
```

**Solution:**  
```java
int n = 4;
// Upper half
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        if (j == 1 || j == 2 * i - 1) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
// Lower half
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        if (j == 1 || j == 2 * i - 1) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

---

### 9. **Solid Square**  
```
*****
*****
*****
*****
*****
```

**Solution:**  
```java
int n = 5;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---



---

### 10. **Hollow Square**  
```
*****
*   *
*   *
*   *
*****
```

**Solution:**  
```java
int n = 5;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        if (i == 1 || i == n || j == 1 || j == n) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

---

### 11. **Right-Angled Triangle (Mirrored)**  
```
   *
  **
 ***
****
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 12. **Pascal’s Triangle**  
```
   1
  1 1
 1 2 1
1 3 3 1
```

**Solution:**  
```java
int n = 4;
for (int i = 0; i < n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    int number = 1;
    for (int j = 0; j <= i; j++) {
        System.out.print(number + " ");
        number = number * (i - j) / (j + 1);
    }
    System.out.println();
}
```

---

### 13. **Number Triangle**  
```
1
12
123
1234
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j);
    }
    System.out.println();
}
```

---

### 14. **Inverted Number Triangle**  
```
1234
123
12
1
```

**Solution:**  
```java
int n = 4;
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j);
    }
    System.out.println();
}
```

---

### 15. **Floyd’s Triangle**  
```
1
2 3
4 5 6
7 8 9 10
```

**Solution:**  
```java
int n = 4;
int number = 1;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(number + " ");
        number++;
    }
    System.out.println();
}
```

---

### 16. **Alternating Binary Triangle**  
```
1
01
101
0101
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    int start = i % 2 == 0 ? 0 : 1;
    for (int j = 1; j <= i; j++) {
        System.out.print(start);
        start = 1 - start;
    }
    System.out.println();
}
```

---

### 17. **Checkerboard Pattern**  
```
10101
01010
10101
01010
10101
```

**Solution:**  
```java
int n = 5;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        if ((i + j) % 2 == 0) {
            System.out.print("1");
        } else {
            System.out.print("0");
        }
    }
    System.out.println();
}
```

---

### 18. **Butterfly Pattern**  
```
*      *
**    **
***  ***
********
***  ***
**    **
*      *
```

**Solution:**  
```java
int n = 4;
// Upper half
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    for (int j = 1; j <= 2 * (n - i); j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
// Lower half
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    for (int j = 1; j <= 2 * (n - i); j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---

### 19. **Zig-Zag Pattern**  
```
   *   *
  * * * *
 *   *   *
```

**Solution:**  
```java
int n = 9;
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= n; j++) {
        if ((i + j) % 4 == 0 || (i == 2 && j % 4 == 0)) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

---

### 20. **Hourglass Pattern**  
```
*******
 *****
  ***
   *
  ***
 *****
*******
```

**Solution:**  
```java
int n = 4;
// Upper half
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
// Lower half
for (int i = 2; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= 2 * i - 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

---



---

### 21. **Hollow Right-Angled Triangle**  
```
*
**
* *
*  *
*****
```

**Solution:**  
```java
int n = 5;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        if (j == 1 || j == i || i == n) {
            System.out.print("*");
        } else {
            System.out.print(" ");
        }
    }
    System.out.println();
}
```

---

### 22. **Staircase Pattern**  
```
   #
  ##
 ###
####
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print("#");
    }
    System.out.println();
}
```

---

### 23. **Number Diamond**  
```
   1
  121
 12321
1234321
 12321
  121
   1
```

**Solution:**  
```java
int n = 4;
// Upper half
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print(j);
    }
    for (int j = i - 1; j >= 1; j--) {
        System.out.print(j);
    }
    System.out.println();
}
// Lower half
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print(j);
    }
    for (int j = i - 1; j >= 1; j--) {
        System.out.print(j);
    }
    System.out.println();
}
```

---

### 24. **Alphabet Pyramid**  
```
   A
  ABA
 ABCBA
ABCDCBA
```

**Solution:**  
```java
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n - i; j++) {
        System.out.print(" ");
    }
    for (int j = 1; j <= i; j++) {
        System.out.print((char) ('A' + j - 1));
    }
    for (int j = i - 1; j >= 1; j--) {
        System.out.print((char) ('A' + j - 1));
    }
    System.out.println();
}
```

---

### 25. **Spiral Numbers (Square)**  
```
1  2  3  4
12 13 14 5
11 16 15 6
10  9  8 7
```

**Solution:**  
```java
int n = 4;
int[][] spiral = new int[n][n];

int top = 0, bottom = n - 1, left = 0, right = n - 1;
int num = 1;

while (top <= bottom && left <= right) {
    // Top row
    for (int i = left; i <= right; i++) {
        spiral[top][i] = num++;
    }
    top++;

    // Right column
    for (int i = top; i <= bottom; i++) {
        spiral[i][right] = num++;
    }
    right--;

    // Bottom row
    for (int i = right; i >= left; i--) {
        spiral[bottom][i] = num++;
    }
    bottom--;

    // Left column
    for (int i = bottom; i >= top; i--) {
        spiral[i][left] = num++;
    }
    left++;
}

// Print the spiral matrix
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.printf("%2d ", spiral[i][j]);
    }
    System.out.println();
}
```

---
