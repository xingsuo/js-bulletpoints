## 1. How to check if array is empty / does not exist.
From [stackoverflow.com](https://stackoverflow.com/questions/24403732/check-if-array-is-empty-does-not-exist-js)

The problem with the example below is that it fails to address some scenarios, such as **null** values, other types of objects with a **length** property
```javascript
if (array === undefined || array.length === 0) {
    // array empty or does not exist
}
```
More proper example:
```javascript
if (!Array.isArray(array) || !array.length) {
    // array does not exist, is not an array, or is exmpty
}
```





## 2. How to handle **undefined** in Javascript
From [dmitripavlutin.com](https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/) by Dmitri Pavlutin

In Javascript:
```javascript
null == undefined // true
null === undefined // false
```
In other modern languages like Ruby, Python or Java have a single null value (**nil** or **null**)

**undefined**: when you try to access a variable or object property that is not yet initialized.
**null**: represents a missing object reference.

### 2.1 What is undefined?
 Javascript has **6** primitive types:
   - Boolean: true or false
   - Number: 1, 6.7, 0xFF
   - String: "Hello World"
   - Symbol: Symbol("name") (starting ES2015)
   - Null
   - Undefined
 - And a separated object type: {name: "max"}


```javascript
let number;
number; // undefined

let movie = { name: 'Interstellar' };
movie.year // undefined

let movies = [ 'Interstellar', 'Alexander' ];
movies[3]; // undefined
``` 
**typeof** works nicely to verify whether a variable contains an **undefined** value:
```javascript
typeof undefined === 'undefined'; // true

let nothing;
typeof nothing === 'undefined'; // true
```
### 2.2 Common scenarios that create **undefined**
- Uninitialized variable
    - Favor **const**, otherwise use **let**, but say goodbye to **var**
        - **const** declaration will create an *immutable binding.*
        - The problem of **var** is that you can declare a var variable somewhere at the end of the function scope, but still it can accessed before declaration: and you'll get an **undefined**.
    - Increase cohesion
- Accessing non-existing property
    - Check the property existence
        - obj.prop !== undefined
        - typeof obj.prop !== 'undefined'
        - obj.hasOwnProperty('prop')
        - 'prop' in obj (**recommended**)
    - Destructuring to access object properties
        - object destructuring in ES2015
        ```javascript
        const object = {  };  
        const { prop = 'default' } = object;  
        prop; 
        ```
        ```js
        function quote(str, config) {  
            const { char = '"', skipIfQuoted = true } = config;
            const length = str.length;
            if (skipIfQuoted
                && str[0] === char
                && str[length - 1] === char) {
                return str;
            }
            return char + str + char;
        }
        quote('Hello World', { char: '*' });        
        quote('"Welcome"', { skipIfQuoted: true });

        // Improved version
        function quote(str, { char = '"', skipIfQuoted = true } = {}) {  
            const length = str.length;
            if (skipIfQuoted
                && str[0] === char
                && str[length - 1] === char) {
                return str;
            }
            return char + str + char;
        }
        quote('Hello World', { char: '*' }); 
        quote('Sunny day');       
        ```
    - Fill the object with default properties
        - By using Javascript spread syntax or Object.assign()
        ```js
        const unsafeOptions = {  
            fontSize: 18
        };
        const defaults = {  
            fontSize: 16,
            color: 'black'
        };
        const options = {  
            ...defaults,
            ...unsafeOptions
        };
        options.fontSize; 
        options.color;    
        ```
- Function parameters
    > The function parameters implicitly default to undefined.
    ```js
    // Problem:
    function multiply(a, b) {  
        a; 
        b; 
        return a * b;
    }
    multiply(5); 
    ```
    - Use default parameter value
    ```js
    function multiply(a, b) {  
        if (b === undefined) {
            b = 2;
        }
        a; 
        b; 
        return a * b;
    }
    multiply(5); 

    // Improved solution by using ES2015 default paramethers feature.
    function multiply(a, b = 2) {  
        a; 
        b; 
        return a * b;
    }
    multiply(5);            
    multiply(5, undefined); 
    ```
- Function return value
    > Implicitly, without return statement, a JavaScript function returns undefined.
    ```js
    function square(x) {  
        const res = x * x;
    }
    square(2); // undefined
    ```
    - Don't trust the automatic semicolon insertion
- **void** operator
    - ***void expression*** evaluates the expression and returns ***undefined*** no matter the result of evaluation.

### 2.3 **undefined** in arrays
*  You get **undefined** when accessing an array element with an out of bounds index.
* When working with arrays, to escape catching undefined, be sure to use valid array indexes and avoid at all creating sparse arrays.
* Refer to No.1 to check How to check if array is empty / does not exist.

### 2.4 Difference between **undefined** and **null**
```js
typeof undefined; // undefined
typeof null;   // object
```

## 3. How to make a JS callback?
```js
function doHomework(subject, callback) {
  alert(`Starting my ${subject} homework.`);
  callback();
}

doHomework('math', function() {
  alert('Finished my homework');
});
```