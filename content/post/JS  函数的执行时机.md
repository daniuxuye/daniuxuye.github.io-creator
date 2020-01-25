# JS 函数的执行时机
今天学习了函数的执行时机下面写一些我的个人心得  

*先看一段代码*
```
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```
其打印出的结果为：
```
6、6、6、6、6、6
```
那为什么会输出6个6呢？  
因为`setTimeout`意思是过一会再执行函数内的内容，过了一会后‘1，2，3，4，5，6’全都变成了6了。所以输出了6个6。

## 那这段代码如何改变可以让其打印出`0、1、2、3、4、5`呢？

直接上代码
```
for(let i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```
此时打印的代码就是 `0、1、2、3、4、5`。  

### 为什么呢?
//  我那知道，又不是我设计的代码。 不过既然规定就是这样我们也得想一个理由来让自己接受这么一个现实。  

* 我的理解是JS在for和let一起使用的时候会加东西
* 每次循环会多创建一个i 
* 所以，setTimeout就形同虚设了。


# 还有别的办法可以打印出`0、1、2、3、4、5`吗？
以下我的千方百计收集来的资料，请大佬接好。
  
 1.  第一种
```
let i = -1
while(i<5){
    i++
    console.log(i);
  }
```
2. 第二种
```
 var arr = []
    var output = (i) => new Promise(res => {
      setTimeout(()=>{
        console.log(i)
        res()
      }, 0)
    })
    for (var i=0; i<5; i++) {
      arr.push(output(i))
    }
    Promise.all(arr).then(()=> console.log(5))
```
3. 第3种
```
  var out = (i) => {
      setTimeout (() => console.log(i), 0)
    }
    for (var i=0; i<6; i++) {
      out(i)
    }
```



