
# NodeJS/React
- NodeJS allows you to run JS outside the browser
- Node programming model
	- Single-threaded
	- Event-based programming
	- Non-blocking
- NPM: Node package manager
	- Allows you to install node packages and store in `package.json`
## Node.js
### Syntax
```js
// iterates through colors and logs each value
colors.forEach(color => console.log(color));

// creates a new array containing each color.length
const lengths = colors.map(color => color.length);
```

**Accessing command-line arguments**
Example usage:  
`node args.js hello world  `
Output:  
All arguments: `['/path/to/node', '/path/to/args.js', 'hello', 'world']`
First argument: `hello`  
Second argument: `world`
### Non-blocking patterns
**Callbacks**
```js
fs.readFile('data.txt', 
	(err, data) => {
		if (err) throw err;
		console.log(data.toString());
	}
);

console.log('This runs before the file is read');
```
- Function is passed as an argument `(err, data) => { ... }` to run after another finishes

**Promises**
```js
fetch('/api')
	.then(res => res.json()) // this runs after network response
	.then(console.log)
	.catch(console.error)
```
- Represents a value that will exist in the future
- `fetch` returns a Promise, and Node runs other code while waiting
	- When the response arrives, `.then()` chains run in order

**Async/Await**
```js
async function load() {
	const res = await fetch('/api'); // pauses only this function
	const data = await res.json();
	console.log(data);
}
```
- `await` pauses only **inside** the async function and not the whole program
- Meanwhile the rest of the event loop continues executing

### Node.js examples

**Basic HTTP Server**
```js
const http = require('http'); // import built-in HTTP module

const server = http.createServer((req, res) => { // create a server, callback runs on each request
	res.writeHead(200, { 'Content-Type': 'text/plain' }); // set response status code and headers
	res.end('Hello World'); // response body and end
});

server.listen(3000, () => console.log('Server running on port 3000')); // start server on port 3000
```

**Express server with JSON**
```js
const express = require('express'); // import express library
const app = express(); // create express application
app.use(express.json()); // middleware to parse JSON bodies

app.get('/hello', (req, res) => res.json({ msg: 'Hi' }); // handle GET request to '/hello', respond with JSON
app.post('/echo', (req, res) => res.json(req.body)); // handle POST request to '/echo', respond with JSON body sent by client

app.listen(3000); // start server on 3000
```

**HTTP requests**
```js
const fetch = require('node-fetch'); // import fetch library

async function getData() {
  const res = await fetch('https://api.example.com/data'); // send GET request and wait for response
  const data = await res.json(); // parse response as JSON and wait for parsing 
  console.log(data); // log parsed JSON data
}

getData();
```
## React
- **Virtual DOM**: React keeps an internal copy of the UI, and when states change, it compares to the actual DOM and only updates the necessary parts
	- State variables stored using `useState`, cannot directly change them and must use the setter function
- **React components** are defined as functions with a single return element
	- Inputs are called *props*
	- `export default` makes it accessible to outside modules
### SPA vs. SSR
- **Single Page Application (SPA)** are structured as a single HTML page, no preloaded content
	- Content loaded *dynamically* through JS
	- Initial load time is slower, but everything is more responsive
- **Server-side rendering (SSR)**: fully rendered page
	- Faster initial load time (only current page sent)
	- Better search engine optimization
	- Requires more server compute, longer response time for user interaction
### Syntax examples
**Arrow functions**
```js
// normal
function add(a, b) { return a + b; }

// arrow functions
const add = (a, b) => a + b;
```

**Attributes (Props in JSX)**
```jsx
<Component propName={value} />

<myButton text ="Save" disabled={isSaving} onClick={saveData} />
```
- Props can become function parameters

**Array methods**
```js
// spread
const nums = [1, 2, 3];
const newNums = [...nums, 4];

// slice(start,end) returns shallow copy without modifying
nums.slice(1,3); // [2, 3]
```
### Example with Node
**Node.js backend (Express)**
```js
const express = require('express');
const cors = require('cors'); // needed if React runs on a different port
const app = express();

app.use(cors());
app.use(express.json());

// API for GET
app.get('/api/message', (req, res) => {
	res.json({ msg: 'Hello' });
});

// API for POST
app.post('/api/echo', (req, res) => {
	res.json({ received: req.body });
});

app.listen(5000, () => console.log('Server running on 5000'));
```

**React Frontend**
```js
import { useEffect, useState } from 'react';

function Message() {
	const [msg, setMsg] = useState('');
	
	useEffect(() => {
		fetch('http://localhost:5000/api/message')
			.then(res => res.json())
			.then(data => setMsg(data.msg))
			.catch(console.error);
	}, []);
	
	return <>{msg}</>;
}

function Echo() {
	const [input, setInput] = useState('');
	const [response, setResponse] = useState('');
	
	const send = async () => {
		const res = await fetch('http://localhost:5000/api/echo', {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({ text: input })
		});
		
		return (
			<>
				<input value={input} onChange{e => setInput(e.target.value)} />
				<button onClick={send}>Send</button>
				<div>Server says: {response}</div>
			</>
		);
	}
}
```

- Node package manager (NPM)
	- Manages Node.js libraries, including installation and dependencies
	- Stores metadata file listening dependencies, scripts, and project info in `package.json`
		- Must always commit `package.json` and `package-lock.json`
	- `npm install` reinstalls all dependencies