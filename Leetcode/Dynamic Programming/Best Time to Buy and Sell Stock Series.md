Best Time to Buy and Sell Stock Series

#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

只能买一次, 只能卖一次

找最小值, 找最大值

![image-20211004234015914](https://first-1303075678.cos.ap-beijing.myqcloud.com/img/image-20211004234015914.png)

```js
// 1. 遍历数组 遇小更新小值, 再进行差值计算
// Input: [7,1,5,3,6,4]
	var maxProfit = function(prices) {
        let min_profit = Infinity
        let max_profit = 0
        for (let i = 0; i < prices.length; i++) {
            min_profit = Math.min(min_profit, prices[i]) // 7 1 1 1 1 1 
            max_profit = Math.max(prices[i] - min_profit, max_profit) // 0 0 4 4 5 5
        }
        return max_profit
    }
    
// 2. dp dp[i]为最大利润
    
    let dp = []
    dp.push(0)

	let min_profit = prices[0]
    for(let i = 1; i < prices.length; i++) {
        min_profit = Math.min(min_profit, prices[i])
        dp[i] = Math.max(prices[i] - min_profit, dp[i-1])
//        console.log(dp)
//        [ 0, 0 ]
//        [ 0, 0, 4 ]
//        [ 0, 0, 4, 4 ]
//        [ 0, 0, 4, 4, 5 ]
//        [ 0, 0, 4, 4, 5, 5 ]
    }
	return dp[dp.length - 1]
```



#### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

可以多次买卖股票

判断一个数是否比之前的数大, 大即正义

<img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/image-20211005000906179.png" alt="image-20211005000906179"  />

```tsx
// 1.贪心 判断一个数是否比之前的数大, 大即正义
// Input: [7,1,5,3,6,4]
	function maxProfit(prices: number[]): number {
        let max_profit: number = 0
        for (let i = 1; i < prices.length; i++ ){
            max_profit += Math.max(prices[i] - prices[i-1], 0) // 0 4 4 7 7
        }
        return max_profit
    }

```

![image-20211005004257663](https://first-1303075678.cos.ap-beijing.myqcloud.com/img/image-20211005004257663.png)

```tsx
// 2.flag buy为前一天价格, sell为后一天价格
// Input: [1,2,3,4,5]
	function maxProfit(prices: number[]):number {
        let max_profit: number = 0, buy: number = 0, sell: number = 0
        for (let i = 1; i < prices.length; i++) {
            if(prices[i] > prices[i-1]){
                sell = prices[i]
                if(buy === -1) {
                    // 保证 buy 每次只更新一回数值
                    buy = prices[i - 1]
                }
                if(i === prices.length - 1) {
                    // 最后一天了 还留着干嘛！
                    max_profit += sell - buy
                }
            }else if(buy < sell) {
                max_profit += sell - buy
                buy = -1
                sell = -1
            }
        }
        return max_profit
    }
```

