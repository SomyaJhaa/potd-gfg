#  Problem Of The Day Solutions GeeksForGeeks

## Today's 11-01-24 
## [Remove K Digits](https://www.geeksforgeeks.org/problems/remove-k-digits/1)

**Intuition:**
The goal of the problem is to remove K digits from the given string to minimize the resulting number. To achieve this, the code uses a greedy approach. The idea is to maintain a stack of digits while iterating through the string. At each step, if the current digit is smaller than the digit at the top of the stack and there are still remaining removals (K > 0), the top of the stack is popped. This is done to ensure that the resulting number is as small as possible. After processing the entire string, any remaining removals are handled by popping elements from the stack.

Finally, the code constructs the result string by iterating over the elements of the stack (or a vector created from the stack) in reverse order.

**Approach:**
1. Initialize a stack (`s`) to store digits and iterate through each character in the input string `S`.
2. For each character, while the stack is not empty, the current character is smaller than the top of the stack, and there are remaining removals (K > 0), pop elements from the stack and decrement K.
3. Push the current character onto the stack.
4. After processing the entire string, if there are remaining removals, pop elements from the stack.
5. Create a vector (`vec`) to store the elements of the stack in reverse order.
6. Iterate over the vector (`vec`) in reverse order and construct the result string (`min`), ignoring leading zeros.
7. If the resulting number is empty, return "0"; otherwise, return the resulting number.

This approach ensures that the resulting number is minimized by considering smaller digits earlier in the process and handling removals greedily. The stack is used to keep track of the selected digits, and the final result is constructed by iterating over the reversed stack elements.

# Complexity
- Time complexity : $O(N)$
$$n$$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $O(N)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
#include <iostream>
#include <stack>
#include <string>
class Solution {
  public:
    string removeKdigits(string S, int K) {
        if(S.size() <= K) return "0";
        
        stack<char> s;
        for(int i=0; i< S.size(); i++) {
            while(!s.empty() && s.top() > S[i] && K>0) {
                s.pop();
                K--;
            }
            s.push(S[i]);
        }
        while(K-- > 0) s.pop();
        
        vector<char> vec;
        while (!s.empty()) {
            vec.push_back(s.top());
            s.pop();
        }
       string min;
       // Iterate over the vector to construct the result string
        for (auto it = vec.rbegin(); it != vec.rend(); ++it) {
            if (*it == '0' && min.empty()) {
                continue;
            }
            min.push_back(*it);
        }

        // If the resulting number is empty, return "0"
        return min.empty() ? "0" : min;

    }
};

```
