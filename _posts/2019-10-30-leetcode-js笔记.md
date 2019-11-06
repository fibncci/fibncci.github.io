---
layout: post
title: "leetcode_map"
date: 2019-10-30
tag: topic
---





刷leetcode用到的知识

## 数组和字符串



### 数组添元素

##### 1.尾部添加数组	.push(元素)

>  此方法是在数组的后面添加新加元素，此方法改变了数组的长度：
>
> arr.push(element1, ..., elementN)

##### 2.头部添加 数组.unshift(元素)

> arr.unshift(element1, ..., elementN)

```
 此方法是将一个或多个元素添加到数组的开头，并返回新数组的
    arr.unshift(6, 7)
    console.log(arr) //[6, 7, 2, 3, 4, 5]
    console.log(arr.length) //7 
```



##### 3.想添在哪就添在哪splice() 

> array.splice(start   [, deleteCount[, item1[, item2[, ...]]]]    )
> //从下标为start的元素开始，删除deleteCount个元素,并从start开始替换为item。deleteCount可以为0，这样你就只是添加了
>
> 第一个是开始，第二个删除个数，第三个添加的数
>
> Array.splice(开始位置， 删除的个数，元素)

```jsx
var arr=[1,2,3,4,5];
arr.splice(1,0,7);//返回[],这个函数返回的是删除的元素组成的数组。
console.log(arr);//[1,7,2,3,4,5]

   　　　　万能方法，可以实现增删改：
let arr = [1, 2, 3, 4, 5];
     let arr1 = arr.splice(2, 0 'haha')
     let arr2 = arr.splice(2, 3)
     let arr1 = arr.splice(2, 1 'haha')
     console.log(arr1) //[1, 2, 'haha', 3, 4, 5]新增一个元素
     console.log(arr2) //[1, 2] 删除三个元素
     console.log(arr3) //[1, 2, 'haha', 4, 5] 替换一个元素
```

##### 4.添在头或尾

> var new_array = old_array.concat(value1[, value2[, ...[, valueN]]]);

```csharp
[0].concat([1,2]);//返回[0,1,2]
[1,2].concat([0]);//返回[1,2,0]

 此方法是一个可以将多个数组拼接成一个数组：
 let arr1 = [1, 2, 3]
      arr2 = [4, 5]
  let arr = arr1.concat(arr2)
  console.log(arr)//[1, 2, 3, 4, 5]
```







### 操作数组

印象中数组有很多方法，系统的整理一下，放在自己家里方便回头查~

1. Array.map()

   ```js
   此方法是将数组中的每个元素调用一个提供的函数，结果作为一个新的数组返回，并没有改变原来的数组
   let arr = [1, 2, 3, 4, 5]
       let newArr = arr.map(x => x*2)
       //arr= [1, 2, 3, 4, 5]   原数组保持不变
       //newArr = [2, 4, 6, 8, 10] 返回新数组
   ```

   

   　　

2. Array.forEach()

   ```js
   此方法是将数组中的每个元素执行传进提供的函数，没有返回值，直接改变原数组，注意和map方法区分
   let arr = [1, 2, 3, 4, 5]
      num.forEach(x => x*2)
      // arr = [2, 4, 6, 8, 10]  数组改变,注意和map区分
   ```

   

   　　

3. Array.filter()

   ```js
   此方法是将所有元素进行判断，将满足条件的元素作为一个新的数组返回
   let arr = [1, 2, 3, 4, 5]
       const isBigEnough => value => value >= 3
       let newArr = arr.filter(isBigEnough )
       //newNum = [3, 4, 5] 满足条件的元素返回为一个新的数组
   ```

   

   　　

4. Array.every()

   ```js
   此方法是将所有元素进行判断返回一个布尔值，如果所有元素都满足判断条件，则返回true，否则为false：
   let arr = [1, 2, 3, 4, 5]
       const isLessThan4 => value => value < 4
       const isLessThan6 => value => value < 6
       arr.every(isLessThan4 ) //false
       arr.every(isLessThan6 ) //true
   ```

   

   　　

5. Array.some()

   ```js
    此方法是将所有元素进行判断返回一个布尔值，如果存在元素都满足判断条件，则返回true，若所有元素都不满足判断条件，则返回false：
    let arr= [1, 2, 3, 4, 5]
       const isLessThan4 => value => value < 4
       const isLessThan6 => value => value > 6
       arr.some(isLessThan4 ) //true
       arr.some(isLessThan6 ) //false
   ```

   

6. Array.reduce()

   ```js
    此方法是所有元素调用返回函数，返回值为最后结果,传入的值必须是函数类型：
    let arr = [1, 2, 3, 4, 5]
      const add = (a, b) => a + b
      let sum = arr.reduce(add)
      //sum = 15  相当于累加的效果
      与之相对应的还有一个 Array.reduceRight() 方法，区别是这个是从右向左操作的
   ```

   

7. Array.pop()

   ```
    此方法在数组后面删除最后一个元素，并返回数组，此方法改变了数组的长度：
   let arr = [1, 2, 3, 4, 5]
       arr.pop()
       console.log(arr) //[1, 2, 3, 4]
       console.log(arr.length) //4
   ```

   

8. Array.shift()

   ```
    此方法在数组后面删除第一个元素，并返回数组，此方法改变了数组的长度：
    let arr = [1, 2, 3, 4, 5]
       arr.shift()
       console.log(arr) //[2, 3, 4, 5]
       console.log(arr.length) //4 
   ```

   







1. Array.toString()

   ```
    此方法将数组转化为字符串：
    let arr = [1, 2, 3, 4, 5];
      let str = arr.toString()
      console.log(str)// 1,2,3,4,5
   ```

   

2. Array.join()

   ```js
     此方法也是将数组转化为字符串：　　
     let arr = [1, 2, 3, 4, 5];
      let str1 = arr.toString()
      let str2 = arr.toString(',')
      let str3 = arr.toString('##')
      console.log(str1)// 12345
      console.log(str2)// 1,2,3,4,5
      console.log(str3)// 1##2##3##4##5
   ```

   

   　　

   ```
   通过例子可以看出和toString的区别，可以设置元素之间的间隔~ 
   ```

　



　　











### 字符串的方法

切片

**1.substr**

substr(start,length)表示从start位置开始，截取length长度的字符串。

```
`var` `src=``"images/off_1.png"``;``alert(src.substr(7,3));`
```

> 弹出值为：off

**2.substring**

substring(start,end)表示从start到end之间的字符串，包括start位置的字符但是不包括end位置的字符。

```
`var` `src=``"images/off_1.png"``;``alert(src.substring(7,10));`
```

> 弹出值为：off

**3.indexOF**

indexOf() 方法返回某个指定的字符串值在字符串中首次出现的位置（从左向右）。没有匹配的则返回-1，否则返回首次出现位置的字符串的下标值。

```
`var` `src=``"images/off_1.png"``;``alert(src.indexOf(``'t'``));``alert(src.indexOf(``'i'``));``alert(src.indexOf(``'g'``));`
```

> 弹出值依次为：-1,0,3

**4.lastIndexOf**

lastIndexOf()方法返回从右向左出现某个字符或字符串的首个字符索引值（与indexOf相反）

[?](https://www.jb51.net/article/161321.htm#)

```
`var` `src=``"images/off_1.png"``;``alert(src.lastIndexOf(``'/'``));``alert(src.lastIndexOf(``'g'``));`
```

> 弹出值依次为：6,15

**5.split**

将一个字符串分割为子字符串，然后将结果作为字符串数组返回。

以空格分割返回一个了字符串返回

[?](https://www.jb51.net/article/161321.htm#)

```jsj s
`function` `SplitDemo(){`` ``var` `s, ss;`` ``var` `s = ``"The rain in Spain falls mainly in the plain."``;`` ``// 在每个空格字符处进行分解。`` ``ss = s.split(``" "``);`` ``return``(ss);``}`
```





## 参考文献

```
g h m j m
```

