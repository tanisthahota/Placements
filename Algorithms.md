# 1. Sorting Algorithms

### 1.1 Quick Sort
```
def quicksort(arr):
	if len(arr) <= 1:
		return arr
	pivot = arr[len(arr)//2]
	left = [x for x in arr if x<pivot]
	mid = [x for x in arr if x==pivot]
	right = [ x for x in arr if x > pivot]
	return quicksort(left)+ middle+ quicksort(right)
```

### 1.2 Merge Sort
```
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
```

# 2. Searching Algorithms
### 2.1 Binary Search
```
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
	
	
```

# 3. Graph Algorithms 
### 3.1 Breadth First Search (BFS)
```

```

### 3.2 Depth First Search (DFS)

```

```