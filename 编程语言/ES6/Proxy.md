# Proxy代理


`Proxy`对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。

对目标对象的操作之前提供了拦截，可以对外界的操作进行过滤和改写，修改某些操作的默认行为，这样我们可以不直接操作对象本身，而是通过操作对象的**代理对象**来间接来操作对象，达到预期的目的

```js
let proxy = new Proxy(target, handler);
```

>  参数 `target` 是用 `Proxy` 包装的目标对象（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）, 参数 `handler` 也是一个对象，其属性是当执行一个操作时定义代理的行为的函数，也就是自定义的行为。

`Proxy` 的基本用法就如同上面这样，不同的是 `handler` 对象的不同，`handler` 可以是空对象 `{}` ，则表示对 `proxy` 操作就是对目标对象 `target` 操作

`handler` **不能** 设置为 `null` ，会抛出一个错误——`Cannot create proxy with a non-object as target or handler`！

## API

- **handler.get(target,property,receiver)**

  用于拦截对象的读取属性操作，`target` 是指目标对象，`property` 是被获取的属性名 ， `receiver` 是 `Proxy` 或者继承 `Proxy` 的对象，一般情况下就是 `Proxy` 实例。

  ```JS
  let proxy = new Proxy({},{
      get : function (target,prop) {
          console.log(`get ${prop}`);
          return 10;
      }
  })
      
  console.log(proxy.a)    // get a
                          // 10
  ```

  

- **handler.set(target, property, value, receiver)**

  用于拦截设置属性值的操作，参数于 `get` 方法相比，多了一个 `value` ，即要设置的属性值

  ```JS
  let obj = {};
  Object.defineProperty(obj, "count", {
      configurable: false,
      enumerable: false,
      value: 10,
      writable: false
  });
  
  let proxy = new Proxy(obj,{
      set : function (target,prop,value) {
          target[prop] = 20;
      }
  })
  
  proxy.count = 20 ;
  console.log(proxy.count)   // 10
  ```

  

- **.apply(target, thisArg, argumentsList)**

  用于拦截函数的调用，共有三个参数，分别是目标对象（函数）`target`，被调用时的上下文对象 `thisArg` 以及被调用时的参数数组 `argumentsList`，该方法可以返回任何值。

  ```js
  function sum(a, b) {
  	return a + b;
  }
  
  const handler = {
      apply: function(target, thisArg, argumentsList) {
      	console.log(`Calculate sum: ${argumentsList}`); 
      	return target(argumentsList[0], argumentsList[1]) * 2;
      }
  };
  
  let proxy = new Proxy(sum, handler);
  
  console.log(sum(1, 2));     // 3
  console.log(proxy(1, 2));   // Calculate sum：1,2
                              // 6
  ```

  

- **handler.construct(target, argumentsList, newTarget)**

  `construct` 用于拦截 `new` 操作符，为了使 `new` 操作符在生成的 `Proxy`对象上生效，用于初始化代理的目标对象自身必须具有`[[Construct]]`内部方法；它接收三个参数，目标对象 `target` ，构造函数参数列表 `argumentsList` 以及最初实例对象时，`new` 命令作用的构造函数，即下面例子中的 `p`。

  ```js
  let p = new Proxy(function() {}, {
      construct: function(target, argumentsList, newTarget) {
      	console.log(newTarget === p );                          // true
      	console.log('called: ' + argumentsList.join(', '));     // called：1,2
      	return { value: ( argumentsList[0] + argumentsList[1] )* 10 };
      }
  });
  
  console.log(new p(1,2).value);      // 30
  ```

  

- **handler.has(target,prop)**

  `has`方法可以看作是针对 `in` 操作的钩子，当我们判断对象是否具有某个属性时，这个方法会生效，典型的操作就是 `in` ,改方法接收两个参数 目标对象 `target` 和 要检查的属性 `prop`，并返回一个 `boolean` 值。

  ```js
  let p = new Proxy({}, {
      has: function(target, prop) {
      	if( prop[0] === '_' ) {
      		console.log('it is a private property')
      		return false;
      	}
      	return true;
      }
  });
  
  console.log('a' in p);      // true
  console.log('_a' in p )     // it is a private property
                              // false
  ```

## 参考

https://juejin.im/post/5bfcbab0518825741e7bd67f
  
