##日积月累 - JavaScript ##
1. js数据类型

	值类型（基本类型）：
	- String（字符串）
	- Number（数字）
	- Boolean（布尔）
	- Null（空）
	- Undefined（未定义）
	- Symbol（es6引入的一种新的原始数据类型，表示独一无二的值）

	引用数据类型：
	- Object（对象）
	- Array（数组）
	- Function（函数）
2. w3c 制定的 javascript 标准事件模型顺序

  	先事件捕获从windows > document 往下级直到 特定的事件节点，然后进行事件处理，再事件冒泡，从特定节点往上级，这个完整的过程.

3. setTimeout 方法， 指定 固定时间后运行 指定的 function 运行， 只运行一次， setInterval 是按照固定的时间 间隔运行。

        ```
        function checkState(){
           alert("liyuming");
        }
			window.setTimeout(checkState(), 10000); //立即被调用
			window.setTimeout(checkState, 10000); // 10s后被调用 
    		window.setTimeout("checkState()", 10000); //10s后被调用 注意和第一个的区别 有引号
		```

	checkState加了圆括弧相当于函数表达式，会立即执行，执行的结果作为返回值传递给settimeout,但要注意checkState（）是否加了引号.

4. 关于Javascript中数字的部分知识总结

	- Javascript中，由于其变量内容不同，变量被分为基本数据类型变量和引用数据类型变量。基本类型变量用八字节内存，存储基本数据类型(数值、布尔值、null和未定义)的值，引用类型变量则只保存对对象、数组和函数等引用类型的值的引用(即内存地址)。
		- javascirpt中的数字在计算机内存储为8Byte
	- JS中的数字是不分类型的，也就是没有byte/int/float/double等的差异。

	
