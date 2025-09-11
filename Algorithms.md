# Algorithms - Comprehensive Python Reference

## 1. Searching Algorithms

### 1.1 Linear Search
*Time Complexity*: O(n)  
*Space Complexity*: O(1)

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i  
    return -1  
```

### 1.2 Binary Search
*Time Complexity*: O(log n)  
*Space Complexity*: O(1)  
*Prerequisite*: Array must be sorted

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```
#### Recursive version
```python

def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

```

---

## 2. Sorting Algorithms

### 2.1 Bubble Sort
*Time Complexity*: O(n²)  
*Space Complexity*: O(1)

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:  
            break
    return arr
```

### 2.2 Selection Sort
*Time Complexity*: O(n²)  
*Space Complexity*: O(1)

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

### 2.3 Insertion Sort
*Time Complexity*: O(n²)  
*Space Complexity*: O(1)

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr
```

### 2.4 Quick Sort
*Time Complexity*: O(n log n) average, O(n²) worst  
*Space Complexity*: O(log n)

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quick_sort(left) + middle + quick_sort(right)
```

#### In-place version
``` python
def quick_sort_inplace(arr, low=0, high=None):
    if high is None:
        high = len(arr) - 1
    
    if low < high:
        pi = partition(arr, low, high)
        quick_sort_inplace(arr, low, pi - 1)
        quick_sort_inplace(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### 2.5 Merge Sort
*Time Complexity*: O(n log n)  
*Space Complexity*: O(n)

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### 2.6 Heap Sort
*Time Complexity*: O(n log n)  
*Space Complexity*: O(1)

```python
def heap_sort(arr):
    n = len(arr)
    
    
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
    
    
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)
    
    return arr

def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2
    
    if left < n and arr[left] > arr[largest]:
        largest = left
    
    if right < n and arr[right] > arr[largest]:
        largest = right
    
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
```


---

## 3. Graph Algorithms

### 3.1 Depth-First Search (DFS)
*Time Complexity*: O(V + E)  
*Space Complexity*: O(V)

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    
    visited.add(start)
    print(start, end=' ')
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
    
    return visited
```
#### Iterative version
```python
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    
    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            print(node, end=' ')
            stack.extend(reversed(graph[node]))  
    
    return visited
```

### 3.2 Breadth-First Search (BFS)
*Time Complexity*: O(V + E)  
*Space Complexity*: O(V)

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)
    
    while queue:
        node = queue.popleft()
        print(node, end=' ')
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    
    return visited
```

### 3.3 Dijkstra's Algorithm
*Time Complexity*: O((V + E) log V)  
*Space Complexity*: O(V)

```python
import heapq

def dijkstra(graph, start):
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    pq = [(0, start)]
    visited = set()
    
    while pq:
        current_dist, current_node = heapq.heappop(pq)
        
        if current_node in visited:
            continue
        
        visited.add(current_node)
        
        for neighbor, weight in graph[current_node].items():
            distance = current_dist + weight
            
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))
    
    return distances
```

### 3.4 Floyd-Warshall Algorithm
*Time Complexity*: O(V³)  
*Space Complexity*: O(V²)

```python
def floyd_warshall(graph):
    nodes = list(graph.keys())
    n = len(nodes)
    
    # Initialize distance matrix
    dist = [[float('inf')] * n for _ in range(n)]
    
    # Set distance from node to itself as 0
    for i in range(n):
        dist[i][i] = 0
    
    # Fill initial distances
    for i, node1 in enumerate(nodes):
        for j, node2 in enumerate(nodes):
            if node2 in graph[node1]:
                dist[i][j] = graph[node1][node2]
    
    # Floyd-Warshall algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
    
    return dist, nodes
```

### 3.5 Bellman-Ford Algorithm
*Time Complexity*: O(VE)  
*Space Complexity*: O(V)

```python
def bellman_ford(graph, start):
    # Initialize distances
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    
    # Get all edges
    edges = []
    for u in graph:
        for v, weight in graph[u].items():
            edges.append((u, v, weight))
    
    # Relax edges V-1 times
    for _ in range(len(graph) - 1):
        for u, v, weight in edges:
            if distances[u] != float('inf') and distances[u] + weight < distances[v]:
                distances[v] = distances[u] + weight
    
    # Check for negative cycles
    for u, v, weight in edges:
        if distances[u] != float('inf') and distances[u] + weight < distances[v]:
            return None  # Negative cycle detected
    
    return distances
```

### 3.6 Topological Sort
*Time Complexity*: O(V + E)  
*Space Complexity*: O(V)

```python
def topological_sort_dfs(graph):
    visited = set()
    stack = []
    
    def dfs_util(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs_util(neighbor)
        stack.append(node)
    
    for node in graph:
        if node not in visited:
            dfs_util(node)
    
    return stack[::-1]  # Reverse to get correct order

# Kahn's Algorithm (using in-degree)
def topological_sort_kahn(graph):
    in_degree = {node: 0 for node in graph}
    
    # Calculate in-degrees
    for node in graph:
        for neighbor in graph[node]:
            in_degree[neighbor] += 1
    
    # Find nodes with no incoming edges
    queue = deque([node for node in in_degree if in_degree[node] == 0])
    result = []
    
    while queue:
        node = queue.popleft()
        result.append(node)
        
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    return result if len(result) == len(graph) else []  # Check for cycles
```

### 3.7 Minimum Spanning Tree - Kruskal's Algorithm
*Time Complexity*: O(E log E)  
*Space Complexity*: O(V)

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    
    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True

def kruskal_mst(n, edges):
    # edges: [(weight, u, v), ...]
    edges.sort()  # Sort by weight
    uf = UnionFind(n)
    mst = []
    total_weight = 0
    
    for weight, u, v in edges:
        if uf.union(u, v):
            mst.append((u, v, weight))
            total_weight += weight
            if len(mst) == n - 1:
                break
    
    return mst, total_weight
```

### 3.8 Minimum Spanning Tree - Prim's Algorithm
*Time Complexity*: O(E log V)  
*Space Complexity*: O(V)

```python
def prim_mst(graph):
    if not graph:
        return [], 0
    
    start = next(iter(graph))
    mst = []
    visited = {start}
    total_weight = 0
    
    # Priority queue: (weight, u, v)
    edges = [(weight, start, neighbor) for neighbor, weight in graph[start].items()]
    heapq.heapify(edges)
    
    while edges and len(visited) < len(graph):
        weight, u, v = heapq.heappop(edges)
        
        if v in visited:
            continue
        
        visited.add(v)
        mst.append((u, v, weight))
        total_weight += weight
        
        # Add new edges from v
        for neighbor, edge_weight in graph[v].items():
            if neighbor not in visited:
                heapq.heappush(edges, (edge_weight, v, neighbor))
    
    return mst, total_weight
```

---

## 4. Dynamic Programming

### 4.1 Fibonacci Sequence
*Time Complexity*: O(n)  
*Space Complexity*: O(n) for memoization, O(1) for bottom-up

```python
# Memoization: Top-down
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    return memo[n]

# Tabulation: Bottom-up
def fibonacci_tab(n):
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

# Space optimized
def fibonacci_optimized(n):
    if n <= 1:
        return n
    
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    
    return b
```

### 4.2 Longest Common Subsequence (LCS)
*Time Complexity*: O(mn)  
*Space Complexity*: O(mn)

```python
def lcs(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]

# Space optimized version
def lcs_optimized(text1, text2):
    m, n = len(text1), len(text2)
    prev = [0] * (n + 1)
    curr = [0] * (n + 1)
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                curr[j] = prev[j-1] + 1
            else:
                curr[j] = max(prev[j], curr[j-1])
        prev, curr = curr, prev
    
    return prev[n]
```

### 4.3 Knapsack Problem (0/1)
*Time Complexity*: O(nW)  
*Space Complexity*: O(nW)

```python
def knapsack_01(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        for w in range(1, capacity + 1):
            if weights[i-1] <= w:
                dp[i][w] = max(
                    dp[i-1][w],  # Don't take item
                    dp[i-1][w - weights[i-1]] + values[i-1]  # Take item
                )
            else:
                dp[i][w] = dp[i-1][w]
    
    return dp[n][capacity]

# Space optimized version
def knapsack_01_optimized(weights, values, capacity):
    dp = [0] * (capacity + 1)
    
    for i in range(len(weights)):
        for w in range(capacity, weights[i] - 1, -1):
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])
    
    return dp[capacity]
```

### 4.4 Longest Increasing Subsequence (LIS)
*Time Complexity*: O(n²) for DP, O(n log n) for binary search  
*Space Complexity*: O(n)

```python
# DP approach
def lis_dp(nums):
    if not nums:
        return 0
    
    n = len(nums)
    dp = [1] * n
    
    for i in range(1, n):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)
    
    return max(dp)

# Binary search approach (more efficient)
def lis_binary_search(nums):
    if not nums:
        return 0
    
    tails = []
    
    for num in nums:
        left, right = 0, len(tails)
        while left < right:
            mid = (left + right) // 2
            if tails[mid] < num:
                left = mid + 1
            else:
                right = mid
        
        if left == len(tails):
            tails.append(num)
        else:
            tails[left] = num
    
    return len(tails)
```

### 4.5 Edit Distance (Levenshtein Distance)
*Time Complexity*: O(mn)  
*Space Complexity*: O(mn)

```python
def edit_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    # Initialize base cases
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j],      # deletion
                    dp[i][j-1],      # insertion
                    dp[i-1][j-1]     # substitution
                )
    
    return dp[m][n]
```

### 4.6 Coin Change Problem
*Time Complexity*: O(amount × coins)  
*Space Complexity*: O(amount)

```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    
    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] != float('inf') else -1

# Count ways to make change
def coin_change_ways(coins, amount):
    dp = [0] * (amount + 1)
    dp[0] = 1
    
    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] += dp[i - coin]
    
    return dp[amount]
```

---

## 5. Tree Algorithms

### 5.1 Binary Tree Traversals

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Inorder (Left, Root, Right)
def inorder_traversal(root):
    result = []
    if root:
        result.extend(inorder_traversal(root.left))
        result.append(root.val)
        result.extend(inorder_traversal(root.right))
    return result

# Preorder (Root, Left, Right)
def preorder_traversal(root):
    result = []
    if root:
        result.append(root.val)
        result.extend(preorder_traversal(root.left))
        result.extend(preorder_traversal(root.right))
    return result

# Postorder (Left, Right, Root)
def postorder_traversal(root):
    result = []
    if root:
        result.extend(postorder_traversal(root.left))
        result.extend(postorder_traversal(root.right))
        result.append(root.val)
    return result

# Level Order (BFS)
def level_order_traversal(root):
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        result.append(node.val)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    
    return result

# Iterative Inorder
def inorder_iterative(root):
    result = []
    stack = []
    current = root
    
    while stack or current:
        while current:
            stack.append(current)
            current = current.left
        
        current = stack.pop()
        result.append(current.val)
        current = current.right
    
    return result
```

### 5.2 Binary Search Tree Operations

```python
class BST:
    def __init__(self):
        self.root = None
    
    def insert(self, val):
        self.root = self._insert_recursive(self.root, val)
    
    def _insert_recursive(self, node, val):
        if not node:
            return TreeNode(val)
        
        if val < node.val:
            node.left = self._insert_recursive(node.left, val)
        else:
            node.right = self._insert_recursive(node.right, val)
        
        return node
    
    def search(self, val):
        return self._search_recursive(self.root, val)
    
    def _search_recursive(self, node, val):
        if not node or node.val == val:
            return node
        
        if val < node.val:
            return self._search_recursive(node.left, val)
        return self._search_recursive(node.right, val)
    
    def delete(self, val):
        self.root = self._delete_recursive(self.root, val)
    
    def _delete_recursive(self, node, val):
        if not node:
            return node
        
        if val < node.val:
            node.left = self._delete_recursive(node.left, val)
        elif val > node.val:
            node.right = self._delete_recursive(node.right, val)
        else:
            # Node to be deleted found
            if not node.left:
                return node.right
            elif not node.right:
                return node.left
            
            # Node has two children
            min_larger_node = self._find_min(node.right)
            node.val = min_larger_node.val
            node.right = self._delete_recursive(node.right, min_larger_node.val)
        
        return node
    
    def _find_min(self, node):
        while node.left:
            node = node.left
        return node
```

### 5.3 Tree Height and Diameter

```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))

def diameter_of_tree(root):
    def helper(node):
        if not node:
            return 0, 0  # (height, diameter)
        
        left_height, left_diameter = helper(node.left)
        right_height, right_diameter = helper(node.right)
        
        current_height = 1 + max(left_height, right_height)
        current_diameter = max(
            left_diameter,
            right_diameter,
            left_height + right_height
        )
        
        return current_height, current_diameter
    
    return helper(root)[1]
```

### 5.4 Lowest Common Ancestor (LCA)

```python
def lca_binary_tree(root, p, q):
    if not root or root == p or root == q:
        return root
    
    left = lca_binary_tree(root.left, p, q)
    right = lca_binary_tree(root.right, p, q)
    
    if left and right:
        return root
    return left if left else right

def lca_bst(root, p, q):
    if not root:
        return None
    
    if p.val < root.val and q.val < root.val:
        return lca_bst(root.left, p, q)
    elif p.val > root.val and q.val > root.val:
        return lca_bst(root.right, p, q)
    else:
        return root
```
### 5.5 Check if Balanced Tree
```python
def is_balanced(root):
    def check(node):
        if not node:
            return 0, True
        left_height, left_bal = check(node.left)
        right_height, right_bal = check(node.right)
        balanced = left_bal and right_bal and abs(left_height - right_height) <= 1
        return 1 + max(left_height, right_height), balanced
    
    return check(root)[1]
```
### 5.6 Maximum Path Sum in Binary Tree
```python
def max_path_sum(root):
    max_sum = float('-inf')
    
    def helper(node):
        nonlocal max_sum
        if not node:
            return 0
        left = max(helper(node.left), 0)
        right = max(helper(node.right), 0)
        max_sum = max(max_sum, node.val + left + right)
        return node.val + max(left, right)
    
    helper(root)
    return max_sum
```
### 5.7 Serialize and Deserialize Binary Tree
```python
class Codec:
    def serialize(self, root):
        if not root:
            return "N"
        return f"{root.val},{self.serialize(root.left)},{self.serialize(root.right)}"
    
    def deserialize(self, data):
        values = iter(data.split(","))
        
        def build():
            val = next(values)
            if val == "N":
                return None
            node = TreeNode(int(val))
            node.left = build()
            node.right = build()
            return node
        
        return build()
```
---

## 6 Greedy Algorithm

### 6.1  Activity Selection Problem
``` python
def activity_selection(activities):
    activities.sort(key=lambda x: x[1])  # sort by finish time
    result = [activities[0]]
    last_finish = activities[0][1]
    
    for start, finish in activities[1:]:
        if start >= last_finish:
            result.append((start, finish))
            last_finish = finish
    
    return result
```
### 6.2 Huffman Coding
``` python
import heapq

class HuffmanNode:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None
    
    def __lt__(self, other):
        return self.freq < other.freq

def huffman_encoding(chars, freqs):
    heap = [HuffmanNode(c, f) for c, f in zip(chars, freqs)]
    heapq.heapify(heap)
    
    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        merged = HuffmanNode(None, left.freq + right.freq)
        merged.left = left
        merged.right = right
        heapq.heappush(heap, merged)
    
    root = heap[0]
    codes = {}
    
    def build_codes(node, code=""):
        if node:
            if node.char:
                codes[node.char] = code
            build_codes(node.left, code + "0")
            build_codes(node.right, code + "1")
    
    build_codes(root)
    return codes
```
### 6.3 Fractional Knapsack
``` python
def fractional_knapsack(weights, values, capacity):
    items = sorted(zip(weights, values), key=lambda x: x[1]/x[0], reverse=True)
    total_value = 0
    
    for w, v in items:
        if capacity >= w:
            capacity -= w
            total_value += v
        else:
            total_value += v * (capacity / w)
            break
    
    return total_value
```
--- 

## 7. Backtracking Algorithms
### 7.1  N-Queens Problem
``` python
def solve_n_queens(n):
    board = [["."] * n for _ in range(n)]
    solutions = []
    
    def is_safe(row, col):
        for r in range(row):
            if board[r][col] == "Q":
                return False
            if col - (row - r) >= 0 and board[r][col - (row - r)] == "Q":
                return False
            if col + (row - r) < n and board[r][col + (row - r)] == "Q":
                return False
        return True
    
    def backtrack(row):
        if row == n:
            solutions.append(["".join(r) for r in board])
            return
        for col in range(n):
            if is_safe(row, col):
                board[row][col] = "Q"
                backtrack(row + 1)
                board[row][col] = "."
    
    backtrack(0)
    return solutions
```
### 7.2 Sudoku Solver
``` python
def solve_sudoku(board):
    def is_valid(r, c, num):
        for i in range(9):
            if board[r][i] == num or board[i][c] == num:
                return False
        start_r, start_c = 3 * (r // 3), 3 * (c // 3)
        for i in range(start_r, start_r + 3):
            for j in range(start_c, start_c + 3):
                if board[i][j] == num:
                    return False
        return True
    
    def solve():
        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    for num in map(str, range(1, 10)):
                        if is_valid(r, c, num):
                            board[r][c] = num
                            if solve():
                                return True
                            board[r][c] = "."
                    return False
        return True
    
    solve()
    return board
```
### 7.3 Rat in a Maze
``` python
def rat_in_maze(maze):
    n = len(maze)
    path = []
    
    def solve(x, y):
        if x == n-1 and y == n-1 and maze[x][y] == 1:
            path.append((x, y))
            return True
        
        if 0 <= x < n and 0 <= y < n and maze[x][y] == 1:
            path.append((x, y))
            maze[x][y] = -1  # mark visited
            
            if solve(x+1, y) or solve(x, y+1) or solve(x-1, y) or solve(x, y-1):
                return True
            
            path.pop()
            maze[x][y] = 1
        return False
    
    if solve(0, 0):
        return path
    return []
```


## 8. Graph Algorithms

### 8.1 BFS
```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    order = []

    while queue:
        node = queue.popleft()
        if node not in visited:
            order.append(node)   # record order
            visited.add(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    queue.append(neighbor)

    return order
```
## 8.2 DFS
#### Recursively
```python
def dfs(graph, node, visited=None, order=None):
    if visited is None:
        visited = set()
    if order is None:
        order = []

    if node not in visited:
        order.append(node)   # record order
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited, order)

    return order

```
#### Iteratively with stacks
```python
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    order = []

    while stack:
        node = stack.pop()
        if node not in visited:
            order.append(node)   # record order
            visited.add(node)
            # reversed ensures same order as recursive DFS
            stack.extend(reversed(graph[node]))

    return order
	```

### 8.3 Tarjan’s Algorithm (Strongly Connected Components)
```python
def tarjans_scc(graph):
    index = 0
    stack, indices, lowlink, on_stack, sccs = [], {}, {}, set(), []
    
    def strongconnect(v):
        nonlocal index
        indices[v] = index
        lowlink[v] = index
        index += 1
        stack.append(v)
        on_stack.add(v)
        
        for w in graph[v]:
            if w not in indices:
                strongconnect(w)
                lowlink[v] = min(lowlink[v], lowlink[w])
            elif w in on_stack:
                lowlink[v] = min(lowlink[v], indices[w])
        
        if lowlink[v] == indices[v]:
            scc = []
            while True:
                w = stack.pop()
                on_stack.remove(w)
                scc.append(w)
                if w == v:
                    break
            sccs.append(scc)
    
    for v in graph:
        if v not in indices:
            strongconnect(v)
    
    return sccs
```
### 8.4 Kosaraju’s Algorithm
```python
def kosaraju_scc(graph):
    visited = set()
    stack = []
    
    def dfs(v):
        visited.add(v)
        for nei in graph[v]:
            if nei not in visited:
                dfs(nei)
        stack.append(v)
    
    for v in graph:
        if v not in visited:
            dfs(v)
    
    rev_graph = {v: [] for v in graph}
    for u in graph:
        for v in graph[u]:
            rev_graph[v].append(u)
    
    visited.clear()
    sccs = []
    
    def dfs_rev(v, comp):
        visited.add(v)
        comp.append(v)
        for nei in rev_graph[v]:
            if nei not in visited:
                dfs_rev(nei, comp)
    
    while stack:
        v = stack.pop()
        if v not in visited:
            comp = []
            dfs_rev(v, comp)
            sccs.append(comp)
    
    return sccs
```

### 8.5 Articulation Points (Tarjan’s Algorithm)
```python
def articulation_points(graph):
    time = 0
    disc = {}
    low = {}
    parent = {}
    ap = set()
    
    def dfs(u):
        nonlocal time
        children = 0
        disc[u] = low[u] = time
        time += 1
        
        for v in graph[u]:
            if v not in disc:
                parent[v] = u
                children += 1
                dfs(v)
                low[u] = min(low[u], low[v])
                
                if parent.get(u) is None and children > 1:
                    ap.add(u)
                if parent.get(u) is not None and low[v] >= disc[u]:
                    ap.add(u)
            elif v != parent.get(u):
                low[u] = min(low[u], disc[v])
    
    for u in graph:
        if u not in disc:
            dfs(u)
    
    return ap
```

