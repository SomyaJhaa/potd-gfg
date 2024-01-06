#  Problem Of The Day Solutions GeeksForGeeks

## Today's 06-01-24 
## [Techfest and the Queue](https://www.geeksforgeeks.org/problems/techfest-and-the-queue1044/1)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The sumOfPowers function aims to calculate the sum of powers of prime factors for numbers in the range [a, b] (inclusive). It does so by iterating through each number in the range and using the sumPrimePowers helper function to calculate the sum of powers for each individual number. The sumPrimePowers function, in turn, uses the primeFactorization helper function to find the prime factorization of a given number and then calculates the sum of powers from its prime factors.

# Approach
<!-- Describe your approach to solving the problem. -->
- The code aims to find the sum of powers of prime factors for numbers in the range [a, b] (inclusive). It achieves this by breaking down the problem into three main functions: sumOfPowers, sumPrimePowers, and primeFactorization.

- sumPrimePowers Function:

- - The function sumPrimePowers takes an integer number as input and calculates the sum of powers of its prime factors.
- - It utilizes the primeFactorization function to obtain the prime factorization of the given number.
- - For each prime factor in the factorization, it adds the power of the prime to the total sum.
- - Returns the computed sum.

- primeFactorization Function:

- - The function primeFactorization takes an integer n as input and returns a map containing the prime factors and their corresponding powers.
- - It uses a divisor-based approach to find the prime factorization of the given number.
- - The algorithm iterates through potential divisors starting from 2 and checks how many times the number is divisible by the current divisor.
- - It updates the count of the divisor in the map if it is divisible.
Continues until the number becomes 1.
- - Returns the map of prime factors and their powers.

- sumOfPowers Function:

- - The function sumOfPowers takes two integers a and b representing the range [a, b].
- - It iterates through each number in the range and calculates the sum of powers of prime factors using the sumPrimePowers function.
- - Accumulates the sums for all numbers in the range.
- - Returns the total sum.


# Complexity
- Time complexity : $$O((b - a + 1) * log(b))$$
$$n$$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $$O(log(b))$$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution {
public:
	long sumOfPowers(int a, int b) {
        long sum = 0;
        for (int i = a; i <= b; i++) {
            sum += sumPrimePowers(i);
        }
        return sum;
    }

private:
    unordered_map<int, int> primeFactorization(int n) {
        unordered_map<int, int> factors;
        int divisor = 2;

        while (n > 1) {
            int count = 0;
            while (n % divisor == 0) {
                n /= divisor;
                count++;
            }

            if (count > 0) {
                factors[divisor] = count;
            }

            divisor++;
            if (divisor * divisor > n && n > 1) {
                factors[n] = 1;
                break;
            }
        }

        return factors;
    }

    long sumPrimePowers(int number) {
        long sum = 0;
        auto primeFactors = primeFactorization(number);

        for (auto& entry : primeFactors) {
            sum += entry.second;
        }

        return sum;
    }
};
```
