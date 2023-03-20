# JS数据结构小记

[toc]

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

> 使用splice方法，指定位置/索引，就可以删除相应位置上指定数量的元素。

:key: : 

```javascript
numbers.splice(5,0,2,3,4);
```



- 第一个参数，表示删除或插入的元素索引值。

- 第二个参数，删除元素的个数。

- 第三个参数往后，添加到数组里的值。

  

### 数组合并

> 数组合并使用`concat`方法。

可以向一个数组传递数组、对象或是元素。数组会按照该方法传入的参数顺序连接指定数组。

```javascript
const zero = 0;
const positiveNumbers = [1, 2, 3];
const negativeNumbers = [-3, -2, -1];
let numbers = positiveNumbers.concat(zero, negativeNumbers);
```

此例子中，`zero`先和`positiveNumbers`合并，后`negativeNumbers` 再继续合并。

### 迭代器

#### `every`

> `every`方法会迭代数组中的每个元素，直到返回`false`。

#### `some`

> `some`方法会迭代数组中的每个元素，直到返回`true`。

#### `forEach`

> 迭代整个数组使用`forEach`方法，等同于使用`for`循环。

#### `map`&&`filter`

> `map`方法保存了传入`map`方法的运行结果。`filter`方法返回的新数组由使函数返回`true`的元素组成。

#### `reduce`

> `reduce`方法接收一个有如下四个参数的函数：

1. `previousValue`
2. `currentValue`
3. `index` (可选)
4. `array` （可选）

该函数返回一个将被叠加到累加器的值，`reduce`方法停止执行后返回这个累加器。

#### `for...of`

> ES2015引入了迭代数组值的`for...of`循环。

```javascript
for (const number of numbers) {
    console.log(number % 2===0?'even':'odd');
}
```



#### `@@iterator`

> ES2015为`Array`类添加了一个`@@iterator`属性，需要通过`Symbol.iterator`来访问。

```javascript
let iterator = numbers[Symbol.iterator]();
console.log(iterator.next().value);
```

或者如下输出所有值：

```javascript
iterator = numbers[Symbol.iterator]();
for (const n of iterator) {
    console.log(n);
}
```

#### `entries&keys&values`

> `entries`方法返回包含键值对的`@@iterator`。

```javascript
let numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15];
let aNumbers = numbers.entries();
console.log(aNumbers.next().value);
console.log(aNumbers.next().value);
console.log(aNumbers.next().value);
```

返回结果如下：

```
[ 0, 1 ]
[ 1, 2 ]
[ 2, 3 ]
```

>`keys`方法返回包含数组索引的`@@iterator`。

```javascript
let numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15];
let aKeys = numbers.keys();
console.log(aKeys.next());//{ value: 0, done: false }
console.log(aKeys.next());//{ value: 1, done: false }
console.log(aKeys.next());//{ value: 2, done: false }
```

`keys`方法返回数组的索引，当没有可迭代的值时，返回一个`value`值为`undefined`,`done`属性为`true`的对象。

`done`属性值为`false`，说明还有可迭代的值。

> `values`方法返回`@@iterator`包含数组的值。

```javascript
let aValues = numbers.values();
console.log(aValues.next());//{ value: 1, done: false }
console.log(aValues.next());//{ value: 2, done: false }
console.log(aValues.next());//{ value: 3, done: false }
```

### `使用from方法`

> `Array.from`根据已有的数组创建一个新数组。

```javascript
let numbers2 = Array.from(numbers);
```

还可以传入一个用来过滤值的函数：

```
let even = Array.from(numbers, x => (x % 2 === 0));
```

结果如下所示：

```
[
  false, true,  false,
  true,  false, true, 
  false, true,  false,
  true,  false, true, 
  false, true,  false 
]
```

### 使用`Array.of`方法

> `Arrya.of`方法根据传入的参数创建一个新数组。