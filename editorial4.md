# Lena's Binary String Operations - Editorial

## Problem Overview
Given a binary string, we need to count the maximum number of possible operations where each operation involves moving a '1' to the right until it hits another '1' or reaches the end of the string. The operation can only be performed if we find a '10' pattern in the string.

## Understanding the Problem

### Key Components:
1. Binary string input
2. Operation rules:
   - Need adjacent '1' and '0' (pattern "10")
   - '1' moves right until hitting another '1' or string end
3. Need to find maximum possible operations

### Example Analysis:
```
Original: "1001101"
Step 1:   "0011101" (moved 1 from index 0)
Step 2:   "0011011" (moved 1 from index 4)
Step 3:   "0010111" (moved 1 from index 3)
Step 4:   "0001111" (moved 1 from index 2)
```

## Solution Approach

### Algorithm

1. First Check:
   - If string length < 2, return 0
   - If no "10" pattern exists, return 0

2. Main approach:
   - Convert string to list for easier manipulation
   - Find rightmost "10" pattern
   - Move '1' to rightmost possible position
   - Count operation
   - Repeat until no more moves possible

## Implementation

### Python Implementation
```python
def max_operations(s: str) -> int:
    # Convert to list for easier manipulation
    s = list(s)
    n = len(s)
    operations = 0
    
    # Continue while we can find valid moves
    while True:
        found_move = False
        
        # Search from right to left for "10" pattern
        for i in range(n-2, -1, -1):
            if s[i] == '1' and s[i+1] == '0':
                # Find rightmost position to move the '1'
                j = i + 1
                while j < n-1 and s[j+1] == '0':
                    j += 1
                    
                # Perform the move
                s[i] = '0'
                s[j] = '1'
                operations += 1
                found_move = True
                break
                
        if not found_move:
            break
            
    return operations

# Handle input
s = input().strip()
print(max_operations(s))
```

### C++ Implementation
```cpp
#include <iostream>
#include <string>
using namespace std;

int max_operations(string s) {
    int n = s.length();
    int operations = 0;
    
    while (true) {
        bool found_move = false;
        
        // Search from right to left for "10" pattern
        for (int i = n-2; i >= 0; i--) {
            if (s[i] == '1' && s[i+1] == '0') {
                // Find rightmost position to move the '1'
                int j = i + 1;
                while (j < n-1 && s[j+1] == '0') {
                    j++;
                }
                
                // Perform the move
                s[i] = '0';
                s[j] = '1';
                operations++;
                found_move = true;
                break;
            }
        }
        
        if (!found_move) break;
    }
    
    return operations;
}

int main() {
    string s;
    cin >> s;
    cout << max_operations(s) << endl;
    return 0;
}
```

## Sample Test Cases Analysis

### Sample Case 1: "1001101"
```
Initial:  1001101
Step 1:   0011101 (move index 0)
Step 2:   0011011 (move index 4)
Step 3:   0010111 (move index 3)
Step 4:   0001111 (move index 2)
Result: 4 operations
```

### Sample Case 2: "00111"
```
Initial:  00111
No "10" patterns found
Result: 0 operations
```

## Edge Cases

1. **Single Character**: Return 0
2. **All Zeros**: Return 0
3. **All Ones**: Return 0
4. **Alternating 10**: Handle multiple moves
5. **Maximum Length**: Handle strings of length 10^5

## Time and Space Complexity

- Time Complexity: O(n²)
  - Each operation can require scanning most of string
  - Maximum n/2 operations possible
- Space Complexity: O(n)
  - We store the string as character array