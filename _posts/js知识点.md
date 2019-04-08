## JS知识点

#### 闭包

闭包就是能够读取其他函数内部变量的函数；

```javascript
function test() {
	var temp = 100;
	function foo() {
		document.write(temp);
	}
	return foo;
}

var tt = test();
tt(); // 100
```

上面代码块中，一旦test()执行完毕，那么我们认为temp变量在外部不可被访问。然而这段代码依然可以运行。造成这种现象的原因就是闭包，tt获取到了test()里面的foo()方法的引用，当执行时，自然而然可以访问test()内部的变量temp。

### 立即执行函数

在上面的闭包中，我们经常会写出这样的代码：

```javascript
function test2() {
	var arr = [];
	for(var i = 0; i < 10; i ++) {
		arr[i] = function() {
			document.write(i + ', ');
		}
	}

	return arr;
}

var myArr = test2();
for(var j = 0; j < 10; j++) {
	myArr[j]();
}
// 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,
```

上面代码运行结果显然不是我们想要的结果，那么造成这种结果的原因是，对于arr数组的每个元素赋值时，每个元素只是引用了i，但当循环结束时i值已经变为10，所以后面运行时会每个元素所使用的i值都是10。解决这种问题有两种方法：

```
// 方法一：立即执行函数
for(var i = 0; i < 10; i ++) {
	(function(j) {
		arr[j] = function() {
			document.write(j + ', ');
		}
	})(i);
}
```

```
// 方法二：改变i的作用域
for(let i = 0; i < 10; i ++) {
	arr[i] = function() {
		document.write(i + ', ');
	}
}
```

立即执行函数格式为：

`(function(j) {})(i)`

`(function(j) {}(i))`

官方建议第一种，后面的`()`相当于是方法的调用。其中的`i`是函数接收的形参，`j`是实参。

### 原型链

在JavaScript中，每个实例对象（object ）都有一个私有属性（称之为`__proto__`）指向它的原型对象（**prototype**），该原型对象也有一个自己的原型对象(__proto__) ，层层向上直到一个对象的原型对象为 `null`。根据定义，`null` 没有原型，并作为这个**原型链**中的最后一个环节。

原型是function对象的一个属性，它定义了构造函数制造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法，原型也是对象。

* 利用原型的特点和概念，可以提取出共有属性

```javascript
Car.proptotype = {
    name: 'BMW',
    color: 'red'
}

function Car() {}
```

上面的`Car`对象中，使用prototype给`Car`对象的原型链增加了两个属性，这种对象通用的属性我们可以使用prototype来给对象赋上。

* 对象如何查看原型 -> 隐式属性 `_proto_`

```javascript
Car._proto_
```

几乎每个对象有个隐式属性(在F12开发者模式中，隐形属性使用浅紫色标识，深紫色标识我们手动赋予的属性或方法)，其中`_proto_`属性指向的就是`Car.prototype`

* 对象如何查看对象的构造函数 -> 隐式属性`constructor`

```javascript
Car.constructor
```

* 使用`Object.create(原型)`还可以通过指定某个对象作为原型对象来继承某个对象

```
var Animal = {
    color: 'white',
    name : 'xiaobai'
};

var dog = Object.create(Animal);
```

上面通过`Object.create()`方法来指定了Animal来作为了dog继承自Animal

### apply/call

call和apply方法类似，区别是call接收的是一个参数列表，apply接收的是一个数组

##### 作用：改变`this`指向

```javascript
function Person(name, age) {
    this.anme = name;
    this.age = age;
}

var obj = {};
Person.call(obj, 'zing', '29');

console.log(obj); // {name: 'zing', age: '29'}
```

通过`call`方法可以改变`Person`中`this`的指向，相当于借用Person实现赋值。

使用场景：

```javascript
// 小王的代码
function Person(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}

// 我的代码
function Student(name, age, sex, score, grade) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.score = score;
    this.grade = grade;
}
```

上面小王的很多代码和我代码重复了，那通过call就可以实现借用小王的代码实现我的功能：

```
// 我的代码
function Student(name, age, sex, score, grade) {
    Person.call(this, name, age, sex);
    this.score = score;
    this.grade = grade;
}
```

使用apply实现上面的代码

```javascript
// 我的代码
function Student(name, age, sex, score, grade) {
    Person.apply(this, [name, age, sex]);
    this.score = score;
    this.grade = grade;
}
```

