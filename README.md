#  Problem Of The Day Solutions GeeksForGeeks

## Today's 28-01-24 
## [Geekina Hate 1s](https://www.geeksforgeeks.org/problems/geekina-hate-1s/1)

## Intuition

The goal is to find the nth number with exactly k set bits in its binary representation. The search space for this problem spans a range from 0 to 10^15.


## Approach

### Binary Search
**Initial Bounds :** 
    Set the initial lower and upper bounds for binary search to 0 and 10^15, respectively.

**Binary Search Loop :** 
    While the lower bound is less than the upper bound, calculated the midpoint and use it to determine the total set bits up to that position.

**Adjust Bounds :** 
    Based on the total set bits, adjusted the bounds to narrow down the search space.

**Result :** 
    The final lower bound represents the nth number with k set bits.

### Total Set Bits Calculation

**Calculated Total Set Bits :** 
    For a given number and a specified maximum set bits count, calculated the total count of set bits up to that position.

**Iterated Over Set Bits Count :** 
    Iterated over set bits count from 0 to the specified maximum and sum up the set bits count at each position.

### Counted Set Bits

**Base Cases :** Handle base cases where set bits count is 0 or the number is 0.

**Highest Bit Position :**  Determined the position of the highest set bit in the binary representation.

**Check Validity :** Checked if there are enough bits to form the required set bits.

**Recursive Calculation :** Calculate the binomial coefficient and continue recursively by flipping the highest set bit.

### Binomial Coefficient

**Calculated Binomial Coefficient:** Calculated the binomial coefficient (n choose r) using the factorial function.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(k * log(10^{15})$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$k$ : maximum set bits count

- Space complexity : $O(k)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 
```
from typing import List
from math import factorial, log2

class Solution:
    def findNthNumber(self, n: int, k: int) -> int:
        # Set the initial lower and upper bounds for binary search
        lower_limit, upper_limit = 0, 10**15
        
        # Performing binary search to find the nth number with k set bits
        result = self.binary_search(lower_limit, upper_limit, n, k)
        
        # Returning the result
        return result

    def binary_search(self, lower_limit, upper_limit, n, k):
        # Binary search loop
        while lower_limit < upper_limit:
            mid_point = lower_limit + (upper_limit - lower_limit) // 2
            total_set_bits = self.calculate_total_set_bits(mid_point, k)

            # Adjusting bounds based on the total set bits
            if total_set_bits >= n:
                upper_limit = mid_point
            else:
                lower_limit = mid_point + 1

        # Returning the final result
        return lower_limit

    def calculate_total_set_bits(self, number, max_set_bits_count):
        # Calculating the total count of set bits up to a specified position
        return sum(self.count_set_bits(number, i) for i in range(max_set_bits_count + 1))

    def count_set_bits(self, number, set_bits_count):
        # Recursive function to count set bits in a binary representation
        if set_bits_count == 0:
            return 1
        if number == 0:
            return 0

        highest_bit_position = int(log2(number))
        
        # Checking if there are enough bits to form the required set bits
        if highest_bit_position < set_bits_count - 1:
            return 0

        # Calculating binomial coefficient and continue recursively
        return self.binomial_coefficient(highest_bit_position, set_bits_count) + self.count_set_bits(number ^ (1 << highest_bit_position), set_bits_count - 1)

    def binomial_coefficient(self, n, r):
        # Calculating binomial coefficient (n choose r)
        return factorial(n) // (factorial(r) * factorial(n - r)) if n >= r else 0
```

