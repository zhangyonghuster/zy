ECMA6新特性
+ let 布局，块作用域
+ 变量赋值

  `
let [foo, [[bar], baz]] = [1, [[2], 3]];
  `

  只要某种数据结构具有Iterator接口，都可以采用数组形式的结构赋值。
  可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。

+ 字符串Unicode表示法
  flag属性，为正则表达式新增了flag属性，会返回正则表达式的修饰符。

+ 数组的转换
  ```
  let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
  };

  // ES5的写法
  var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

  // ES6的写法
  let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
  ```

  + =>的用法
  下面代码中有多少个this

  ```
  function foo() {
    return () => {
      return () => {
        return () => {
          console.log(`id:`, this.id);
        };
      };
    };
  }

  var f = foo.call({id: 1});

  var t1 = f.call({id: 2})()(); // id: 1
  var t2 = f().call({id: 3})(); // id: 1
  var t3 = f()().call({id: 4}); // id: 1
  ```

  上面代码中只有一个this，就是函数foo的this，所以所有的输出都是一样的。
