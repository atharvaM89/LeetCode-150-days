# TC

### Q1.

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j += 2) {
        
    }
}

```

**Answer:**

- Outer loop: runs `n` times
- Inner loop: runs `n/2` ≈ `O(n)`
- Total = `O(n * n)` = **O(n²)**

---

### Q2.

```java
for (int i = 1; i <= n; i *= 2) {
    for (int j = 0; j < i; j++) {
        // O(1)
    }
}

```

**Answer:**

- Outer loop: `i` doubles → runs `log n` times
- Inner loop sum: `1 + 2 + 4 + … + n = O(n)`
- Total = **O(n)**

---

### Q3.

```java
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        // O(1)
    }
}

```

**Answer:**

- Inner loop length decreases: `(n) + (n-1) + (n-2) … + 1 = O(n²)`
- Total = **O(n²)**

---

### Q4.

```java
for (int i = 0; i < n; i++) {
    for (int j = 1; j < n; j *= 2) {
        // O(1)
    }
}

```

**Answer:**

- Outer loop = `n`
- Inner loop = `log n`
- Total = **O(n log n)**

---

### Q5.

```java
int k = 0;
for (int i = 0; i < n; i++) {
    while (k < n && arr[k] < arr[i]) {
        k++;
    }
}

```

**Answer:**

- Outer loop = `n`
- Inner loop doesn’t reset, total `k` increments = `n`
- Total = **O(n)** (amortized trick)

---

---

## **Hard Level**

### Q6.

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        for (int k = 1; k <= j; k++) {
            // O(1)
        }
    }
}

```

**Answer:**

- Work = ∑(i=1→n) ∑(j=1→i) (j)
- = ∑(i=1→n) (i(i+1)/2) = O(n³)
- Total = **O(n³)**

---

### Q7.

```java
for (int i = n; i > 0; i /= 2) {
    for (int j = 0; j < i; j++) {
        // O(1)
    }
}

```

**Answer:**

- Work = n + n/2 + n/4 + … = 2n
- Total = **O(n)**

---

### Q8. (Divide and Conquer)

```java
T(n) = 2T(n/2) + O(n)

```

**Answer:**

- By Master Theorem: a=2, b=2, f(n)=n
- Case 2: f(n) = Θ(n^log₂2) = Θ(n)
- So T(n) = **O(n log n)**

---

### Q9. (Recurrence)

```java
T(n) = T(n-1) + O(1)

```

**Answer:**

- Expands: T(n) = T(n-2) + O(1) + O(1) = … = O(n)
- Total = **O(n)**

---

### Q10.

```java
T(n) = T(n/2) + T(n/3) + O(n)

```

**Answer:**

- Approx recurrence: T(n) ≤ T(n/2) + T(n/3) + n
- By Akra-Bazzi: solution = **O(n log n)**

---

---

## **Brutal Level (Very Hard 💀)**

### Q11.

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        while (k < n) {
            k *= 2;
        }
    }
}

```

**Answer:**

- Outer `i` = n
- Inner `j` = n
- Inner while: log n, but **runs only once fully**, afterward k ≥ n
- Total = **O(n² + log n) = O(n²)**

---

### Q12.

```java
T(n) = 2T(n/2) + n / log n

```

**Answer:**

- a=2, b=2, log_b a = 1
- f(n) = n/log n = smaller than n but not polynomially smaller → **Case 2** variant
- Solution = **Θ(n log log n)**

---

### Q13.

```java
for (int i = 0; i < n; i++) {
    for (int j = i; j > 0; j /= 2) {
        // O(1)
    }
}

```

**Answer:**

- For each i, inner loop = log i
- Total = ∑ log i (i=1→n) = O(n log n)
- Answer = **O(n log n)**

---

### Q14. (Tricky Recurrence)

```java
T(n) = T(n - √n) + O(1)

```

**Answer:**

- Decreases by √n each step → #steps ≈ √n
- Total = **O(√n)**

---

### Q15. (Killer One 🤯)

```java
T(n) = T(n/2) + T(n/4) + T(n/8) + O(n)

```

**Answer:**

- This is like weighted recursion tree
- Work per level: n + n/2 + n/4 + … = 2n
- Depth = log n
- Total = **O(n log n)**