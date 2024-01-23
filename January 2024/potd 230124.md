# Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 23-01-24 [Problem Link](https://www.geeksforgeeks.org/problems/course-schedule/1)
## Course Schedule

## Intuition
As this problem is about finding the order in which courses can be taken given a list of prerequisites, it is essentially a topological sorting problem.

My idea is to represent the courses as nodes in a graph, and the prerequisites as directed edges between the nodes, as the problem asks for an order in which we can take the courses, considering the prerequisites.

## Approach

**Initialized Data Structures :**
- Declared arrays and data structures for in-degrees (`in`), the final answer (`jawab`), an adjacency list (`al`), and a queue (`q`).
   
**Built Graph :**
- Created an adjacency list representing the directed edges between courses based on prerequisites.
- Calculated the in-degree of each course, i.e., the number of prerequisites it has.

**Initialized Queue :**
- Added courses with in-degree 0 to the queue initially.

**BFS Topological Sort :**
- Processed the courses in a Breadth-First Search (BFS) manner:
  - Poll a course from the queue.
  - Added the course to the answer (`jawab`).
  - Updated the in-degrees of its neighbors and add them to the queue if their in-degree becomes 0.

**Checked for Valid Order :**
- After processing all courses, checked if all courses have in-degree 0. If not, return an empty array since a valid order is not possible.

**Returned Result:**
- Returned the final answer (`jawab`) representing the order in which courses can be taken.

The BFS ensures that I processed courses with no prerequisites first, gradually moving to courses with all prerequisites satisfied. If a valid topological order exists, I returned it; otherwise, it returned an empty array.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(m + n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of courses

$m$ : number of prerequisites

- Space complexity : $O(m + n)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 
```
//User function Template for Java

class Solution
{
    // Declaring static arrays and data structures
    static int[] in;
    static int[] jawab;
    static ArrayList<ArrayList<Integer>> al;
    static Queue<Integer> q;
    
    static int[] findOrder(int n, int m, ArrayList<ArrayList<Integer>> prerequisites) {
        
        // Initializing in-degree array, adjacency list, and queue
        in = new int[n];
        al = new ArrayList<>();
        for( int i = 0; i < n; i++){
            al.add(new ArrayList<>());
        }
        
        // Populating adjacency list and in-degree array based on prerequisites
        for(ArrayList<Integer> a : prerequisites){
            al.get(a.get(1)).add(a.get(0));
            in[a.get(0)]++;
        }
        
        // Initializing queue with courses having in-degree 0
        q = new LinkedList<>();
        for(int i = 0; i < n; i++){
            if(in[i] == 0){
                q.add(i);
            }
        }
        
        // If no courses have in-degree 0, returning an empty array
        if(q.isEmpty()){
            return new int[0];
        }
        
        int t = 0;
        jawab = new int[n];
        
        // Processing courses in topological order using BFS
        while(!q.isEmpty()){
            int p = q.poll();
            jawab[t++] = p;
            for(int aaspass : al.get(p)){
                in[aaspass]--;
                if(in[aaspass] == 0){
                    q.add(aaspass);
                }
            }
        }
        
        // Checking if all courses have been processed
        for(int i = 0; i < n; i++){
            if(in[i] != 0){
                return new int[0];
            }
        }
        return jawab;
    }
}

```

