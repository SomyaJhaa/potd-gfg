#  Problem Of The Day Solutions GeeksForGeeks

## Today's 09-01-24 
## (Search Pattern (KMP-Algorithm)(https://www.geeksforgeeks.org/problems/search-pattern0205/1)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The given code is a simple implementation of the Knuth-Morris-Pratt (KMP) algorithm for pattern matching. The algorithm is designed to efficiently find occurrences of a pattern within a text by exploiting the information about the matches that have already been performed.

# Key Ideas:

- Preprocessing (Building LPS Array):

- - The algorithm first preprocesses the pattern to construct the Longest Prefix Suffix (LPS) array. The LPS array is computed using a linear-time algorithm, providing information about the proper prefix which is also a suffix for each prefix of the pattern.
- - The LPS array helps to determine the maximum length of matching proper prefix that is also a suffix for any given position in the pattern.
- Pattern Matching:

- - Once the LPS array is built, the algorithm iterates through the text and the pattern concurrently.
- - At each position in the text, it compares the characters of the pattern with the corresponding characters in the text.
- - If a mismatch occurs, the LPS array is consulted to determine the new position in the pattern where the matching should resume.
- - This avoids unnecessary comparisons and improves the overall efficiency of the pattern matching process.
# Overall Approach:

- The code iterates through the text, maintaining two pointers: i for the text and j for the pattern.
- - When a mismatch occurs, the LPS array guides the algorithm to determine the new starting position in the pattern.
- - The process continues until either a match is found, or the end of the text is reached.


# Complexity
- Time complexity : $O(N + M)$

<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $O(M)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution
{
    public:
        vector <int> search(string pat, string txt)
        {
            vector<int> result;
        int m = pat.size();
        int n = txt.size();
        vector<int> lps(m, 0);

        // Build LPS array
        computeLPS(pat, lps);

        int i = 0; // index for txt
        int j = 0; // index for pat

        while (i < n) {
            if (pat[j] == txt[i]) {
                i++;
                j++;
            }

            if (j == m) {
                result.push_back(i - j + 1);
                j = lps[j - 1];
            } else if (i < n && pat[j] != txt[i]) {
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }

        if (result.empty()) {
            result.push_back(-1);
        }

        return result;
    }

private:
    void computeLPS(string pat, vector<int>& lps) {
        int len = 0; // length of the previous longest prefix suffix

        for (int i = 1; i < pat.size();) {
            if (pat[i] == pat[len]) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        }
     
};

```
