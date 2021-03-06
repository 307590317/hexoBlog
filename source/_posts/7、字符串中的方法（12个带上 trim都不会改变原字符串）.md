---
title: 7、字符串中的方法（12个带上 trim都不会改变原字符串）
categories: 基础知识与数据类型
toc: true
---

在JS中用单/双引号包裹起来的都是字符串
字符串就是由0-多个字符组成的字串
1.以数字为索引，从零开始
2.有length属性，存储的是当前字符串中字符的个数（字符串的长度）
## `字符串的查询`
### `charAt && charCodeAt`
str.charAt(索引)：返回指定位置的字符
**<font color=red>字符串可以用[]访问单个字符，为什么还要用charAt()?区别如下：<font>**
- str[index]，IE7及以下不兼容，index超不超出字符串的长度都会返回undefined；
- str.charAt(index)：对于超出index 范围的值，会返回空字符串，IE6-8兼容

str.charCodeAt(索引)：返回指定位置字符的Unicode编码值（对应ASCII码表）
String.fromCharCode(十进制的Unicode值)：把Unicode值转换为对应的字符

### `indexOf && lastindexOf`(字符串中的此方法兼容所有浏览器)
str.indexOf（'A'）：获取A字符在str中第一次出现位置的索引
str.lastindexOf（'A'）:获取A字符在str中最后一次出现位置的索引
如果当前字符没有在str中出现过，则返回-1，我们可以根据这个规律验证一下字符串中是否包含某个字符
## `字符串的截取`
### `slice && substr && substring`
1.slice(start，end)
- start：要抽取的字串的起始下标（从0开始，可不写，如果不写start，则end也不能写，结果返回整个字符串）,支持负数，-1表示字符串的最后一个字符）
- end：子字符串的结束位置，包含start，而不包含end。（可不写，不写的话则返回start到原字符串结尾，如果为负数，-2则表示到子字符串的倒数第二个字符结束）
**说明**
1：<font color=red>**start >= end**</font>，则返回空字符串
2：<font color=red>**start或end超出范围**</font>，只截取未超出范围的字符，没有返回空字符串
```javascript
	var m='zhufengpeixun';
	var f=m.slice(12,15);
	console.log(f);//"n";
```

2.substr(start，length)['sʌbstər]
- start：要抽取的字串的起始下标（可不写，如果不写start，则end也不能写，结果返回整个字符串）,支持负数，-1表示字符串的最后一个字符）
- length：子串的字符数，必须是数值。如果省略了该参数，那么返回从 stringObject 的开始位置到结尾的字串。如果为0或负数，则返回空字符串
**提示和注释**
**注释**：substr() 的参数指定的是子串的开始位置和长度，因此它可以替代 substring() 和 slice() 来使用。
<font color=red>**重要事项：**</font>ECMAscript 没有对该方法进行标准化，因此反对使用它。

3.substring(start，end)
- start：要抽取的字串的起始下标（从0开始，可不写，如果不写start，则end也不能写，结果返回整个字符串）
- end：子字符串的结束位置，包含start，而不包含end。（可不写，不写的话则返回start到原字符串结尾）
**说明**
1：<font color=red>**start = end**</font>，则返回空字符串
2：<font color=red>**start >end**</font>，那么该方法在提取子串之前会先交换这两个参数。
3：<font color=red>**start或end超出范围**</font>，只截取未超出范围的字符，没有返回空字符串
<font color=red>**重要事项：**</font>与 slice() 和 substr() 方法不同的是，substring() 不接受负的参数，会将负数转换为0，然后和start调换位置
## `字符串转换为数组`
### **`split`**
str.split（）：按照某一个字符把字符串分割成数组，参数为字符或者正则
a.split（''）：将字符串分割为单个字符的数组
a.spit（' '）：将字符串分割为单词组成的数组
## `字符串的修改`
### `replace`
str.replace（n,m）：把字符n替换成为字符m。
**`注意`**：replace并不会修改原来的字符串，而是返回一个新的字符串
    1.在不使用正则的情况下，每次执行只能替换第一个匹配的字符串
	2.第一项为正则时，正则捕获几次，就替换几次，换成函数也同理，正则捕获几次，函数就执行几次，函数中返回的是什么，就相当于把正则捕获的内容替换成什么。
	3.如果换成函数，函数中会默认传入三个参数，arguments（当前函数的参数集合）
```javascript
	str.replace(/zhufeng/g,function(content,index,input){
		arguments（捕获到的内容，索引，原始字符串集合）
		默认传入的参数：
			如果传入的正则中有小括号，
				arguments[1] =  第一个小括号捕获的内容
				arguments[2] =  第二个小括号捕获的内容…直到小括号捕获的内容显示完，然后才继续显示索引
				arguments[n] =  每一次捕获的开始索引
			  arguments[n+1] =  原始字符串
			传入的正则中没有小括号
				arguments[0] = content:每一次捕获的大正则内容
				arguments[1] = index：每一次捕获的开始索引
				arguments[2] = input：原始字符串
		})
```
## `字符串的大小写转换`
### `toUpperCase && toLowerCase`
str.toUpperCase：把字母转换为大写
str.toLowerCase：把字母转换为小写
## `字符串中去除空格`
### `trim && trimLeft &&trimRight`
str.trim()：去除字符串两端的空白字符
str.trimLeft()：去除字符串左边的空白字符
str.trimRight())：去除字符串右边的空白字符
