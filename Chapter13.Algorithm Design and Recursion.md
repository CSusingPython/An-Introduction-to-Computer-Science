## Chapter 13

### 목표

- To understand basic techniques for analyzing the efficiency of algorithms. 

- To know what searching is and understand the algorithms for linear and 

  binary search. 

- To understand the basic principles of recursive definitions and functions and be able to write simple recursive functions. 

- To understand sorting in depth and know the algorithms for selection sort and merge sort. 

### 1. Searching

#### Example

> [1,4,9,11,15,21,25,29,31,36,40,45,52,59,61,65,69,71,91,101] 에서 특정 값의 index를 찾는 문제

#### 1. Linear Search

````python
def search(x, nums):
    for i in range(len(nums)):
		if nums[i] == x: #item found, return the index value .
		    return 1
    return -1 #loop finished, item was not in list
````

시간 복잡도 계산

1. 최상의 경우 (Best Case) -> 첫번째 원소에 있는 경우(1을 찾는 경우)
   $$
   T(n) = 1
   $$

2. 최악의 경우(Worst case) -> 아예 없는 경우(5를 찾는 경우)
   $$
   T(n) = n
   $$

3. 평균적인 경우(Average case) 
   $$
   T(n) = (\frac{n}{2}*\frac{1}{2}) + (n*\frac{1}{2}) = \frac{3}{4}n
   $$

#### 2. Binary Search

````python
def search(x, nums): 
    low= 0
	high= len(nums) - 1 
    while low <= high:
		#There is still a range to search 
        mid= (low + high)//2 #position of middle item
		item= nums[mid]
		if x== item : #Found it! Return the index
            return mid
        elif x < item:
            high = mid - 1
        else:
        	low = mid + 1
    return -1
````

시간 복잡도 계산

1. 최상의 경우 (Best Case) -> 가운데 원소에 있는 경우(40을 찾는 경우)
   $$
   T(n) = 1
   $$

2. 최악의 경우(Worst case) -> 아예 없는 경우(32를 찾는 경우)
   $$
   T(n) = 4 (==|log(20)|)
   $$

3. 평균적인 경우(Average case) -> d
   $$
   T(n) = log_2n
   $$

### 2. Recursive function

#### Example

> factorial 10을 계산해보자!

````python
def fact(n):
    if n == 0:
        return 1
   	else:
        return n * fact(n-1)
````

#### Recursion VS Iteration

* 재귀함수는 loop(Iteration)의 일반화된 모습

  -> 모든 루프는 재귀함수로 표현이 가능하다.

  -> 논리적으로는 동등한 속도가 나와야 하나, 실제 구현은 iteration이 좀 더 빠름 (재귀함수는 함수를 콜하기 때문.)

  -> 하지만 재귀함수를 잘못 짜면 이터레이션 보다 굉장히 느림.

##### CASE STUDY - BAD CASE fibonacci

````python
def loopfib(n):
    #returns the nth Fibonacci number
    curr= 1
    prev= 1
    for i in range(n-2):
	    curr, prev = curr+prev, curr return curr
    return curr

def fib(n):
    # bad case recursive function
    if n < 3:
        return 1
    else:
        return fib(n-1)+fib(n-2)
````

### 3. Selection Sort and Merge Sort

> [9,1,6,8,4,3,2,0]을 Sorting

#### Selection Sort

```python
def selSort(nums):
    #sort nums into asc ending order
    n = len(nums)
    #For each position in the list (except the very last) 
    for bottom in range(n-1):
    	#find the smallest item in nums[bottom] . . nums[n-1]
        mp = bottom#bottom is smallest initially 
        for i in range(bottom+1,n): #look at each position
	        if nums[i] < nums[mp]: #this one is smaller
                mp = i # remember its index
    #swap smallest item to the bottom 
    nums[bottom], nums[mp] = nums[mp], nums[bottom]
```

#### Merge Sort

````python
def mergeSort(nums):
    #Put items of nums in ascending order
    n = len(nums)
    #Do nothing if nums contains 0 or 1 items 
    if n > 1:
        #split into two sublists
        m= n//2
        nums1, nums2 = nums[: m], nums[m: ]
        #recursively sort each piece
        mergeSort(nums1)
        mergeSort(nums2)
        #merge the sorted pieces back into original list 
        merge(nums1, nums2, nums)
        
def merge(lst1, lst2, lst3):
    #these indexes keep track of current position in each list 
    i1,i2,i3= 0,0,0 #all start at the front
    n1, n2 = len(lst1), len(lst2)
    
    #Loop while both lst1 and lst2 have more items 
    while i1 < n1 and i2 < n2:
		if lst1[i1] < lst2[i2]: 
            lst3[i3] = lst1[i1] #top of lst1 is smaller
            i1 = i1 + 1 # copy it into current spot in lst3
        else:  #top of lst2 is smaller
            lst3[i3] = lst2[i2] # copy it into current spot in lst3
            i2 = i2 + 1 
            i3 = i3 + 1 #item added to lst3, update position
    #Copy remaining items (if any) from lst1 
	while i1 < n1:
        lst3[i3] = lst1[i1] 
        i1 = i1 + 1
        i3 = i3 + 1
	#Copy remaining items (if any) from lst2 
    while i2 < n2:
		lst3[i3] = lst2[i2] 
        i2 = i2 + 1
		i3 = i3 + 1

````
