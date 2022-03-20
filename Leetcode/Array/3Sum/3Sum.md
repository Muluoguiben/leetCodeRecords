## 15.三数之和

[三数之和](https://leetcode-cn.com/problems/3sum/)

给你一个包含 `n` 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？请你找出所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

 

**示例 1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

**示例 2：**

```
输入：nums = []
输出：[]
```

**示例 3：**

```
输入：nums = [0]
输出：[]
```

 

**提示：**

- `0 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`



### 思路

排序成有序递增数组后, 双指针查找

```ts
// TS
function threeSum(nums: number[]): number[][] {
  if (nums.length < 3) return []
  let res = [];
  let n: number = nums.length;
  nums.sort((a,b) => a - b)
  for (let i = 0; i < nums.length; i ++) {
    if (nums[i] > 0) break
    if (i > 0 && nums[i] === nums[i-1]) continue
    let L = i + 1;
    let R = nums.length - 1
    while (L < R) {
      let sum = nums[L] + nums[R] + nums[i]
      if (sum === 0) {
        res.push([nums[L],nums[i],nums[R]])
        while (L < R && nums[L] === nums[L+1]) L++
        while (L < R && nums[R] === nums[R-1]) R--
        L++
        R--
      }else if (sum < 0) {
        L++
      }else {
        R--
      }
    }
  }
  return res
};
```

![](https://first-1303075678.cos.ap-beijing.myqcloud.com/img/202201150042746.png)



进一步优化, 缩小遍历的范围

```ts
// TS
function threeSum(nums: number[]): number[][] {
  let res = []
  let n = nums.length 
  if (n < 3) return res
  nums.sort((a,b) => a - b)
  
  for (let i = 0; i < n - 2 && nums[i] <= 0; i++) {
    if (i > 0 && nums[i] === nums[i-1]) continue
    const target = -nums[i]
    let L = i + 1
    let R = n - 1
    while (L < R) {
      let sum = nums[L] + nums[R]
      if( sum === target) {
        res.push([nums[L],-target,nums[R]])
        while (L < R && nums[L] === nums[L+1]) L++
        while (L < R && nums[R] === nums[R-1]) R--
        L++
        R--
      }else if (sum < target) {
        L++
      }else {
        R--
      }
    }
  }
  return res
};
```

![image-20220115010033391](https://first-1303075678.cos.ap-beijing.myqcloud.com/img/202201150100759.png)



