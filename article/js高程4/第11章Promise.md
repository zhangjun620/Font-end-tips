### Promise 、 异步


#### 《前端核心进阶》中的promise async await

1. 历史
  早期解决异步行为，只支持用回调函数来表明异步操作完成，这样会串联多个回调函数，形成了回调地狱。

2. new Promise(()=>()) 必须传入一个执行器函数，不提供会报错。
promise有三个状态 pending、resolved、rejected 待定、兑现、拒绝
无论落定为哪种状态都是不可逆的，


一般处理回调地狱会用到promise

 ##### setTimeout 执行时间的问题
  JS中任务分为同步和异步

  同步任务：当前主线程要消化执行的任务，这些任务一起形成执行栈

  异步任务：不进入主线程，而是进入任务队列，即不会马上进行的任务

  ` setTimeout(()=>{
    console.log('workou')
  },0）
    while(1){}
  `
  <br>
  这段代码不会得到任何输出，因为while循环会一直执行，而setTimeou执行任务时，是将内容放入任务队列中，继续执行同步任务。所以即使设置的0也要等主任务执行完毕再来。<br>
  ` function b(){
    setTimeout(()=>{console.log('1')},1);
    seTimeout(()=>{console.log('0')},0);}`<br>
  这段反而是输出 1，0 ，实际上这两个setTimeout谁先进入任务队列，谁就会先执行，并不会严格按照1ms和0ms区分。谁顺序靠前，谁先执行,在这种地方没必要钻牛角尖，只要清楚有这个概念就行了，这全依赖于规范制定和浏览器引擎的实现


**对于输出顺序这些问题，除了作用域，还需要知道同步代码与任务队列的顺序**

1. 在任务队列中，又分为宏任务，微任务。两个任务同时在队列中时，不管顺序，引擎会优先执行微任务。
2. 一般情况下宏任务包括： setTimeout、setInterval、i/o、事件、postMessage、requestAnimationFrame、UI渲染、setImmediate(nodejs中的特性，浏览器端废弃)
微任务包括： promise.then、MutationObserver、process.nextTick（nodejs）

