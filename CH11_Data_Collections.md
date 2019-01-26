### Data Collections



#### List

```python
myList = [36, 18, 5, 4]
```

- a sequence of items stored as a single object
- Items in a list can be accessed by indexing and sublists can be accesed by slicing
- mutable



#### List Operations

| operatonr           | meaning                             |
| ------------------- | ----------------------------------- |
| <seq> + <seq>       | concatenation                       |
| <seq>* <int-expr>   | repetition                          |
| <seq>[]             | indexing                            |
| len(<seq>)          | length                              |
| <seq>[:]            | slicing                             |
| for <var> in <seq>: | iteration                           |
| <expr> in <seq>     | membership check(returns a boolean) |



#### List Mehods

- append(x) : adds element x to end of list
- sort() : Sorts(orders) the list
- reverse() : reverses the list
- index(x) : returns index of first occurrence of x
- insert(i, x) : inserts x into list at index i
- count(x) : returns the number of occurrences of x in list
- remove(x) : deletes the first occurrence of x in list
- pop(i) : deletes the ith element of the list and reutrns its value

cf) del : not list method, built-in operation

```python
del myList[1]
del myList[1:3]
```



##### Example: Statistic

```python
from math import sqrt

def getNumbers():
    nums = []
    xStr = input("Enter a number (<Enter> to quit) >> ")
    while xStr != "":
        x = float(xStr)
        nums.append(x)
        xStr = input("Enter a number (<Enter> to quit) >> ")
    return nums

def mean(nums):
    total = 0.0
    for num in nums:
        total = total + num
    return total / len(nums)

def stdDev(nums, xbar):
    sumDevSq = 0.0
    for num in nums:
        dev = num - xbar
        sumDevSq = sumDevSq + dev * dev
    return sqrt(sumDevSq / (len(nums) - 1))

def median(nums):
    nums.sort()
    size = len(nums)
    midPos = size // 2
    if size % 2 == 0:
        med = (nums[midPos] + nums[midPos - 1]) / 2.0
    else:
        med = nums[midPos]
    return med
```



#### Dictionary

```python
passwd = {"guido":"superprogrammer", "turing":"genius",
          "bill":"monopoly"}
psswd["guido"]
passwd["bill"] = "bluescreen"
```

- one of the built-in data types for collections
- key-value pair  mapping cf) hashes / associative array

- mutable
- order of keys will look essentially random

- keys can be any immutable type, and values can be any type at all



#### Dictionary Methods

- <key> in <dict> : Return True if dictionary contains the key
- <dict>.keys() : returns a sequence of keys
- <dict>.values() : returns a sequence of values
- <dict>.items() : returns a sequence of tuples (key, value)
- <dict>.get(<key>, <default>) : if dictionary has key reutrns its value, otherwise default
- del <dict>[<key>] : deletes the specified entry
- <dict>.clear() : deltes all entries
- for <ar> in <dict>: : loops over the keys



##### Example: Word Count

```python
def byFreq(pair):
    reutrn pair[1]
    
def main():
    print("This is program analyzes word frequency in a file")
    print("and prints a report on the n most frequent words.\n")
    
    fname = input("File to analyze: ")
    text = open(fname, 'r').read()
    text = text.lower()
    for ch in '!"#$%&()*+,-./:;<=>?@[\\]^_`{|}~':
        text = text.replace(ch, ' ')
    words = text.split()
    
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
        
    n = eval(input("Output analysis of how many words? "))
    items = list(counts.items())
    items.sort()
    items.sort(key=byFreq, reverse=True)
    for i in range(n):
        word, count = items[i]
        print("{0:<15}{1:>5}".format(word, count))
        
if __name__ == '__main__': main()
```



[추가 참고:Collections module](https://www.slideshare.net/dahlmoon/collections-20160313)

