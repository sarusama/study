# 笔记

## 关于date
[关于日期的奇思妙想](https://github.com/lishengzxc/bblog/issues/5)


## map 和 forEach的差别
相同数据量下，map所花的时间要比foreach久。
Reason:
The map() method creates a new array with the results of calling a provided function on every element in the calling array.
The forEach() method executes a provided function once for each array element.
原因：
map函数会用原数组的每个元素执行完提供的函数来创建一个新数组
foreach函数每个元素执行一次提供的函数


## slice和substring在操作字符串上花的时间一致

## 循环的执行效率要比递归高


## JS栈的实现

```
window.Stack = function Stack (value = []) {
	let items = [];
	if ( _.isArray(value) ) {
		items = value;
	}
	this.top = items.length;
	this.items = items;
};
Stack.prototype.pushStack = function pushStack ( value ) {
	this.items.push(value);
	++this.top;

	return true;
};
Stack.prototype.popStack = function popStack () {
	--this.top;

	return this.items.pop();
}
Stack.prototype.peakStack = function peakStack () {
	return this.items[this.top - 1];
}
```
