# Optimal Checkpoint Placement Problem

## Problem Overview
In this problem, we need to find the optimal location for a checkpoint `c` between two villages located at positions `a` and `b` such that the total distance traveled `(c - a) + (b - c)` is minimized.

## Understanding the Problem

### Key Components:
1. Two villages at positions `a` and `b` where `a ≤ b`
2. A checkpoint `c` that must be placed between them (`a ≤ c ≤ b`)
3. The objective is to minimize the total distance: `(c - a) + (b - c)`



Given: `a = 7`, `b = 9`
- We need to find `c` where `7 ≤ c ≤ 9`
- The expression `(c - 7) + (9 - c)` needs to be minimized


## Implementation
 - Python
```python
def solve(a, b):
    return b - a
```
 - C++
```c++
#include <iostream>
using namespace std;

int solve(int a, int b) {
    return b - a;
}

int main() {
    int a, b;
    cin >> a >> b;
    cout << solve(a, b) << endl;
    return 0;
}

```

## Sample Test Case

Input: `7 9`
```
b - a = 9 - 7 = 2
```
Output: `2`


## Time and Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)
