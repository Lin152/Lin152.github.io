---
title: JavaScript实用的功能
tags: Lin
---

includes() 函数用来判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回false
	
	let arr = ['react', 'angular', 'vue']
		if  (arr.includes('react')) {
    	console.log('react存在')
	}
指数运算符，具有与Math.pow(..)等效的计算结果。

	console.log(Math.pow(2, 10)) // 输出1024
	console.log(2**10) // 输出1024



对async/await的支持，也就我们所说的异步函数，这是一个很实用的功能。 async/await相当于一个语法糖，解决了回调地狱的问题

Object.values()是一个与Object.keys()类似的新函数，但返回的是Object自身属性的所有值，不包括继承的值。

	const obj = {
	    a: 1,
	    b: 2,
	    c: 3,
	}
	// 不使用Object.values()
	const vals = Object.keys(obj).map(e => obj[e])
	console.log(vals) // [ 1, 2, 3 ]
	
	// 使用Object.values()
	console.log(Object.values(obj)) // [ 1, 2, 3 ]
Object.entries()函数返回一个给定对象自身可枚举属性的键值对的数组。

	const obj = {
	    a: 1,
	    b: 2,
	    c: 3,
	}
	// 不使用Object.entries()
	Object.keys(obj).forEach(key=>{
	    console.log('key:'+key+' value:'+obj[key])
	})
	//key:a value:1
	//key:b value:2
	//key:c value:3
	
	// 使用Object.entries()
	for(let [key,value] of Object.entries(obj1)){
	    console.log(`key: ${key} value:${value}`)
	}
	//key:a value:1
	//key:b value:2
	//key:c value:3

通过Set实现数组去重

	const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]
	console.log([...new Set(numbers)]) 
	// [2, 3, 4, 5, 6, 7, 32]

Array对象的扩展

Array.prototype.from：转换具有Iterator接口的数据结构为真正数组，返回新数组。

	console.log(Array.from('foo')) // ["f", "o", "o"]
	console.log(Array.from([1, 2, 3], x => x + x)) // [2, 4, 6]
	
Array.prototype.of()：转换一组值为真正数组，返回新数组。
	
	Array.of(7)       // [7] 
	Array.of(1, 2, 3) // [1, 2, 3]
	Array(7)          // [empty, empty, empty, empty, empty, empty]
	Array(1, 2, 3)    // [1, 2, 3]
数组空位：ES6明确将数组空位转为undefined或者empty

	Array.from(['a',,'b']) // [ "a", undefined, "b" ]
	[...['a',,'b']] // [ "a", undefined, "b" ]
	Array(3) //  [empty × 3]
	[,'a'] // [empty, "a"]
includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

	const array1 = [1, 2, 3]
	console.log(array1.includes(2)) // true
	
	const pets = ['cat', 'dog', 'bat']
	console.log(pets.includes('cat')) // true
	console.log(pets.includes('at')) // false

幂运算符**，具有与Math.pow()一样的功能，代码如下：
	
	console.log(2**10) // 1024
	console.log(Math.pow(2, 10)) // 1024
flatMap()与 map() 方法和深度为1的 flat() 几乎相同.，不过它会首先使用映射函数映射每个元素，然后将结果压缩成一个新数组，这样效率会更高。


	var arr1 = [1, 2, 3, 4]
	
	arr1.map(x => [x * 2]) // [[2], [4], [6], [8]]
	
	arr1.flatMap(x => [x * 2]) // [2, 4, 6, 8]
	
	// 深度为1
	arr1.flatMap(x => [[x * 2]]) // [[2], [4], [6], [8]]
	
从数组中获取惟一的值
要从数组中获得唯一的值，需要使用filter方法过滤掉重复的值。但是有了新的Set原生对象，事情就变得非常简单了。

	let uniqueArray = [...new Set([1, 2, 3, 3,3,"school","school",'ball',false,false,true,true])];
	>>> [1, 2, 3, "school", "ball", false, true]
在某些情况下， 我们想从数组中删除虚值。 虚值是 JavaScript 中的值为FALSE的值。 JavaScript 中只有六个虚值，它们是：
undefined
null
NaN
0
'' (空字符)
false
过滤这些虚值的最简单方法是使用下面的函数：

	myArray.filter(Boolean)

禁用鼠标右键
有些情况，我们想在网页上禁用鼠标的右键，可以使用下面的方式来禁用：

	<body oncontextmenu="return false">
	  <div></div>
	</body>

获取数组中的最后一项
如果要获取数组的末尾元素，可以使用slice方法。

	let array = [0, 1, 2, 3, 4, 5, 6, 7] 
	console.log(array.slice(-1))
	>>>[7]
	
	console.log(array.slice(-2))
	>>>[6, 7]
	
	console.log(array.slice(-3))
	>>>[5, 6, 7]

格式化JSON代码
我们都非常熟悉JSON.stringify，但比较少知道的是它还可以进行格式化的输出。

stringify 方法有三个参数：value，replacer和space。其中，后两个是可选参数，这也是我们很少知道它的原因。 要缩进JSON，必须使用space参数。

	console.log(JSON.stringify({name:"John",Age:23},null,'\t'));
	>>> 
	{
	 "name": "John",
	 "Age": 23
	}











