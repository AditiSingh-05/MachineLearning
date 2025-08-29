# 🧮 Python NumPy Full Tutorial: Beginner to Expert

> **Audience:** You know basic Python (`input`, `print`), but want to master NumPy for production-grade data science, numerical computing, and interviews.

---

## 📖 Table of Contents

1. [Concept Overview: What is NumPy?](#concept-overview-what-is-numpy)
2. [Why Use NumPy?](#why-use-numpy)
3. [Installing NumPy](#installing-numpy)
4. [Detailed Mechanics: NumPy Arrays vs Python Lists](#detailed-mechanics-numpy-arrays-vs-python-lists)
5. [Core Array Creation and Manipulation](#core-array-creation-and-manipulation)
6. [Array Indexing, Slicing, and Iteration](#array-indexing-slicing-and-iteration)
7. [Array Operations: Math, Broadcasting, Vectorization](#array-operations-math-broadcasting-vectorization)
8. [Shape Transformations, Reshaping, Flattening](#shape-transformations-reshaping-flattening)
9. [Random Number Generation](#random-number-generation)
10. [Aggregations, Statistics, and Axis Operations](#aggregations-statistics-and-axis-operations)
11. [Masked Arrays and Boolean Indexing](#masked-arrays-and-boolean-indexing)
12. [Advanced: Views, Copies, Memory Model](#advanced-views-copies-memory-model)
13. [Performance, Alternatives, and Integration](#performance-alternatives-and-integration)
14. [Common Mistakes, Pro Tips, Interview Angles](#common-mistakes-pro-tips-interview-angles)
15. [Extra Insights & References](#extra-insights--references)

---

## 1. Concept Overview: What is NumPy?

NumPy (Numerical Python) is the foundational library for numerical computing in Python.  
It provides a powerful n-dimensional array object (`ndarray`) and efficient operations for mathematical, logical, and statistical computations.

### Big Picture  
- **Core of scientific Python ecosystem** (used by pandas, scikit-learn, TensorFlow, PyTorch).
- Enables high-performance, vectorized operations (no slow Python loops for math).
- Used for data science, machine learning, physics, engineering, finance, and more.

---

## 2. Why Use NumPy?

- Python lists are slow and inefficient for numbers.
- NumPy arrays are **contiguous, typed blocks of memory**—enabling fast operations.
- Under-the-hood: implemented in C for speed; provides SIMD (Single Instruction, Multiple Data) vectorization.
- Powers almost every data science workflow: from basic math to multi-dimensional tensors.

---

## 3. Installing NumPy

```bash
pip install numpy
```

---

## 4. Detailed Mechanics: NumPy Arrays vs Python Lists

- **Python list:** Can hold mixed types, not memory efficient, slow for numerical ops.
- **NumPy array (`ndarray`):**  
  - Homogeneous data type (all elements must be same type).
  - Memory is contiguous; operations are performed in compiled C code.
  - Supports multi-dimensional arrays (matrices, tensors).

**Internal:**  
When you create a NumPy array, it allocates a block of memory and stores all elements in a single C array of a fixed type (like float64).

**Array Creation:**

```python
import numpy as np
a = np.array([1, 2, 3])
print(a, type(a))  # ndarray, not list
```

---

## 5. Core Array Creation and Manipulation

### Creating Arrays

```python
np.array([1,2,3])                # From Python list
np.zeros((2,3))                  # 2x3 array of zeros
np.ones(5)                       # 1D array of ones
np.full((3,3), 7)                # 3x3 array of sevens
np.eye(4)                        # 4x4 identity matrix
np.arange(0, 10, 2)              # [0, 2, 4, ..., 8]
np.linspace(0, 1, 5)             # [0. , 0.25, ... , 1. ]
```

### Data Types

```python
np.array([1,2,3], dtype=np.float32)
```

### Reshaping

```python
a = np.arange(12)       # [0..11]
a2 = a.reshape((3,4))   # 3x4 matrix
```

---

## 6. Array Indexing, Slicing, and Iteration

### Indexing

```python
a = np.arange(10)
print(a[2])      # Single element
print(a[-1])     # Last element
```

### Slicing (like Python lists, but faster)

```python
print(a[2:6])    # [2, 3, 4, 5]
print(a[:])      # All elements
print(a[::-1])   # Reverse
```

### Multi-dimensional

```python
m = np.array([[1,2,3],[4,5,6]])
print(m[1,2])        # Row 1, Col 2 (6)
print(m[0])          # First row
print(m[:,1])        # Second column
```

---

## 7. Array Operations: Math, Broadcasting, Vectorization

### Elementwise Math

```python
a = np.array([1,2,3])
b = np.array([10,20,30])
print(a + b)      # [11, 22, 33]
print(a * 2)      # [2, 4, 6]
print(a ** 2)     # [1, 4, 9]
```

### Universal Functions (ufuncs)

```python
np.sqrt(a)        # [1.0, 1.41, 1.73]
np.log(b)         # [2.3, 3.0, 3.4]
```

### Broadcasting

NumPy can "expand" arrays of different shapes for operations.

```python
A = np.ones((3,1))
B = np.arange(3)
print(A + B)      # Shape (3,3): B is "broadcast" across A
```
**Internals:** Broadcasting doesn't copy data; it creates a virtual expanded view, for memory efficiency.

---

## 8. Shape Transformations, Reshaping, Flattening

```python
a = np.arange(6).reshape((2,3))
a.T                    # Transpose
a.flatten()            # 1D copy
a.ravel()              # 1D view (no copy if possible)
np.expand_dims(a, 0)   # Add new axis
```

---

## 9. Random Number Generation

```python
np.random.seed(42)                # For reproducibility
np.random.rand(3,2)               # Uniform [0,1)
np.random.randn(3,2)              # Standard normal
np.random.randint(1, 10, size=5)  # Integers [1,10)
```

---

## 10. Aggregations, Statistics, and Axis Operations

```python
a = np.arange(6).reshape((2,3))
a.sum()                   # Sum all
a.mean(axis=0)            # Mean of each column
a.max(axis=1)             # Max of each row
np.median(a)
np.std(a)
np.percentile(a, 50)
```

---

## 11. Masked Arrays and Boolean Indexing

```python
a = np.array([1,2,3,4,5])
mask = a > 2
print(a[mask])            # [3 4 5]
a[a % 2 == 0] = -1        # Replace even numbers
```

---

## 12. Advanced: Views, Copies, Memory Model

### Views vs Copies

- **Slicing returns a view** (no data copied, changes affect original).
- **Use `.copy()`** to force a real copy.

```python
b = a[1:4]      # View
b[0] = 99
print(a)        # a is changed!

c = a[1:4].copy()
c[0] = 77
print(a)        # a is NOT changed
```

### Memory Layout

- **C-order** (row-major), **F-order** (column-major, Fortran style).
- Useful for interfacing with C/Fortran, optimizing performance.

---

## 13. Performance, Alternatives, and Integration

- **NumPy is FAST:** Uses BLAS, LAPACK, SSE/AVX instructions under the hood.
- **Alternatives:** [CuPy](https://cupy.dev/) (GPU), [JAX](https://github.com/google/jax) (autodiff + GPU), [TensorFlow](https://www.tensorflow.org/) (deep learning).
- **Integration:** NumPy arrays are the data interchange format for pandas, scikit-learn, OpenCV, PIL, etc.
- Use `@` for matrix multiplication (Python 3.5+): `A @ B`.

---

## 14. Common Mistakes, Pro Tips, Interview Angles

### Mistakes

- Confusing lists and arrays (`a[0]` works, but `a[0][1]` fails if 1D).
- Not using `.copy()` when needed—can get data corruption bugs.
- Using Python loops instead of vectorized NumPy ops (much slower).
- Not setting random seed for reproducibility.

### Pro Tips

- Use `np.where` for conditional assignments: `np.where(a > 2, 1, 0)`
- Profile memory and time with `np.info`, `%timeit` in Jupyter.
- Use `dtype` wisely: `float32` for big data, `float64` for precision.
- Prefer broadcasting over manual reshaping.

### Interview Angle

- **Why NumPy over lists?** (memory, speed, vectorization, C backend)
- **Explain broadcasting and shape rules.**
- **How do views/copies affect performance/bugs?**
- **How does NumPy fit into ML stack?** (interoperability, tensor ops)
- **What are alternatives for GPU or large scale?**
- **Show how vectorization replaces loops.**

---

## 15. Extra Insights & References

- **Historical:** NumPy evolved from Numeric/numarray, inspired by Matlab.
- **Source:** [GitHub](https://github.com/numpy/numpy) (review C code for internals)
- **Design Philosophy:** Make scientific computing fast, safe, and expressive.

### Key Docs

- [NumPy User Guide](https://numpy.org/doc/stable/user/)
- [Quickstart Tutorial](https://numpy.org/doc/stable/user/quickstart.html)
- [Broadcasting Rules](https://numpy.org/doc/stable/user/basics.broadcasting.html)

---

## 🧪 End-to-End Example: Data Science Workflow

```python
import numpy as np

# 1. Load data (simulate)
data = np.random.randint(0, 100, (1000, 5))

# 2. Basic stats
print("Mean:", data.mean(axis=0))
print("Std:", data.std(axis=0))

# 3. Mask and filter
mask = data[:,0] > 50
filtered = data[mask]

# 4. Transform
normalized = (filtered - filtered.mean(axis=0)) / filtered.std(axis=0)

# 5. Save/Load
np.save('filtered.npy', filtered)
loaded = np.load('filtered.npy')
```

---

## 💬 TL;DR

- NumPy gives you fast, memory-efficient, C-backed arrays for all numeric work.
- Learn array creation, indexing, math, broadcasting, and advanced memory/model concepts.
- Use vectorized ops for speed; avoid Python loops.
- Master shape, dtype, views/copies, and broadcasting for interviews and production.
- NumPy is the backbone of the Python data stack.

---
