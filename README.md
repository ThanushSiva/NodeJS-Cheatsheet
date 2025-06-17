# Nodejs

Node.js allows you to use JavaScript for backend development, file system operations, network programming, and building server applications. It's event-driven and uses non-blocking I/O operations, making it efficient for handling concurrent requests.

# Browser vs Node

<strong>Browser</strong>: Runs inside a web browser's JavaScript engine (V8 in Chrome, SpiderMonkey in Firefox, etc.)\
<strong>Node.js</strong>: Runs directly on your computer/server using V8 engine outside the browser

# Global Objects

# Browser

- <kbd>window</kbd> - global object and browser window\
- <kbd>document</kbd> - DOM manipulation\
- <kbd>localStorage</kbd>, <kbd>sessionStorage</kbd> - browser storage\
- <kbd>location</kbd>, <kbd>history</kbd> - navigation\
- <kbd>fetch()</kbd> - HTTP requests

# Nodejs

- <kbd>global</kbd> - global object\
- <kbd>process</kbd> - current Node.js process info\
- <kbd>__dirname</kbd>, <kbd>__filename</kbd> - current directory/file paths\
- <kbd>Buffer</kbd> - handle binary data\
- No DOM-related objects

# APIs

# browser

- DOM manipulation (getElementById, querySelector, etc.)
- Browser APIs (Geolocation, Camera, Notifications)
- Web APIs (WebSockets, Service Workers, Canvas)
- Limited file system access

# Nodejs

- File system operations (fs module)
- Network operations (http, https, net)
- Operating system utilities (os, path)
- Process management (child_process)
- Full file system access

# Module Systems

Node.js modules are reusable blocks of code that help organize and structure your applications.

# Types of Modules

- Built-in Modules : Come with Node.js installation
- Local Modules : Files you create in your project
- Third-party Modules : Installed via NPM

# Module Systems

# CommonJS-Traditional

```js
// Exporting (math.js)
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = {
  add,
  subtract
};

// Or export individual functions
module.exports.multiply = (a, b) => a * b;

// Importing
const math = require('./math');
const { add, subtract } = require('./math');

console.log(math.add(5, 3)); // 8
console.log(add(5, 3)); // 8
```

# ES Modules-Modern

```js
// Exporting (math.js)
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// Default export
export default function multiply(a, b) {
  return a * b;
}

// Importing
import { add, subtract } from './math.js';
import multiply from './math.js';
import * as math from './math.js';
```

Note: To use ES modules, add "type": "module" to your package.json or use .mjs file extension.

# Built-in Modules

- [path](./path/README.md)
- [fs](./fs/README.md)
- [http](./http/README.md)