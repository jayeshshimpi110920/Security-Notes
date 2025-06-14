## Good practice to have code review :
1) **Use const and let instead of var** => These keywords help to prevent accidental variable reassignment and improve code readability.
> const x = 5; // cannot be reassigned <br>
> let y = 10; // can be reassigned
2) **Use arrow functions**
> // ES5  
function add(x, y) {  
  return x + y;  
}  
// ES6  
const add = (x, y) => x + y;
3) **Use template literals**  
Template literals are a convenient way to concatenate strings and variables. They allow you to embed expressions inside backticks instead of using the concatenation operator (+).

> const name = 'John';  
console.log(`Hello, ${name}!`);



## Lookout for :
1) **`exec` function** which is used to execute commands in a shell and buffer the output. The `exec` function is a common source of **command injection vulnerabilities** in Node.js applications. => lookout/search for `exec`
