# The Professor's Shift Cipher - Editorial

## Problem Overview
Given two strings `s` and `goal`, we need to determine if `goal` can be obtained by performing any number of left shifts on string `s`. A left shift moves the leftmost character to the rightmost position.

## Understanding the Problem

### Key Components:
1. Original string `s`
2. Target string `goal`
3. Shift operation: moves leftmost character to rightmost position
4. We can perform any number of shifts (0 to n)

### Example Transformation:
```
Original: "abcde"
1 shift:  "bcdea"
2 shifts: "cdeab"
3 shifts: "deabc"
4 shifts: "eabcd"
5 shifts: "abcde" (back to original)
```

## Solution Approach

### Key Observations

1. **Cyclic Nature**:
   - After n shifts (where n is the length of string), we get back the original string
   - All possible shifts form a cycle

2. **String Length**:
   - Both strings must be of equal length for a valid transformation
   - If lengths differ, it's impossible to transform one into another

3. **String Concatenation Property**:
   - All possible shifts of string s are substrings of s + s (excluding the last character)
   - Example: For "abcde", s + s = "abcdeabcde"
   - All shifts are substrings: "abcde", "bcdea", "cdeab", "deabc", "eabcd"

### Algorithm

1. First checks:
   - If lengths are different → return false
   - If strings are identical → return true

2. Main approach:
   - Concatenate s with itself: s + s
   - Check if goal is a substring of s + s
   - This checks all possible shifts in O(n) time

## Implementation

### Python Implementation
```python
def can_shift_string(s: str, goal: str) -> bool:
    if len(s) != len(goal):
        return False
        
    if s == goal:
        return True
        
    doubled = s + s
    return goal in doubled

# input
s = input().strip()
goal = input().strip()
print(str(can_shift_string(s, goal)).lower())
```

### C++ Implementation
```cpp
#include <iostream>
#include <string>
using namespace std;

bool can_shift_string(string s, string goal) {
    // Check if lengths are equal
    if (s.length() != goal.length())
        return false;
        
    // If strings are identical, no shifts needed
    if (s == goal)
        return true;
        
    // Create concatenated string and check if goal is substring
    string doubled = s + s;
    return doubled.find(goal) != string::npos;
}

int main() {
    string s, goal;
    cin >> s >> goal;
    cout << (can_shift_string(s, goal) ? "true" : "false") << endl;
    return 0;
}
```

## Sample Test Cases Analysis

### Sample Case 1
```
Input: 
s = "abcde"
goal = "cdeab"

Process:
1. Lengths match (5 characters)
2. Create "abcdeabcde"
3. "cdeab" is a substring
Output: true
```

### Sample Case 2
```
Input:
s = "abcde"
goal = "abced"

Process:
1. Lengths match (5 characters)
2. Create "abcdeabcde"
3. "abced" is not a substring
Output: false
```

## Edge Cases

1. **Empty Strings**: Not possible due to constraints
2. **Single Character**: Works the same way
3. **Same String**: Should return true immediately
4. **Maximum Length**: Handle strings of length 100

## Time and Space Complexity

- Time Complexity: O(n)
  - String concatenation: O(n)
  - Substring check: O(n)
- Space Complexity: O(n)
  - We create a new string of length 2n