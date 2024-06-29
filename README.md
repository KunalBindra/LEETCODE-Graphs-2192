# LEETCODE-Graphs-2192
Let's do a dry run of the provided code for the given input.

### Input
```plaintext
n = 6
edges = [[0,3],[0,4],[1,3],[2,4],[2,5],[4,5]]
```

### Code Breakdown

1. **Initialization:**
   - Create a list `ans` to store the ancestors of each node.
   - Create an array `graph` to represent the adjacency list of the graph.

2. **Graph Construction:**
   - Initialize each entry of `graph` as an empty list.
   - Populate `graph` using the edges.

3. **DFS Traversal:**
   - For each node `i`, perform a DFS traversal to find all its ancestors.

### Step-by-Step Execution

1. **Initialization:**
   ```java
   List<List<Integer>> ans = new ArrayList<>();
   List<Integer>[] graph = new List[n];

   for (int i = 0; i < n; ++i) {
     ans.add(new ArrayList<>());
     graph[i] = new ArrayList<>();
   }
   ```

   - `ans` = `[[], [], [], [], [], []]`
   - `graph` = `[[], [], [], [], [], []]`

2. **Graph Construction:**
   ```java
   for (int[] edge : edges) {
     final int u = edge[0];
     final int v = edge[1];
     graph[u].add(v);
   }
   ```

   - After processing edges:
     - `graph` = `[[3, 4], [3], [4, 5], [], [5], []]`

3. **DFS Traversal:**
   - For each node `i`, perform DFS traversal to find all its ancestors.

   ```java
   for (int i = 0; i < n; ++i)
     dfs(graph, i, i, new boolean[n], ans);
   ```

### Detailed DFS Execution

#### Node 0
- Call `dfs(graph, 0, 0, new boolean[n], ans)`.
  - `seen` = `[true, false, false, false, false, false]`
  - Process neighbor `v = 3`.
    - `ans[3].add(0)` → `ans` = `[[], [], [], [0], [], []]`
    - Call `dfs(graph, 3, 0, [true, false, false, true, false, false], ans)`.
      - No further neighbors for node 3.
  - Process neighbor `v = 4`.
    - `ans[4].add(0)` → `ans` = `[[], [], [], [0], [0], []]`
    - Call `dfs(graph, 4, 0, [true, false, false, true, true, false], ans)`.
      - Process neighbor `v = 5`.
        - `ans[5].add(0)` → `ans` = `[[], [], [], [0], [0], [0]]`
        - Call `dfs(graph, 5, 0, [true, false, false, true, true, true], ans)`.
          - No further neighbors for node 5.

#### Node 1
- Call `dfs(graph, 1, 1, new boolean[n], ans)`.
  - `seen` = `[false, true, false, false, false, false]`
  - Process neighbor `v = 3`.
    - `ans[3].add(1)` → `ans` = `[[], [], [], [0, 1], [0], [0]]`
    - Call `dfs(graph, 3, 1, [false, true, false, true, false, false], ans)`.
      - No further neighbors for node 3.

#### Node 2
- Call `dfs(graph, 2, 2, new boolean[n], ans)`.
  - `seen` = `[false, false, true, false, false, false]`
  - Process neighbor `v = 4`.
    - `ans[4].add(2)` → `ans` = `[[], [], [], [0, 1], [0, 2], [0]]`
    - Call `dfs(graph, 4, 2, [false, false, true, false, true, false], ans)`.
      - Process neighbor `v = 5`.
        - `ans[5].add(2)` → `ans` = `[[], [], [], [0, 1], [0, 2], [0, 2]]`
        - Call `dfs(graph, 5, 2, [false, false, true, false, true, true], ans)`.
          - No further neighbors for node 5.

#### Node 3
- Call `dfs(graph, 3, 3, new boolean[n], ans)`.
  - `seen` = `[false, false, false, true, false, false]`
  - No neighbors for node 3.

#### Node 4
- Call `dfs(graph, 4, 4, new boolean[n], ans)`.
  - `seen` = `[false, false, false, false, true, false]`
  - Process neighbor `v = 5`.
    - `ans[5].add(4)` → `ans` = `[[], [], [], [0, 1], [0, 2], [0, 2, 4]]`
    - Call `dfs(graph, 5, 4, [false, false, false, false, true, true], ans)`.
      - No further neighbors for node 5.

#### Node 5
- Call `dfs(graph, 5, 5, new boolean[n], ans)`.
  - `seen` = `[false, false, false, false, false, true]`
  - No neighbors for node 5.

### Final Output
```plaintext
[[], [], [], [0, 1], [0, 2], [0, 2, 4]]
```

### Summary
The dry run of the algorithm correctly identifies the ancestors of each node in the directed acyclic graph.
