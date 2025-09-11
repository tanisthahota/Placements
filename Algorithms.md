# 1. Searching Algorithms
### 1.1 Linear Search

	def linearsearch(arr,target):
		n= len(arr)-1
		for i in range(n):
			if arr[i]== target:
				return 1
			else:
				return -1

### 1.2 Binary Search

	def binarysearch(arr, target):
		n = len(arr)+1
		right , left =0
		for i in range (0,n):
			mid= (right+left) //2
			if arr[mid] == target:
				return mid
			elif arr[mid] > target:
				left= mid+1
			else:
				right = mid -1
		return -1 


# 2.Sorting Algorithms

### 2.1 Bubble Sort
def bubblesort(arr):
	n = len(arr)
	for i in range(n):
		for j in range(i,n):	
			if arr[i]>arr[j]:
				arr[i], arr[j] = arr[j], arr[i]

### 2.2 Selection Sort
	def selectionsort(arr):
		n = len(arr)
		for i in range(n):
			minindex = i
			for j in range(i,n):
				if arr[j] < arr[i]:
					minindex = j
				
			arr[i], arr[minindex]= arr[minindex], arr[i]
		return arr


### 2.3 Quick Sort

	def quicksort(arr):
		if len(arr) <= 1:
			return arr
		pivot = arr[len(arr)//2]
		left = [x for x in arr if x<pivot]
		mid = [x for x in arr if x==pivot]
		right = [ x for x in arr if x > pivot]
		return quicksort(left)+ middle+ quicksort(right)


### 2.4 Merge Sort

	def mergesort(arr):
		if len(arr) <=1:
			return arr
			
		middle = len(arr) //2
		left = mergesort(arr[:mid])
		right = mergesort(arr[mid:])
		return merge(left,right)

	def merge(left, right):
		result = []
		i = j = 0 
		while i < len(left) and j < len(right): 
			if left[i] < right[j]:
				result.append(left[i]) 
				i += 1
			else:
				result.append(right[j]) 
				j += 1 
		result.extend(left[i:])
		result.extend(right[j:]) 
		return result

### 2.5 Heap Sort


# 3. Recursion & Divide and Conquer

### 3.1 Tower of Hanoi
	

### 3.2 Binary Exponentiation (Fast Power)

### 3.3 Karatsuba’s Algorithm (Fast Multiplication)

### 3.4 Strassen’s Matrix Multiplication


# 4. Greedy Algorithms

### 4.1 Activity Selection

Fractional Knapsack

Huffman Coding

Kruskal’s Algorithm (MST)

Prim’s Algorithm (MST)

Dijkstra’s Algorithm (Shortest Path)

Job Scheduling (Greedy Scheduling)





# 3. Graph Algorithms 
### 3.1 Breadth First Search (BFS)
```

```

### 3.2 Depth First Search (DFS)

```

```

Topological Sort

Bellman-Ford Algorithm

Floyd-Warshall Algorithm

Johnson’s Algorithm

A* Search Algorithm

Tarjan’s Algorithm (SCCs)

Kosaraju’s Algorithm (SCCs)

Edmonds-Karp / Ford-Fulkerson (Max Flow)

Dinic’s Algorithm (Max Flow)

Union-Find / Disjoint Set Union (DSU)

# dp


# Mathematical Algorithms
## Euclids Algorithm
