# 对象
- `Object.craete(p)`创建一个继承了p的对象 ，具体可参考面向对象一节
-  `getter`和`setter` 存取器属性
-  对象的属性`value`，`writable`,`enumerable`,`configurable`,如果是存取器属性，没有前两个但是有`get`和`set`
-  设置对象的属性可以使用`Object.defineProperty()`
	
	```javascript
		var o={}
		o
		Object.defineProperty(o,x,{
									value:1,
									writable:true,
									enumerable:false,
									configurable:true
		})
	```
	
- 如果要同时修改或者创建多个属性，可以使用`Object.defineProperties`
	- 如果对象是不可扩展的，则可以编辑已有的属性，但是不能添加新属性
	- 如果属性是不可配置的，不能修改可配置性和可枚举性
	- 如果存储器属性是不可配置的，则不能修改其getter和setter方法，也不能转换为数据属性
	- 如果数据属性是不可配置的，则不能转换为存取器属性
	- 如果数据属性是不可配置的，则不能将可写性从false修改为true，但可以从true修改为false
	- 如果数据属性是不可配置和不可写的，不能修改它的值，然而可配置但不可写属性的值是可以修改的
-  对象扩展
	-  `Object.isExtensible(o)`判断对象的可扩展性
	-  `Object.preventExtensions()` 将对象转换为不可扩展的，当前属性不影响，新的属性不能加入（不可扩展的无法转换回可扩展的）
	-  `Object.seal()` 将对象转换为不可扩展的，同时将所有自有属设置为不可配置的(不能删除不能转换成存取器)，但是已有的可写属性依然可以更新，可以通过`Object.isSealed()`检测是否封闭，（封闭的不能解封）
	-  `Objecj.freeze()` 在seal的基础上，将自有的数据属性设置为只读，无法添加，删除，跟新属性；如果属性本身是一个对象的话，该对象可以更新，存取器属性不受影响；这个称为浅冻结；`Object.isFrozen()`判断是否`freeze`
	-  查询原型`Object.getPrototypeOf()`
	-  `Object.keys()`返回可枚举的自有属性名称组成的数组
	-  `Object.getOwnPropertyNames()`返回所有自有属性名称组成的数组，包括不可枚举的
	-  `Object.getOwnPropertypeDescriptor()`得到自有属性的描述符
	-  获取类属性`Object.prototype.toString.call(o).slice(8,-1)`，表示对象的类型信息


