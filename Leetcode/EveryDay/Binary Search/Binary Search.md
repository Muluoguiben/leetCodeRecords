Binary Search

https://leetcode.com/problems/binary-search/discuss/423162/Binary-Search-101

# From Leetcode

### **1. Choice of `lo` and `hi`, aka the boundary**

Normally, we set the initial boundary to the number of elements in the array



```
let lo = 0, hi = nums.length - 1;
```



But this is not always the case.
We need to remember: the boundary is the range of elements we will be searching from.
The initial boundary should include **ALL** the elements, meaning all the possible answers should be included. Binary search can be applied to none array problems, such as Math, and this statement is still valid.



For example, In LeetCode 35, the question asks us to find an index to **insert** into the array.
It is possible that we insert after the last element of the array, thus the complete range of boundary becomes



```
let lo = 0, hi = nums.length;
```



### **2. Calculate `mid`**

Calculating mid can result in overflow when the numbers are extremely big. I ll demonstrate a few ways of calculating `mid` from the worst to the best.



```javascript
let mid = Math.floor((lo + hi) / 2) // worst, very easy to overflow

let mid = lo + Math.floor((hi - lo) / 2) // much better, but still possible

let mid = (lo + hi) >>> 1 // the best, but hard to understand
```



When we are dealing with even elements, it is our choice to pick the left `mid` or the right `mid` , and as I ll be explaining in a later section, a bad choice will lead to an infinity loop.



```javascript
let mid = lo + Math.floor((hi - lo) / 2) // left/lower mid

let mid = lo + Math.floor((hi - lo + 1) / 2) // right/upper mid
```



### **3. How do we shrink boundary** ***

I always try to keep the logic as simple as possible, that is a single pair of `if...else`. But what kind of logic are we using here? My rule of thumb is always use a logic that you can **exclude** `mid`.
Let's see an example:



```javascript
if (target < nums[mid]) {
	hi = mid - 1
} else {
	lo = mid; 
}
```



Here, if the target is less than `mid`, there's no way `mid` will be our answer, and we can exclude it very confidently using `hi = mid - 1`. Otherwise, `mid` still has the potential to be the target, thus we include it in the boundary `lo = mid`.
On the other hand, we can rewrite the logic as:



```javascript
if (target > nums[mid]) {
	lo = mid + 1; // mid is excluded
} else {
	hi = mid; // mid is included
}
```



### **4. while loop**

To keep the logic simple, I always use



```
while(lo < hi) { ... }
```



Why? Because this way, the only condition the loop exits is `lo == hi`. I know they will be pointing to the same element, and I know that element always exists.



### **5. Avoid infinity loop** ***

Remember I said a bad choice of left or right `mid` will lead to an infinity loop? Let's tackle this down.
Example:



```javascript
let mid = lo + ((hi - lo) / 2); // Bad! We should use right/upper mid!

if (target < nums[mid]) {
	hi = mid - 1
} else {
	lo = mid; 
}
```



Now, imagine when there are only 2 elements left in the boundary. If the logic fell into the `else` statement, since we are using the left/lower mid, it's simply not doing anything. It just keeps shrinking itself to itself, and the program got stuck.
**We have to keep in mind that, the choice of `mid` and our shrinking logic has to work together in a way that every time, at least 1 element is excluded.**



```javascript
let mid = lo + ((hi - lo + 1) / 2); // Bad! We should use left/lower mid!

if (target > nums[mid]) {
	lo = mid + 1; // mid is excluded
} else {
	hi = mid; // mid is included
}
```

**So when your binary search is stuck, think of the situation when there are only 2 elements left. Did the boundary shrink correctly?**





# From  GeekTime

### 	变体一：查找第一个值等于给定值的元素

![img](https://first-1303075678.cos.ap-beijing.myqcloud.com/img/503c572dd0f9d734b55f1bd12765c4f8.jpg)

```java

public int bsearch(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid = low + ((high - low) >> 1);
    if (a[mid] >= value) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  if (low < n && a[low]==value) return low;
  else return -1;
}
```

完美,简洁但并不重要👆

```java
public int bsearch(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] > value) {
      high = mid - 1;
    } else if (a[mid] < value) {
      low = mid + 1;
    } else {
      if ((mid == 0) || (a[mid - 1] != value)) return mid;
      else high = mid - 1;
    }
  }
  return -1;
}
```

我们重点看第 11 行代码。**如果 mid 等于 0，那这个元素已经是数组的第一个元素，那它肯定是我们要找的；**

**如果 mid 不等于 0，但 a[mid]的前一个元素 a[mid-1]不等于 value，那也说明 a[mid]就是我们要找的第一个值等于给定值的元素。**

如果经过检查之后发现 a[mid]前面的一个元素 a[mid-1]也等于 value，那说明此时的 a[mid]肯定不是我们要查找的第一个值等于给定值的元素。那我们就更新 high=mid-1，因为要找的元素肯定出现在[low, mid-1]之间。

### 变体二：查找最后一个值等于给定值的元素

```java
public int bsearch(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] > value) {
      high = mid - 1;
    } else if (a[mid] < value) {
      low = mid + 1;
    } else {
      if ((mid == n - 1) || (a[mid + 1] != value)) return mid;
      else low = mid + 1;
    }
  }
  return -1;
}
```

我们还是重点看第 11 行代码。**如果 a[mid]这个元素已经是数组中的最后一个元素了，那它肯定是我们要找的；**

**如果 a[mid]的后一个元素 a[mid+1]不等于 value，那也说明 a[mid]就是我们要找的最后一个值等于给定值的元素。**

如果我们经过检查之后，发现 a[mid]后面的一个元素 a[mid+1]也等于 value，那说明当前的这个 a[mid]并不是最后一个值等于给定值的元素。我们就更新 low=mid+1，因为要找的元素肯定出现在[mid+1, high]之间。

### 变体三：查找第一个大于等于给定值的元素

```java
public int bsearch(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] >= value) {
      if ((mid == 0) || (a[mid - 1] < value)) return mid;
      else high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return -1;
}
```

如果 a[mid]小于要查找的值 value，那要查找的值肯定在[mid+1, high]之间，所以，我们更新 low=mid+1。

对于 a[mid]大于等于给定值 value 的情况，我们要先看下这个 a[mid]是不是我们要找的第一个值大于等于给定值的元素。**如果 a[mid]前面已经没有元素，或者前面一个元素小于要查找的值 value，那 a[mid]就是我们要找的元素。**这段逻辑对应的代码是第 7 行。

如果 a[mid-1]也大于等于要查找的值 value，那说明要查找的元素在[low, mid-1]之间，所以，我们将 high 更新为 mid-1。

### 变体四：查找最后一个小于等于给定值的元素

```java
public int bsearch7(int[] a, int n, int value) {
  int low = 0;
  int high = n - 1;
  while (low <= high) {
    int mid =  low + ((high - low) >> 1);
    if (a[mid] > value) {
      high = mid - 1;
    } else {
      if ((mid == n - 1) || (a[mid + 1] > value)) return mid;
      else low = mid + 1;
    }
  }
  return -1;
}
```



# Leetcode

[704. Binary Search](https://leetcode-cn.com/problems/binary-search/)  https://leetcode-cn.com/problems/binary-search/

[34. Find First and Last Position of Element in Sorted Array](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)  https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/

