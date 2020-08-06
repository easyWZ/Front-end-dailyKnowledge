## 原型 ##
[> https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects/Object_prototypes](http://https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Objects/Object_prototypes "对象原型")

   javaScript常被描述为一种基于原型的语言（prototype-based language） 

- 每个对象拥有一个原型对象，对象以其原型为模板，从原型继承方法和属性。
- 原型对象也可能拥有原型，并从中继承方法和属性，一层一层，以此类推。这种关系常被称为**原型链（prototype chain）**，它解释了为何一个对象会拥有定义在其他对象中的属性和方法。
- 准确的说，这些属性和方法定义在Object的构造器函数（constructor functions）之上的prototype属性上，而非对象实例本身。
- 在传统的OOP中，首先定义“类”，此后创建对象实例时，类中定义的所有属性和方法都被复制到实例中。在JavaScript中并不如此复制-而是在对象实例和它的构造器之间建立一个链接（它是_proto_属性，是从构造函数的prototype属性派生的），之后通过上溯原型链，在构造器中找到这些属性和方法。

> - 注意：对象的原型可以通过Object.getPrototypeOf(obj)或者_proto_属性获得
> - 对象的原型是每个实例上都有的属性，构造函数的prototype仅是构造函数的属性
> - 即： Object.getPrototypeOf(new Foobar())和Foobar.prototype指向着同一个对象。
> 

