## 1.两数之和

[两数之和](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

```
示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

```
示例 2：

输入：nums = [3,2,4], target = 6
输出：[1,2]
```

```
示例 3：

输入：nums = [3,3], target = 6
输出：[0,1]
```

- 
  提示：

- 2 <= nums.length <= 104

- -109 <= nums[i] <= 109

- -109 <= target <= 109

- 只会存在一个有效答案

  

  进阶：时间复杂度小于 O(n2) 的算法





### 思路

#### 	1. 暴力解法

双层循环

```tsx
// TS
function twoSum(nums: number[], target: number): number[] {
  for(let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i,j]
      }
    }
  }
};
```

```rust
// rust
impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        for i in 0..nums.len() {
          for j in i+1..nums.len() {
            if nums[i] + nums[j] == target {
              return vec![i as i32, j as i32];
            }
          }
      }
      vec![]
    }
}
```



#### 2. 哈希表

##### 	

```ts
// TS
function twoSum(nums: number[], target: number): number[] {
  let map = new Map()

  for (let i = 0; i < nums.length; i++) {
    if (map.has(target - nums[i])) {
      return [map.get(target - nums[i]), i]
    }
    map.set(nums[i], i)
  }
  return []
};
```

详细版本

```ts
// TS
function twoSum(nums: number[], target: number): number[] {
  const prevNums = []

  for(let i = 0; i < nums.length; i++) {
    const num = nums[i]
    const targetNum = target - num
    const targetNumIndex = prevNums[targetNum]
    if (targetNumIndex !== undefined) {
      return [targetNumIndex, i]
    }else {
      prevNums[num] = i
    }
  }
  return []
};
```

```rust
// rust
use std::collections::HashMap;

impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut map = HashMap::new();
        for i in 0..nums.len() {
          if let Some(v) = map.get(&(target - nums[i])) {
            return vec![*v, i as i32];
          }
          map.insert(nums[i], i as i32);
      }
      vec![]
    }
}
```

记第一次用 rust 写算法. 

在写的过程以后要注意的点：

- 必须返回 vec![]
- 标准库 Hash**M**ap**::new()** 
- get (**&**(t - n))  && return vec![*****v, i as i32]
- 遍历 0..nums.len()

2022.1.7