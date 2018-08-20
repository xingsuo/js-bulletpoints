```js
new Promise( /* executor */ function(resolve, reject) { ... } );
```
Three states:
* pending
* fuifilled
* rejected

```js
var p = new Promise(function(resolve, reject){
    //做一些异步操作
    setTimeout(function(){
        console.log('finish');
        resolve('Some data');
    }, 2000);
});
```
In the example above, although we just created the Promise, the function we passed into has been executed. Usually we need to put the Promise inside a function, and run the function whenever we need it.
```js
function runAsync(){
    var p = new Promise(function(resolve, reject){
        //做一些异步操作
        setTimeout(function(){
            console.log('finish');
            resolve('Some data');
        }, 2000);
    });
    return p;            
}
runAsync();
```
Why we need to wrap the promise in a function and what's the purpose of 'resolve'?
```js
runAsync().then(function(data){
    console.log(data);
    //Do something by using data
    //......
});
```
It's similiar to js callback function. But for the scenario which we need use 'callback of callback', it's easier to chain all those together by using Promise. It's a way to simplify callback functions.
```js
function runAsync(callback){
    setTimeout(function(){
        console.log('finish');
        callback('Some data');
    }, 2000);
}

runAsync(function(data){
    console.log(data);
});
```


From [Juejin.im](https://juejin.im/post/5b5577916fb9a04fb900d2e1)