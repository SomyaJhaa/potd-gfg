#  Problem Of The Day Solutions GeeksForGeeks

## Today's 19-01-24 
## [Top k numbers in a stream](https://www.geeksforgeeks.org/problems/top-k-numbers3425/1)

### Intuition
My code aims to find the top K elements based on their frequency at each iteration while traversing an input array. I used a combination of an array (`jada`) and a HashMap (`m`) to efficiently keep track of the current top K elements and their frequencies.

### Approach

- Initialized an array (`jada`) with an extra slot to hold the current element at the last position. Also, created a HashMap (`m`) to store the frequency of each element.
- Iterated over the input array, updating the last slot of `jada` with the current element and updating its frequency in the HashMap (`m`).
- Found the position of the current element in `jada` and moved it to its correct position based on its frequency. This ensured that `jada` maintains the top K elements at all times.
- Populated a new array with the current top K elements and add it to the result array.
- Repeated the last three steps steps for each element in the input array.
- The final result array contained sub-arrays representing the top K elements at each iteration.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(N*K)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N$ : length of the input array

$K$ : given
- Space complexity : $O(K)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code
```
import java.util.*;

class Solution {
    
    // Function to determine the top K elements based on frequency at each iteration
    
    public static ArrayList<ArrayList<Integer>> kTop(int[] arr, int N, int K) {
        // Resultant array of arrays to store the top K elements at each iteration
        ArrayList<ArrayList<Integer>> result = new ArrayList<>();

        // Array to maintain the current top K elements along with an extra slot
        int[] jada = new int[K + 1];

        // HashMap to store the frequency of each element
        HashMap<Integer, Integer> m = new HashMap<>();

        // Initializing the frequency map with zeros for each element from 0 to K
        for (int i = 0; i <= K; i++) {
            m.put(i, 0);
        }

        // Iterating over the input array
        for (int i = 0; i < arr.length; i++) {
            // Update the last slot of jada with the current element
            jada[K] = arr[i];

            // Updating the frequency map for the current element
            if (m.containsKey(arr[i])) {
                m.put(arr[i], m.get(arr[i]) + 1);
            } else {
                m.put(arr[i], 1);
            }

            // Finding the position of the current element in jada
            int in = -1;
            for (int j = 0; j < jada.length; j++) {
                if (jada[j] == arr[i]) {
                    in = j;
                    break;
                }
            }
            in--;

            // Moving the current element to its correct position in jada based on frequency
            while (in >= 0) {
                if (m.get(jada[in]) < m.get(jada[in + 1])) {
                    int t = jada[in];
                    jada[in] = jada[in + 1];
                    jada[in + 1] = t;
                } else if ((jada[in] > jada[in + 1]) && (m.get(jada[in]) == m.get(jada[in + 1]))) {
                    int t = jada[in];
                    jada[in] = jada[in + 1];
                    jada[in + 1] = t;
                } else {
                    break;
                }
                in--;
            }

            // Populating the current array with the top K elements and add it to the result
            ArrayList<Integer> aa = new ArrayList<>();
            for (int e = 0; e < K && jada[e] != 0; e++) {
                aa.add(jada[e]);
            }
            result.add(aa);
        }

        // Returning the final result
        return result;
    }
}

```

