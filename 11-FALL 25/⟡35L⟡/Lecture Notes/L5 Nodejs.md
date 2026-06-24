# Fundamentals
*ex.* creates a simple web server on port 8080 that displays "Hello World!"
``` js
let http = require('http');  
http.createServer(function (req, res) {  
  res.writeHead(200, {'Content-Type': 'text/html'});  
}).listen(8080);
```

## Variables and functions
```js
// Variables (let, const, var)  
let name = 'Node.js';  
const version = 20;  
  
// Function declaration  
function greet(user) {  
  return `Hello, ${user}!`; // Template literal (ES6)  
}  
  
// Arrow function (ES6+)  
const add = (a, b) => a + b;  
  
console.log(greet('Developer')); // Hello, Developer!  
console.log(add(5, 3)); // 8
```
## Objects and arrays
```js
// Object  
const user = {  
  name: 'Alice',  
  age: 25,  
  greet() {  
    console.log(`Hi, I'm ${this.name}`);  
  }  
};  
  
// Array  
const colors = ['red', 'green', 'blue'];  
  
// Array methods (ES6+)  
colors.forEach(color => console.log(color));  
const lengths = colors.map(color => color.length);
```

## Asynchronous JavaScript
```js
// 1. Callbacks (traditional)  
function fetchData(callback) {  
  setTimeout(() => {  
    callback('Data received!');  
  }, 1000);  
}  
  
// 2. Promises (ES6+)  
const fetchDataPromise = () => {  
  return new Promise((resolve) => {  
    setTimeout(() => resolve('Promise resolved!'), 1000);  
  });  
};  
  
// 3. Async/Await (ES8+)  
async function getData() {  
  const result = await fetchDataPromise();  
  console.log(result);  
}  
  
getData(); // Call the async function
```
- the callback function is passed as a parameter to `fetchData`, which calls the callback function after a delay with the parameter `'Data received!'`.
## Destructuring & Template Literals
```js
const { name } = user;  
console.log(`Hello, ${name}!`);
```

## Differences from browser
```js
// Global objects
global.mylet = 42;  
console.log(global.mylet); // 42

// File Access
const fs = require('fs');  
fs.readFile('myfile.txt', 'utf8', (err, data) => {  
  if (err) throw err;  
  console.log(data);  
});

// HTTP Requests
const https = require('https');  
https.get('https://example.com', res => {  
  let data = '';  
  res.on('data', chunk => data += chunk);  
  res.on('end', () => console.log(data));  
});

// Modules
const fs = require('fs');
```

## Command Line
```
# Run a JavaScript file  
node app.js  
  
# Run with additional arguments  
node app.js arg1 arg2  
  
# Run in watch mode (restarts on file changes)  
node --watch app.js
```

### Using the REPL
```js
> const name = 'Node.js';  
> console.log(`Hello, ${name}!`);  
> .help // Show available commands  
> .exit // Exit REPL
```

### Access command line arguments 
- using `process.argv`
```js
// args.js  
console.log('All arguments:', process.argv);  
console.log('First argument:', process.argv[2]);  
console.log('Second argument:', process.argv[3]);  
  
// Example usage:  
// node args.js hello world  
// Output:  
// All arguments: ['/path/to/node', '/path/to/args.js', 'hello', 'world']  
// First argument: hello  
// Second argument: world
```

### Access and set environment variables
```js
// env.js  
console.log('Environment:', process.env.NODE_ENV || 'development');  
console.log('Custom variable:', process.env.MY_VARIABLE);  
console.log('Database URL:', process.env.DATABASE_URL || 'Not set');  
  
// Example usage with environment variables:  
// NODE_ENV=production MY_VARIABLE=test node env.js
```

While running:
```
# Set environment variables when running  
NODE_ENV=production MY_VARIABLE=test node env.js
```

## Node Architecture
Node.js uses a **single-threaded, event-driven** architecture that is designed to handle many connections at once, efficiently and without blocking the main thread.

**1. Client Request Phase**
- Clients send requests to the Node.js server
- Each request is added to the **Event Queue**

**2. Event Loop Phase**
- The Event Loop continuously checks the **Event Queue**
- Picks up requests one by one in a loop

**3. Request Processing**
- Simple (non-blocking) tasks are handled immediately by the main thread
- Complex/blocking tasks are offloaded to the Thread Pool

**4. Response Phase**
- When blocking tasks complete, their callbacks are placed in the **Callback Queue**
- Event Loop processes callbacks and sends responses

### Non-blocking file read
```js
const fs = require('fs');  
console.log('Before file read');  
fs.readFile('myfile.txt', 'utf8', (err, data) => {  
  if (err) throw err;  
  console.log('File contents:', data);  
});  
console.log('After file read');
```
- `After file read` is printed before the file contents

### Blocking vs. non-blocking
```js
// Blocking code example  
console.log('Start of blocking code');  
const data = fs.readFileSync('myfile.txt', 'utf8'); // Blocks here  
console.log('Blocking operation completed');  
  
// Non-blocking code example  
console.log('Start of non-blocking code');  
fs.readFile('myfile.txt', 'utf8', (err, data) => {  
  if (err) throw err;  
  console.log('Non-blocking operation completed');  
});  
console.log('This runs before the file is read');
```

## Event Loop
- handles asynchronous operations by delegating tasks to the system and processing their results through callbacks

Node.js follows these steps to handle operations:
1. Execute the main script (synchronous code)
2. Process any microtasks (Promises, `process.nextTick`)
3. Execute timers (`setTimeout`, `setInterval`)
4. Run I/O callbacks (file system, network operations)
5. Process `setImmediate` callbacks
6. Handle close events (like `socket.on('close')`)

```js
console.log('First');  
setTimeout(() => console.log('Third'), 0);  
Promise.resolve().then(() => console.log('Second'));  
console.log('Fourth');
```
1. Sync code runs first ('First', 'Fourth')
2. Microtasks (Promises) run before the next phase ('Second')
3. Timers execute last ('Third')

# Asynchronous
**Asynchronous** operations let your program do other work while waiting for tasks like file I/O or network requests to complete.
