# 任务26考题
* 第一题
关于如何把数组中的元素变成其他元素  

题目是
```
let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map(补全代码)
console.log(arr2) // ['周日', '周一', '周二', '周二', '周三', '周三', '周三', '周四', '周四', '周四', '周四','周六']
```
```
let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map((i)=>['周日','周一','周二','周三','周四','周五','周六'][i])
console.log(arr2) // ['周日', '周一', '周二', '周二', '周三', '周三', '周三', '周四', '周四', '周四', '周四','周六']
```
* 第二题
关于找出所有大于 60 分的成绩
```
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let scores2 = scores.filter(补全代码)
console.log(scores2) //  [95,91,82,72,85,67,66, 91]
```
```
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let scores2 = scores.filter(scrore => scrore > 65)
console.log(scores2) //  [95,91,82,72,85,67,66, 91]
```
* 第三题题目：

算出所有奇数之和
```
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let sum = scores.reduce((sum, n)=>{
  补全代码
},0)
console.log(sum) // 奇数之和：598 
```
```
let scores = [95,91,59,55,42,82,72,85,67,66,55,91]
let sum = scores.reduce((sum, n)=>sum + (n%2 ? n : 0),0)
console.log(sum) // 奇数之和：598 
```
