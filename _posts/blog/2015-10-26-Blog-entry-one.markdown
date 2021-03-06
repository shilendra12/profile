---
layout: post
title:  "Polyfills"
date:   2020-4-6 16:51:11
categories: blog
---
ForEach
```javascript
Array.prototype.myForEach = function(cb, thisArg){
      if(typeof cb !== 'function'){
        throw('not a function')
      }
      let thisArg = thisArg || window;
      for(var i = 0; i < this.length; i++){
       cb.call(thisArg, this[i], i, this);
      }
  }
```

Map
```javascript
  Array.prototype.myMap = function(cb, thisArg){
      if(typeof cb !== 'function'){
        throw('not a function')
      }
      let ob = Object(this)
      let arr = []
      let thisArg = thisArg || window;
      for(var i = 0; i < this.length; i++){
       arr.push (cb.call(thisArg, ob[i], i, ob));
      }
      return arr;
  }
```

Filter

``` javascript
  Array.prototype.myFilter = function(cb, thisArg){
      if(typeof cb !== 'function'){
        throw('not a function')
      }
      let ob = Object(this)
      let arr = []
      let thisArg = thisArg || window;
      for(var i = 0; i < this.length; i++){
        cb.call(thisArg, ob[i], i, ob) && arr.push (ob[i]);
      }
      return arr;
  }
```

Reduce
```javascript
  Array.prototype.myReduce = function(cb, thisArg){
      if(typeof cb !== 'function'){
        throw('not a function')
      }
      let ob = Object(this);
      let i = 1
      let acc = ob[0];
      if(arguments.length >= 2){
        acc = arguments[1];
        i = 0;
      }
      let arr = [];
      let thisArg = thisArg || window;
      for(i; i < this.length; i++){
        acc = cb.call(thisArg, acc, ob[i], i, ob)
      }
      return acc;
  }
```

Debounce
```
var myDebounce = (cb, wait) => {
  let timeInterval;
  return function (...args){
    let context = this;
    clearInterval(timeInterval);
    timeInterval = setTimeout(cb.apply(context,args),wait);
  }
}
```

Throttle 

```
var myThrottle = (cb, wait) => {
  let interval;
  return function (...args){
    let context = this;
    if(!interval){ 
      cb.apply(context, args);
      interval = true
      setTimeout(() => interval = false, wait)
    }
  }
}
```
