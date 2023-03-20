# JS数据结构小记

## 数组

### 创建和初始化

>使用new关键字，便可以简单地声明并初始化一个数组。并且可以指定数组长度。

```javascript
let daysOfweek = new Array(7);
```

除此之外，直接用中括号进行初始化也可。

```javascript
let daysOfweek = ['Sunday','Monday','Tuesday']
```

得到数组存储元素，即数组大小，使用length属性即可:arrow_double_down:

```javascript
console.log(daysOfweek.length);
```

#### 访问元素和迭代数组

> 访问数组里特定位置的元素，使用中括号传递数值位置即可。

### 添加元素

> 在数组末尾插入元素，把值赋给数组中最后一个空位上的元素，或者使用push方法。

:pushpin:JavaScript的数组是一个可以修改的对象。添加元素会动态增长。

> 在开头插入元素，使用unshift，可以直接把数值插入数组的开头。



:key:实现原理：腾出第一个元素的位置，将所有元素向右移动一位。

```javascript
Array.prototype.insertFirstPosition = function (value) {
    for (let i = this.length; i >= 0; i--) {
        this[i] = this[i - 1];
    }
    this[0] = value;
};

```

### 删除元素

> 删除数组里最靠后的元素，使用pop方法。

:pushpin: 通过push和pop方法，可以用数组来模拟栈。

> 删除数组的第一个元素，使用shift方法。

:pushpin:通过unshift和shift方法，可以用数组模拟队列。



### 在任意位置添加或删除元素