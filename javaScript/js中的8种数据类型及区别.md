
## js中的8种数据类型
String,Number,Boolean,undefined,null,Symbol,bigInt,Object

**ES5 已认知数据类型为6种**
	
> **基本类型（原始类型）**
> 
	1. String
	2. Number
	3. Boolean
	4. undefined
	5. null
>>说明：
> >
1. 只能提供单一值，无法额外存储数据，所有的方法操作都是在对应的“对象包装器”创建临时对象的帮助下执行的。
2. 基本数据类型的变量是保存在栈内存中的，基本数据类型的值直接在栈内存中存储，值与值之间是独立存在的，修改一个变量不会影响其他的变量。

>>比较:
>
>>当比较两个基本数据类型的值时，本质上是比较值

> **引用类型**

	6. Object
		Object中包含的常规使用类型：
			1. Data
			2. function
			3. Array
			4. RegExp
>>说明：
>>
1. 无序属性的集合
2. 对象是保存在堆内存中的，每创建一个新的对象，就会在堆内存中开辟出一个新的空间，而变量保存的是对象的内存地址(对象的引用)，如果两个变量保存的是同一个对象引用，当修改其中一个变量修改属性时，另一个也会受到影响。

>>比较:
>
>>当比较两个引用数据类型时，本质上是比较的对象的内存地址.如果两个对象的属性是一模一样的，但是地址不同，也会返回false。
			
		
**后续加入两种基本类型**

	7. Symbol
	8. bigInt

Symbol:Symbol 值表示唯一的标识符。

1. Symbol() 创建
	```
	let demo1 = Symbol("demo") //demo为描述 可选
	```
2. 唯一标识符 相同描述也不是同一个
	```
	let demo1 = Symbol("demo");
	let demo2 = Symbol("demo");
	console.log(demo1 === demo2);//false
	```
3. Symbol并不支持字符串的隐式转换
	```
	不能 alert(demo1);
	而是使用：
	alert(demo1.toString() || alert(demo1.description)
4. Symbol的用处：（核心：Symbol是唯一的）

	1. “隐藏”属性
	
	- 如果我们想要向“属于”另一个脚本或者库的对象添加一个属性，我们可以创建一个 Symbol 并使用它作为属性的键。
	- Symbol 属性不会出现在 for..in 中，因此它不会意外地被与其他属性一起处理。并且，它不会被直接	访问，因为另一个脚本没有我们的 symbol。因此，该属性将受到保护，防止被意外使用或重写。
	
	2. 全局Symbol
	- ​ 通常所有的 Symbol 都是不同的，即使它们有相同的描述。但如果我们想创建两个不同地点的变量指向同一个Symbol呢
		1. Symbol.for():在全局注册表中通过描述创建/查找Symbol
		```
		let demo1 = Symbol.for('demo');
		let demo2 = Symbol.for('demo');
		console.log(demo1 === demo2);//true
		```
		2. Symbol.keyFor()：在全局注册表中通过全局Symbol查找其描述
		```
		let demo1 = Symbol("demo");
		console.log(Symbol.keyFor(demo1));//demo
		```
		3. 注意：上面两个方法仅限全局Symbol
		```
		let demo1 = Symbol('demo');
		console.log(Symbol.keyFor(demo1));//undefined
		
		let demo1 = Symbol.for('demo');
		console.log(Symbol.keyFor(demo1));//demo
		```
BigInt: 
- 在JS中，按照IEEE 754-2008标准的定义，所有数字都以双精度64位浮点格式表示。(-9007199254740991 (-(253-1))------9007199254740991(253-1))
	- 在此标准下，无法精确表示的非常大的整数将自动四舍五入。
	- 确切地说，JS 中的 Number类型只能安全地表示 -9007199254740991(-(2^53-1)) 和 9007199254740991(2^53-1)之间的整数，任何超出此范围的整数值都可能失去精度。
	```
	console.log(9999999999999999);    // → 10000000000000000
	```
	- JS 提供 Number.MAX_SAFE_INTEGER常量来表示 最大安全整数， Number.MIN_SAFE_INTEGER常量表示最小安全整数：
	```
	const minInt = Number.MIN_SAFE_INTEGER;	
	console.log(minInt);         // → -9007199254740991	
	console.log(minInt - 5);     // → -9007199254740996	
	// notice how this outputs the same value as above	
	console.log(minInt - 4);     // → -9007199254740996
	```

- 使用BigInt，应用程序不再需要变通方法或库来安全地表示Number.MAX_SAFE_INTEGER和Number.Min_SAFE_INTEGER之外的整数。 现在可以在标准JS中执行对大整数的算术运算，而不会有精度损失的风险。
	
1. 要创建 BigInt，只需在整数的末尾追加n即可
	```
	console.log(9007199254740995n);    // → 9007199254740995n	
	console.log(9007199254740995);     // → 9007199254740996
	```
	或者可以调用 BigInt() 构造函数
	```
	BigInt("9007199254740995");    // → 9007199254740995n
	```
	BigInt文字也可以用二进制、八进制或十六进制表示
	```
	// binary	
	console.log(0b100000000000000000000000000000000000000000000000000011n);	
	// → 9007199254740995n	
	// hex	
	console.log(0x20000000000003n);	
	// → 9007199254740995n	
	// octal	
	console.log(0o400000000000000003n);	
	// → 9007199254740995n	
	// note that legacy octal syntax is not supported	
	console.log(0400000000000000003n);	
	// → SyntaxError
	```
2. 不能使用严格相等运算符将 BigInt与常规数字进行比较，因为它们的类型不同：
	```
	console.log(10n === 10);    // → false	
	console.log(typeof 10n);    // → bigint	
	console.log(typeof 10);     // → number
	```
3. 可以使用等号运算符，它在处理操作数之前执行隐式类型转换
	```
	console.log(10n == 10);    // → true
	```
4. 除一元加号( +)运算符外，所有算术运算符都可用于 BigInt
	1. 不支持一元加号（ +）运算符的原因是某些程序可能依赖于 +始终生成 Number的不变量，或者抛出异常。 更改 +的行为也会破坏 asm.js代码。
	```
	10n + 20n;    // → 30n	
	10n - 20n;    // → -10n	
		+10n;         // → TypeError: Cannot convert a BigInt value to a number	
		-10n;         // → -10n	
	10n * 20n;    // → 200n	
	20n / 10n;    // → 2n	
	23n % 10n;    // → 3n	
	10n ** 3n;    // → 1000n	
	const x = 10n;	
		++x;          // → 11n	
		--x;          // → 9n
	```
5. 与 BigInt操作数一起使用时，算术运算符应该返回 BigInt值。因此，除法( /)运算符的结果会自动向下舍入到最接近的整数。例如:
	```
	25 / 10;      // → 2.5	
	25n / 10n;    // → 2n
	```
6. 隐式类型转换。
	- 因为隐式类型转换可能丢失信息，所以不允许在 bigint和 Number 之间进行混合操作。当混合使用大整数和浮点数时，结果值可能无法由 BigInt或 Number精确表示。
	- (9007199254740992n + 1n) + 0.5 
		- 这个表达式的结果超出了 BigInt和 Number的范围。小数部分的 Number不能精确地转换为 BigInt。大于 2^53的 BigInt不能准确地转换为数字。
		- 由于这个限制，不可能对混合使用 Number和 BigInt操作数执行算术操作。还不能将 BigInt传递给Web api和内置的 JS 函数，这些函数需要一个 Number 类型的数字。尝试这样做会报 TypeError错误
		```
		10 + 10n;    // → TypeError	
		Math.max(2n, 4n, 6n);    // → TypeError
		```
		- 注意，关系运算符不遵循此规则
		```
		10n > 5;    // → true
		```
		- 如果希望使用 BigInt和 Number执行算术计算，首先需要确定应该在哪个类型中执行该操作。为此，只需通过调用 Number()或 BigInt()来转换操作数：
		```
		BigInt(10) + 10n;    // → 20n	
		// or	
		10 + Number(10n);    // → 20
		```
		- 当 Boolean 类型与 BigInt 类型相遇时， BigInt的处理方式与 Number类似，换句话说，只要不是 0n， BigInt就被视为 truthy的值：
		```
		if (5n) {	
		    // 这里代码块将被执行	
		}	
		if (0n) {	
		    // 这里代码块不会执行	
		}
		``` 
		- 排序 BigInts和 Numbers数组时，不会发生隐式类型转换：
		```
		const arr = [3n, 4, 2, 1n, 0, -1n];	
		arr.sort();    // → [-1n, 0, 1n, 2, 3n, 4]
		```
		- 位操作符如 |、&、<<、>>和 ^对 Bigint的操作方式与 Number类似.
		

7. BigInt构造函数

	- 与其他基本类型一样，可以使用构造函数创建 BigInt。传递给 BigInt()的参数将自动转换为 BigInt:
	```
	BigInt("10");    // → 10n	
	BigInt(10);      // → 10n	
	BigInt(true);    // → 1n
	```
	- 无法转换的数据类型和值会引发异常:
	```
	BigInt(10.2);     // → RangeError	
	BigInt(null);     // → TypeError	
	BigInt("abc");    // → SyntaxError
	```
	- 可以直接对使用构造函数创建的 BigInt执行算术操作
	```
	BigInt(10) * 10n;    // → 100n
	```
	- 使用严格相等运算符的操作数时，使用构造函数创建的 Bigint与常规 Bigint的处理方式类似
	```
	BigInt(true) === 1n;    // → true
	```
总结：

BigInt是一种新的数据类型，用于当整数值大于 Number数据类型支持的范围时。这种数据类型允许我们安全地对大整数执行算术操作，表示高分辨率的时间戳，使用大整数id，等等，而不需要使用库。

不能使用 Number和 BigInt操作数的混合执行算术运算，需要通过显式转换其中的一种类型。 此外，出于兼容性原因，不允许在 BigInt上使用一元加号（ +）运算符。