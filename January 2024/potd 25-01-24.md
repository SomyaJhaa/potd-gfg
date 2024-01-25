#  Problem Of The Day Solutions GeeksForGeeks

## Today's 25-01-24 
## [Shortest Prime Path](https://www.geeksforgeeks.org/problems/shortest-prime-path--141631/1)

## Intuition

The goal of this problem is to find the minimum number of flips required to transform one given number (Num1) into another (Num2). A flip is defined as changing one digit at a time.


## Approach

- If Num1 is already equal to Num2, no flips are needed, and the answer is 0.

- Used Breadth-First Search (BFS) to explore all possible transformations:
    - Started with Num1 and enqueue it in the BFS queue.
    - Maintained a set (`visitedNumStrings`) to track previously visited prime numbers to avoid cycles.
    - For each number popped from the queue, try changing each digit to every possible digit from '0' to '9', excluding the current digit and avoiding leading zeros.
    - If the changed number becomes equal to Num2, returned the number of flips.
    - If the changed number is prime, enqueue it for further exploration in the BFS.

- If no transformation is possible, returned -1.

My BFS traversal ensures that the algorithm explores all possible transformations in the minimum number of flips, and the isPrime function is used to check if a number is prime.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(V * sqrt(N))$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N$ : maximum value of the input number

$V$ :  total number of possible transformations of the input number `Num1`. 

In the worst case, the BFS explores all valid transformations, which can be at most 10^D (since each digit can be changed to any digit from '0' to '9'). Then, $V$ = $10^D$, Were D is the number of digits in the input number 

- Space complexity : $O(V)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 
```
//User function Template for Java

class Solution {
    
    // Function to find the minimum number of flips required to transform Num1 to Num2
    int solve(int Num1, int Num2) {
        // If Num1 is already equal to Num2, no flips are needed
        if (Num1 == Num2) return 0;

        // Initializing a queue for BFS traversal
        Queue<Integer> queue = new LinkedList<>();
        queue.add(Num1);

        // Set to track visited number strings to avoid cycles
        Set<String> visitedNumStrings = new HashSet<>();

        // Variable to track the number of flips
        int flips = 0;

        // Performing BFS traversal
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size != 0) {
                int poppedNum = queue.remove();
                size--;

                String startNumString = String.valueOf(poppedNum);

                // Skipping if the number string is already visited
                if (!visitedNumStrings.add(startNumString.toString())) continue;

                // Iterating over each digit in the number string
                for (int i = 0; i < 4; i++) {
                    StringBuffer currString = new StringBuffer(startNumString);
                    // Trying to change the digit to every possible digit from '0' to '9'
                    for (char c = '0'; c <= '9'; c++) {
                        // Skipping if the digit doesn't change or the first digit becomes '0'
                        if (currString.charAt(i) == c || (i == 0 && c == '0')) {
                            continue;
                        }
                        currString.setCharAt(i, c);
                        int changedNum = Integer.parseInt(currString.toString());

                        // If the changed number becomes Num2, returning the number of flips
                        if (changedNum == Num2) {
                            return flips + 1;
                        }

                        // If the changed number is prime, adding it to the queue for further exploration
                        if (isPrime(changedNum)) {
                            queue.offer(changedNum);
                        }
                    }
                }
            }
            flips++; // Incrementing flips per level in BFS
        }

        // If no transformation is possible, returning -1
        return -1;
    }

    // Function to check if a number is prime
    static boolean isPrime(int num) {
        if (num <= 1) return false;

        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) return false;
        }

        return true;
    }
}

```
