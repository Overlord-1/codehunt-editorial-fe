# Button Game - Editorial

## Problem Overview
Two players, Anna and Katie, play a game with buttons where:
- There are `a` buttons only Anna can press
- There are `b` buttons only Katie can press
- There are `c` buttons either player can press
- Players take turns pressing unPressed buttons
- Anna goes first
- A player loses if they can't press a button on their turn

## Understanding the Game

### Key Components:
1. Each player has exclusive buttons (`a` for Anna, `b` for Katie)
2. Shared buttons (`c`) that either can press
3. Game ends when a player can't make a valid move
4. Both players play optimally

## Solution Approach

### Key Observations

1. **Shared Buttons Matter Most**:
   - The shared buttons (`c`) should be considered first
   - They provide flexibility in strategy

2. **Turn Order is Critical**:
   - Anna goes first
   - Each turn consumes exactly one button
   - Total turns will be `a + b + c`

3. **Winning Strategy**:
   - Players should use shared buttons strategically
   - Need to ensure opponent runs out of moves first

### Mathematical Analysis

Let's analyze what happens in each turn:

1. For Anna to win:
   - She needs enough moves for all her turns
   - Katie must run out of moves

2. Key Calculation:
   - Total game length = `a + b + c`
   - Anna's turns = ⌈(a + b + c)/2⌉
   - Katie's turns = ⌊(a + b + c)/2⌋

3. Winning Condition:
   - Anna wins if she can make all her required moves
   - Katie wins if Anna can't make all her moves

### Algorithm

1. Calculate total turns needed for Anna:
   ```
   anna_turns = (total_buttons + 1) // 2
   ```

2. Calculate buttons available to Anna:
   ```
   anna_available = a + c
   ```

3. If Anna has enough buttons available for her turns, she wins
   Otherwise, Katie wins

## Implementation

### Python Implementation
```python
def solve_button_game(a: int, b: int, c: int) -> str:
    total_buttons = a + b + c
    anna_turns = (total_buttons + 1) // 2
    anna_available = a + c
    return "First" if anna_available >= anna_turns else "Second"

# input
a, b, c = map(int, input().split())
print(solve_button_game(a, b, c))
```

### C++ Implementation
```cpp
#include <iostream>
using namespace std;

string solve_button_game(long long a, long long b, long long c) {
    
    long long total_buttons = a + b + c;
    long long anna_turns = (total_buttons + 1) / 2;
    long long anna_available = a + c;
    return (anna_available >= anna_turns) ? "First" : "Second";
}

int main() {
    long long a, b, c;
    cin >> a >> b >> c;
    cout << solve_button_game(a, b, c) << endl;
    return 0;
}
```

## Sample Test Cases Analysis

### Sample Case 1: a=1, b=1, c=1
- Total buttons = 3
- Anna needs 2 turns ((3+1)//2 = 2)
- Anna has access to 2 buttons (a + c = 1 + 1 = 2)
- Anna can make all her moves, so she wins

### Sample Case 2: a=1, b=2, c=3
- Total buttons = 6
- Anna needs 3 turns ((6+1)//2 = 3)
- Anna has access to 4 buttons (a + c = 1 + 3 = 4)
- Katie wins through optimal play


## Edge Cases

1. **Equal Values**: a = b = c
2. **Zero Values**: Not possible due to constraints
3. **Maximum Values**: Handle large numbers (use long long in C++)

## Time and Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)