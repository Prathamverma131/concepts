# AMA Session 6th July
## 1. What is the difference between (==) and (===) operator?
- '==' Checks the value of the variable
- '===' Checks the value as well as **datatype** of the Variable.

    Example:
    ```
    let number = 7;
    let string = "7";
    console.log(number == string);
    console.log(number === string); 
    ```
    Output:
    ```
    true
    false
    ```

## 2. console.log(typeof []) is equals to 'object' why?
- Arrays in JavaScript are considered objects because they exhibit key characteristics of objects, such as:
    1. **Properties:** Arrays can have properties (like length) and methods (like push() and pop()).
    2. **Dynamic Nature:** Arrays can dynamically grow or shrink in size, unlike traditional arrays in some other programming languages which have fixed sizes.
    3. **Indexed Elements:** Array elements are stored in properties with names that are integers (indices), and these indices are used to access the elements.
- Array is inherited from 'Array.prototype'. This inheritance mechanism is fundamental featuere of object-oriented design.

## 3. Whats are the disadvantages of using closure?
- **Memory Consumption:** Closures keep the outer function's scope alive in memory even after the outer function has finished executing. This can lead to increased memory consumption.
- **Performance Overhead:** Each closure maintains a separate scope chain, which can impact lookup times.
- **Difficulties in Debugging:** Closures can make debugging more challenging, especially in complex applications with deeply nested functions and closures.

## 4. Why using global variables are bad in js?
- Global variables can be read or modified by any part of the program, making it difficult to remember or reason about every possible use.
- Global names are available everywhere. You may unknowingly end up using a global when you think you are using a local (by misspelling or forgetting to declare the local) or vice versa.
- When dynamically linking modules, it can be unclear whether different libraries have their own instances of globals or whether the globals are shared.
## 5. How to extract certain properties from an array of objects to create a new array?
- Using map() function we can extract certain property from array of objects.
    
    Example:
    ```
    const array = [
        {name:"Pikachu", color:"Yellow"},
        {name:"Bulbasaur", color:"Green"},
        {name:"ElectBuzz", color:"Yellow"},
        {name:"Mewtwo", color:"Pink"},
        {name:"Charizard", color:"Yellow"},
    ]
    function color_array(array){
        const colorArray=array.map((elem)=>{
            return elem.color;
        });
        return colorArray
    }
    console.log(color_array(array))
    ```
    Outputs:
    ```
    ['Yellow', 'Green', 'Yellow', 'Pink', 'Yellow']
    ```
## 6. Difference between charAt() and at() method in js?
- The charAt() method is used to retrieve the character at a specified index within a string.
- Syntax: string.charAt(index)
    Where index is is a zero based integer.
- charAt() returns the character at the specified index. If the index is out of range (i.e., less than 0 or greater than or equal to the length of the string), an empty string  is returned.
        
    Example:
    ```
    const string = "India";
    console.log(string.charAt(0));
    console.log(string.charAt(4));
    console.log(string.charAt(-3));
    console.log(string.charAt(10));
    ```
    Outputs:
    ```
    I
    4


    ```
- The at() method is used to retrieve the element at a specified index.
- The at() accepts negative index.
- The at() returns 'undefined' when index is out of range.
- **Syntax:** array.at(index)

    Example:
    ```
    const string = "India";
    console.log(string.at(0));
    console.log(string.at(4));
    console.log(string.at(-3));
    console.log(string.at(10));
    ```
    Ouputs:
    ```
    I
    a
    d
    undefined
    ```

## 7. How to reset initial or 1st commit in git, if its possible?
- Initial commit cannot be deleted, in order to delete it, we need to delete the branch.
- If we want to delete the main/master branch, git won't allow it, as it is the primary and only branch in git repo. In order to create the primary branch we need to do the following.
    ```
    git branch -m master old_master
    git checkout --orphan master
    git branch -D old_master
    ```
    'git branch -m master old_master' will rename the master branch to old_master.

    'git checkout --orphan master' will create a new branch that start from empty states with no prior commits. 

    Once another primary branch is created, git won't restrict deleting 'old_master' branch.

    'git branch -D old_master' will delete the branch.

## 8. console.log(typeof []) returns 'object', then why can not we use (.) operator in array to accesss its values just like objects,where we use (.) operator in objects for accessing key and values.
- In JavaScript, both arrays and objects are types of objects.
- Arrays in JavaScript are special types of objects that have numeric keys (indexes) and a length property.
- Objects in JavaScript are collections of key-value pairs  where keys are strings or numbers.
- Dot notation (.) is used to access properties of objects where the property name is a valid identifier. A valid identifier in JavaScript starts with a letter or underscore (_) or a dollar sign ($).
- Since array keys are integers and integers are not a valid identifier, we use bracket notation ([]).
## 9. Why 'forEach' loop skips 'not defined' whereas 'for' loop gives 'undefined'?
- 'forEach' loops iterates over an array by its elements, but 'for' loop iterates over an error by its index.
## 10. How can we mimic the action array.splice() and 'array.slice()' on objcts.
- Objects have custom named keys, where as array keys are in integers. Also are not ordered collection of like arrays so operations like slice() or splice() does not work
-  The customised functions for objects mimicing slice() and splice() are as follows.
```
const pokemon = {name:"Pikachu", color:"Yellow", power:"electric", size: "1 foot"};
function sliced(object, startIndex, endIndex){
    if (typeof object !== "object" || Array.isArray(object)){
        console.log("Object required");
        return;
    }
    const keys = Object.keys(object)
    const new_object = {}
    if (!endIndex){
        endIndex = keys.length;
    }
    if (endIndex > startIndex){
        for (let key of keys.slice(startIndex, endIndex)){
            new_object[key]=object[key];
        }
    }
    return new_object;
}
console.log(sliced(pokemon,0,1));
console.log(pokemon); //Original object is not changed
```
Outputs:
```
{name: 'Pikachu'}
{name: 'Pikachu', color: 'Yellow', power: 'electric', size: '1 foot'}
```
spliced()
```
function spliced(object, startIndex, endIndex){
    if (typeof object !== "object" || Array.isArray(object)){
        console.log("Object required");
        return;
    }
    const keys = Object.keys(object)
    const new_object = {}
    if (!endIndex){
        endIndex = keys.length;
    }
    if (endIndex > startIndex){
        for (let key of keys.slice(startIndex, endIndex)){
            new_object[key] = object[key];
            delete object[key];
        }
    }
    return new_object;
}
console.log(spliced(pokemon,0,1));
console.log(pokemon); //Original object is not changed
```
Outputs:
```
{name: 'Pikachu'}
{color: 'Yellow', power: 'electric', size: '1 foot'}
```


## 11. What is "Callback Hell" problem and how to avoid it?
- "Callback hell" is a term used to describe a situation in JavaScript programming where multiple nested callbacks make the code difficult to read, understand, and maintain. It typically occurs when dealing with asynchronous operations that depend on each other or require sequential execution.
- To avoid callback hell
    - **Promises:** Promises provide a cleaner and more structured way to handle asynchronous operations, allowing you to chain operations and handle errors more effectively.
    - **Using Await:** Async functions and the 'await' keyword provide a more readable and sequential way to write asynchronous code.
    - **Modularize Code:** Break down complex logic into smaller, more manageable functions. This helps reduce nesting and improves code organization.
## 12. From the following program
- file1.js
    ```
    let ar = [1, 2, 3];
    console.log("Hello");
    module.exports = ar;
    ```
- file2.js
    ```
    const ar = require('./file1.js')
    console.log(ar);
    ```
    Output: 
    ```
    Hello
    [1, 2, 3]
    ```
## From above program why "Hello" is also printing? When 'ar' is imported.
- When we use 'import' or 'require' to bring in variables or functions from another file, JavaScript treats the imported file as a module.
- The file is executed in its own scope, and any statements such as console.log statements or variable initializations within the module is executed.
- ES6 modules are designed to initialize and run immediately upon import, which ensures that dependencies are correctly managed and initialized before they are used.
- We can avoid these side effects by removing log staments, or wrapping it inside a function.
