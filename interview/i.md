# Interview

- [常见问题](#常见问题)
- [0218 面试](#0218面试)

## 找工作

https://www.zhipin.com/job_detail/db5e3672984fa2fb1X1-3tS6GFo~.html?ka=search_list_24

校招请官网投递 投递链接：https://job.bytedance.com/campus/
内推码： XADVXZP
前端（高级）研发工程师

岗位描述

1. 负责今日头条相关产品前端业务实现。
2. 负责 WEB/WAP 页面性能优化，打造良好的用户体验。
3. 搭建高效的开发环境，review 同事代码，确保工程质量。

岗位要求 学历本科及以上

1. 熟悉 WEB 前端技术，对符合 WEB 标准的网站重构有丰富经验，有大型工程经验优先。
2. 至少熟悉一门 MVVM 框架，熟悉 React+Redux+Koa+Webpack+SSR 技术栈优先。
3. 精通 HTML5、CSS3、ES6，熟悉 HTTP 协议和 Node.js 开发。
4. 计算机基础扎实，熟悉常见的数据结构、算法和设计模式。
5. 能够独立开发通用的 UI 组件，有 UI 组件开发经验优先。
6. 团队精神，性格乐观，能积极面对压力。
7. 有较强的逻辑思维能力，善于分析、归纳、解决问题。
8. 学习能力强，有一定的技术视野。

## 学技术

6 种原始（Primitive）类型

- boolean
- number
- string
- undefined
- null
- symbol

typeof 对于原始类型来说，除了 null 都可以显示正确的类型；typeof 对于对象来说，除了函数都会显示 object，所以说 typeof 并不能准确判断变量到底是什么类型。

如果我们想判断一个对象的正确类型，这时候可以考虑使用 instanceof，因为内部机制是通过原型链来判断的，且他调用的是 `[Symbol.hasInstance]()`.比如，`foo instanceof Foo`在语言内部，实际调用的是`Foo[Symbol.hasInstance](foo)`。

```js
var b = function() {
  function a() {
    console.log(this)
  }

  console.log(this)

  a()
}

b.call({})
// {}
// Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, frames: Window, …}
```

以上证明：call 等修改 this 只能改一层，下面的几层不会改变

箭头函数使用 bind 等函数无效，且不报错。箭头函数的 this 一旦被绑定，就不会再被任何方式所改变。

闭包：函数 A 内部有一个函数 B，函数 B 可以读写函数 A 中的变量，那么函数 B 就是闭包。

关于是否加分号： https://www.zhihu.com/question/20298345 所以就不加了。真正会导致上下行解析出问题的 token 有 5 个： ( , [ , / , + , - 括号，方括号，正则开头的斜杠，加号，减号 是这些为一行开头时，js 不会在上一行自动加分号

`JSON.parse(JSON.stringify(object))` 深拷贝有如下问题：

- 会忽略 undefined
- 会忽略 symbol
- 不能序列化函数
- 不能解决循环引用的对象

`Reflect.ownKeys()`参数是 object，其实 `[]` 也是 object：

```js
const a = [1, 2, 3]

console.log(Reflect.ownKeys(a))
// (4) ["0", "1", "2", "length"]
```

当对象是函数时：

```js
let func = (a, b, c) => {
  return 1
}

Reflect.ownKeys(func).forEach(k => {
  console.log(k, func[k])
})
// length 3
// name func
```

提升存在的根本原因就是为了解决函数间互相调用的情况

函数提升优先于变量提升，函数提升会把整个函数挪到作用域顶部，变量提升只会把声明挪到作用域顶部

### 组合继承

```js
function Parent(value) {
  this.val = value
}
Parent.prototype.getValue = function() {
  console.log(this.val)
}
function Child(value) {
  Parent.call(this, value)
}
Child.prototype = new Parent()

const child = new Child(1)

child.getValue() // 1
child instanceof Parent // true
```

所以：

- 函数有 `prototype` ，对象有 `__proto__`
- 在子类的构造函数中通过 Parent.call(this) 继承父类的属性，然后改变子类的原型为 new Parent() 来继承父类的函数。

有好多骚操作： https://www.jianshu.com/p/e161bd720e64

```js
;['1', '2', '3'].map(parseInt)
// [1, NaN, NaN]
```

`+` 的优先级比三元运算符 `condition ? val1 : val2`的优先级高。

```js
var val = 'smtg'
console.log('Value is ' + (val === 'smtg') ? 'Something' : 'Nothing')
// "Something"
```

在 JavaScript 中，2^53 是最大的值，没有比这更大的值了。所以 2^53 + 1 == 2^53，所以这个循环无法终止。

JavaScript 中采用双精度浮点数格式，即 IEEE 754 标准。在该格式下，有些数字无法表示出来，比如：0.1 + 0.2 = 0.30000000000000004 ，这不是 JavaScript 的锅，所有采用该标准的语言都有这个问题，比如：Java、Python 等。

在 switch 内部使用严格相等 === 进行判断

`-9 % 2 = -1` 以及 `Infinity % 2 = NaN`，求余运算符会保留符号，所以只有 isEven 的判断是可靠的，因为 `0 === -0` 返回 true。

一个鲜为人知的事实：其实 `Array.prototype` 也是一个数组。这点在 MDN 文档中提到过。 而 `Object.prototype` 就是对象

当 `[0]` 需要被强制转成 Boolean 的时候会被认为是 true，而 a == true 的转换规则在 ES5 规范的第 11.9.3 节中已经定义过。规范指出，== 相等中，如果有一个操作数是布尔类型，会先把他转成数字，所以比较变成了 `[0] == 1`；同时规范指出如果其他类型和数字比较，会尝试把这个类型转成数字再进行宽松比较，而对象（数组也是对象）会先调用它的 toString() 方法，此时`[0]`会变成 "0"，然后将字符串 "0" 转成数字 0

```js
;[] == []
// false
```

如果比较的两个对象指向的是同一个对象，就返回 true，否则就返回 false，显然，这是两个不同的数组对象。

"5" + 2 = "52" 很好理解，+ 运算符中只要有一个是字符串，就会变成字符串拼接操作。你不知道的是，- 运算符要求两个操作数都是数字，如果不是，会强制转换成数字，所以结果就变成了 5 - 2 = 3。

js 能表示的最大安全整数是 `2**53 - 1` 也就是 `Number.MAX_SAFE_INTEGER` === `9007199254740991`，最小安全整数是 `-9007199254740991` 因为有`-0`的存在，才会出现这种情况。`Number.MIN_VALUE`是大于 0 的最小浮点数。

<和>（大于号、小于号）的左结合，是从左到右比较；赋值运算符（++、--）是右结合，从右向左

`2 == [[[2]]]` 是 `true`，根据 ES5 规范，如果比较的两个值中有一个是数字类型，就会尝试将另外一个值强制转换成数字，再进行比较。

点运算符会被优先识别为数字常量的一部分，然后才是对象属性访问符。所以 `3.toString()` 实际上被 JS 引擎解析成 `(3.)toString()`，显然会出现语法错误。但是如果你这么写 `(3).toString()`，人为加上括号，这就是合法的。

每个字面的正则表达式都是一个单独的实例，即使它们的内容相同。

数组也是对象，ES5 规范指出如果两个对象进行相等比较，只有在它们指向同一个对象的情况下才会返回 true，其他情况都返回 false。而对象进行大小比较，会调用 toString 方法转成字符串进行比较，所以结果就变成了字符串 "1,2,3" 和 "1,2,4" 按照字典序进行比较了

arr.reduce() 有 4 个参数，1 个累积值 + 3 个 item idx arr

任何函数都是 Function 的实例，而 p 是函数 Person 的实例，Object.getPrototypeOf 会获取构造当前对象的原型。所以 Object.getPrototypeOf(p) === Person.prototype，而 Object.getPrototypeOf(Person) === Function.prototype

```js
function Person() {}
var p = new Person()

var a = p.__proto__
var b = Object.getPrototypeOf(p)
var c = Person.prototype
console.log(a === b, a === c, b === c)
// true, true, true

var d = Person.__proto__
var e = Object.getPrototypeOf(Person)
var f = Function.prototype
console.log(d === e, d === f, e === f)
// true, true, true
```

`foo.name = 'bar'` 函数名是禁止修改的，但这样不会报错

`String.prototype.replace(regexp|substr, newSubStr|function)` 的 function 有 3 个参数：查询出的值、对应下标、源字符串

```js
function f() {}

console.log(Function.prototype === Object.getPrototypeOf(f)) // true
```

你的正则加了 g 关系到 exec() 的执行：如果有 g，它会按照上一个匹配的位置继续执行，直到返回 null 了之后，Only invoke again, it will restart.

callback hell 虽然可以把函数分开写，但没有改变根本问题：

1. 嵌套函数耦合性高，一旦有所改动，就会牵一发而动全身
2. 不易处理错误

`next()` 如果不传参，yield 的返回值就是 undefined

```js
function* foo(x) {
  let y = 2 * (yield x + 1)
  let z = yield y / 3
  return x + y + z
}
let it = foo(5)
console.log(it.next()) // => {value: 6, done: false}
console.log(it.next(12)) // => {value: 8, done: false}
console.log(it.next(13)) // => {value: 42, done: true}
```

当我们在构造 Promise 的时候，构造函数内部的代码是立即执行的：promise 会先把同步代码全部执行完，再把第一个与 res 或 rej 相关的放到 event loop 中，后面就不会执行：

```js
const a = new Promise((res, rej) => {
  res('888')
  res('999')
  console.log(1)
  rej('e')
  console.log(2)
})

a.then(s => {
  console.log('th' + s)
}).catch(e => {
  console.log('er' + e)
})
// 1
// 2
// th888
```

如果你在 then 中 使用了 return，那么 return 的值会被 Promise.resolve() 包装

```js
Promise.resolve(1)
  .then(res => {
    console.log(res) // => 1
    return 2 // 包装成 Promise.resolve(2)
  })
  .then(res => {
    console.log(res) // => 2
  })
```

一个函数如果加上 async ，那么该函数就会返回一个 Promise

```js
async function test() {
  return '1'
}
console.log(test()) // -> Promise {<resolved>: "1"}
```

async function 中的异步 await 会同步执行，即只有第一个 await 执行完后，才会执行第二个。

```js
let a = 0
let b = async () => {
  a = a + (await 10)
  console.log('2', a) // -> '2' 10
}
b()
a++
console.log('1', a) // -> '1' 1
```

await 内部实现了 generator ，generator 会保留堆栈中东西，所以这时候 a = 0 被保存了下来

js 中 `[[a]]` 这种属性是干嘛的呢？ [这里](https://stackoverflow.com/questions/17174786/what-is-the-significance-of-the-double-brackets-for-the-prototype-property-i) ：These internal properties are not part of the ECMAScript language 内部属性，不能从外部引用

[基于 Promise 对象的自动执行](http://es6.ruanyifeng.com/#docs/generator-async#%E5%9F%BA%E4%BA%8E-Promise-%E5%AF%B9%E8%B1%A1%E7%9A%84%E8%87%AA%E5%8A%A8%E6%89%A7%E8%A1%8C) generator 自动执行器

```js
function run(gen) {
  var g = gen()

  function next(data) {
    var result = g.next(data)
    if (result.done) return result.value
    result.value.then(function(data) {
      next(data)
    })
  }

  next()
}

run(gen)
```

通常来说不建议使用 setInterval。第一，它和 setTimeout 一样，不能保证在预期的时间执行任务。第二，它存在执行累积的问题，即存在多个回调函数连续执行的情况。

简易 promise 实现

```js
const PENDING = 'pending'
const RESOLVED = 'resolved'
const REJECT = 'reject'

function MyPromise(fn) {
  const that = this
  that.state = PENDING
  that.value = null
  that.resolvedCallbacks = []
  that.rejectedCallbacks = []

  function resolve(value) {
    if (that.state === PENDING) {
      that.state = RESOLVED
      that.value = value
      that.resolvedCallbacks.map(cb => cb(that.value))
    }
  }

  function reject(value) {
    if (that.state === PENDING) {
      that.state = REJECT
      that.value = value
      that.rejectedCallbacks.map(cb => cb(that.value))
    }
  }

  try {
    fn(resolve, reject)
  } catch (e) {
    reject(e)
  }
}

MyPromise.prototype.then = function(onFulfilled, onRejected) {
  const that = this
  onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : v => v
  onRejected =
    typeof onRejected === 'function'
      ? onRejected
      : r => {
          throw r
        }
  if (that.state === PENDING) {
    that.resolvedCallbacks.push(onFulfilled)
    that.rejectedCallbacks.push(onRejected)
  }
  if (that.state === RESOLVED) {
    onFulfilled(that.value)
  }
  if (that.state === REJECT) {
    onRejected(that.value)
  }
}

new MyPromise((resolve, reject) => {
  setTimeout(() => {
    resolve(1)
  }, 1000)
}).then(value => {
  console.log(value)
})
```

在浏览器里，当一个事件发生且有一个事件监听器绑定在该事件上时，消息会被随时添加进队列。如果没有事件监听器，事件会丢失。所以点击一个附带点击事件处理函数的元素会添加一个消息，其它事件类似。

一个 web worker 或者一个跨域的 iframe 都有自己的栈，堆和消息队列。两个不同的运行时只能通过 postMessage 方法进行通信。

setTimeout 会比 Promise 后执行

process.nextTick 函数其实是独立于 Event Loop 之外的，它有一个自己的队列，当每个阶段完成后，如果存在 nextTick 队列，就会清空队列中的所有回调函数，并且优先于其他 microtask 执行。

实现 call 函数：其实就是在第一个参数上加一个 fn 函数，并调用，之后删了。

```js
Function.prototype.myCall = function(context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  const args = [...arguments].slice(1)
  const result = context.fn(...args)
  delete context.fn
  return result
}
```

在调用 new 的过程中会发生以上四件事情：

1. 新生成了一个对象
2. 链接到原型
3. 绑定 this
4. 返回新对象

`Number.prototype.toFixed()`会四舍五入，并且返回值是字符串

`Tree Shaking` 可以实现删除项目中未被引用的代码，如果你使用 `Webpack 4` 的话，开启生产环境就会自动启动这个优化功能。

用 `history.pushState` 和 `history.replaceState` 改变 URL，不会引起页面的刷新，只会更新浏览器的历史记录，当点击后退按钮时会触发 popState 事件

UDP 协议是面向无连接的，也就是说不需要在正式传递数据之前先连接起双方。

### 常见问题

_实习都干了什么_

我在 2 个地方实习过，中国航天时，维护过大型项目，了解了 Java web 相关技术，并且我也经常独自加班到 10 点以后，看书提升自身技术能力，之后秋招 10 月分左右，通过自身的努力，获得了字节跳动实习资格，在这期间主要使用 React 技术栈开发需求，也与很多厉害的人交流，更加明确了自己的目标。

_为什么实习没留下_

对于这个问题，我并不想编造什么理由。我确实参加了实习答辩，但是没有通过。我个人认为我的能力还有所欠缺，比如：总结能力，团队中的协作能力等。但经历了这个，我也深刻认识到了自己的不足，也在努力改进。

_http & s different_

_快速排序_

```js
const quickSort = arr => {
  if (arr.length <= 1) {
    return arr
  }

  const left = [],
    right = [],
    current = arr.splice(0, 1)

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] < current) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }
  return quickSort(left).concat(current, quickSort(right))
}

let a = []

for (let i = 0; i < 10; i++) {
  a[i] = Math.floor(Math.random() * 50)
}

console.log(a)

a = quickSort(a)

console.log(a)
```

### 0218 面试

position 有 6 个值：

1. `static` 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
2. `relative` 生成相对定位的元素，相对于其正常位置进行定位。**保留原来的空间**
3. `absolute` 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
4. `fixed` 生成绝对定位的元素，相对于浏览器窗口进行定位。 **尺寸不够也不会产生滚动条**
5. `inherit` 只从父元素继承 position 属性的值，不会管父级以上的 position
6. `sticky` 基于用户的滚动位置来定位。在 position:relative 与 position:fixed 定位之间切换

display

块级元素(block)特性：

- 总是独占一行，表现为另起一行开始，而且其后的元素也必须另起一行显示;
- 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制;

内联元素(inline)特性：

- 和相邻的内联元素在同一行;
- 宽度(width)、高度(height)、内边距的 top/bottom(padding-top/padding-bottom)和外边距的 top/bottom(margin-top/margin-bottom)都不可改变，就是里面文字或图片的大小;

![](flex.png)

#### 经典面试题 1

```js
/**
 * 从一个数组中找出 N 个数，其和为 M 的所有可能 https://mp.weixin.qq.com/s/2pJkk0avrTF3Vo1FEslRrQ
 * @param {Array} arr 所给数组
 * @param {number} count 用几个数组合
 * @param {number} sum 要寻找的合的值
 */
const search = (arr, count, sum) => {
  // 二进制中1的个数
  const amount = num => {
    let count = 0
    while (num) {
      num &= num - 1
      count++
    }
    return count
  }

  let len = arr.length
  let bit = 1 << len
  const res = []

  // 暴力遍历所有情况
  for (let i = 1; i < bit; i++) {
    if (amount(i) === count) {
      let s = 0
      const temp = []
      for (let j = 0; j < len; j++) {
        if ((i & (1 << j)) !== 0) {
          s += arr[j]
          temp.push(arr[j])
        }
      }

      if (s === sum) {
        res.push(temp)
      }
    }
  }
  return res
}

const arr = Array.from({ length: 10 }, (item, idx) => idx + 1)

console.log(arr)

console.log(search(arr, 3, 19))

// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
// [ [ 5, 6, 8 ],
//   [ 4, 7, 8 ],
//   [ 4, 6, 9 ],
//   [ 3, 7, 9 ],
//   [ 2, 8, 9 ],
//   [ 4, 5, 10 ],
//   [ 3, 6, 10 ],
//   [ 2, 7, 10 ],
//   [ 1, 8, 10 ] ]
```
