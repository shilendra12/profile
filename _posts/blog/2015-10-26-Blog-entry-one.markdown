---
layout: post
title:  "Polyfills"
date:   2015-10-26 16:51:11
categories: blog
---
Array.prototype.myForEach = function(cb, thisArg){
      if(typeof cb !== 'function'){
        throw('not a function')
      }
      let thisArg = thisArg || window;
      for(var i = 0; i < this.length; i++){
       cb.call(thisArg, this[i], i, this);
      }
  }


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
