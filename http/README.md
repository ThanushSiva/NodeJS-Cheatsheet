# http

The HTTP module is a core Node.js module that enables you to create HTTP servers and make HTTP requests.

# Table of Contents

- [Creating a Server](#creating-a-server)
- [Request Object](#request-object)
- [Response Object](#response-object)
- [Simple Routing](#simple-routing)
- [Post Method](#post-method)
- [Notes](#notes)

# Key Concepts

# Creating a Server

- Use <kbd>http.createServer()</kbd> with a callback function
- The callback receives <kbd>request</kbd> and <kbd>response</kbd> objects
- Call <kbd>server.listen(port)</kbd> to start the server

```js
const http = require('http');

// BASIC SERVER
const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World!');
});

server.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

# Request Object

- <kbd>req.method</kbd> - HTTP method (GET, POST, PUT, DELETE)
- <kbd>req.url</kbd> - The requested URL path
- <kbd>req.headers</kbd> - Object containing request headers
- <kbd>req.on('data')</kbd> - Listen for incoming data chunks
- <kbd>req.on('end')</kbd> - Triggered when request data is complete

```js
const serverWithDetails = http.createServer((req, res) => {
    console.log('Method:', req.method);      // GET, POST, etc.
    console.log('URL:', req.url);            // /path/to/resource
    console.log('Headers:', req.headers);    // Request headers object
    
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end(`
        <h1>Request Details</h1>
        <p><strong>Method:</strong> ${req.method}</p>
        <p><strong>URL:</strong> ${req.url}</p>
        <p><strong>User-Agent:</strong> ${req.headers['user-agent']}</p>
    `);
});
```

# Response Object

- <kbd>res.writeHead(statusCode, headers)</kbd> - Set status and headers
- <kbd>res.setHeader(name, value)</kbd> - Set individual headers
- <kbd>res.write(data)</kbd> - Write data to response
- <kbd>res.end(data)</kbd> - End response (optionally with data)

```js
const responseMethodsServer = http.createServer((req, res) => {
    // Set status code and headers
    res.statusCode = 200;
    res.setHeader('Content-Type', 'application/json');
    
    // Or use writeHead for both
    // res.writeHead(200, { 'Content-Type': 'application/json' });
    
    // Send data
    res.write('{"message": "Hello"}');
    res.write('{"status": "success"}');
    
    // End response
    res.end();
});
```

# Simple Routing

```js
const routingServer = http.createServer((req, res) => {
    const url = req.url;
    const method = req.method;
    
    if (url === '/' && method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>Home Page</h1>');
    } 
    else if (url === '/about' && method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>About Page</h1>');
    }
    else if (url === '/api/data' && method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: 'API data', timestamp: Date.now() }));
    }
    else {
        res.writeHead(404, { 'Content-Type': 'text/html' });
        res.end('<h1>404 - Page Not Found</h1>');
    }
});
```

# Post Method

```js
const postServer = http.createServer((req, res) => {
    if (req.method === 'POST') {
        let body = '';
        
        // Collect data chunks
        req.on('data', (chunk) => {
            body += chunk.toString();
        });
        
        // Process when complete
        req.on('end', () => {
            console.log('Received data:', body);
            
            res.writeHead(200, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ 
                message: 'Data received', 
                receivedData: body 
            }));
        });
    } else {
        res.writeHead(405, { 'Content-Type': 'text/plain' });
        res.end('Method Not Allowed');
    }
});
```

# Notes

- Always call <kbd>res.end()</kbd> to complete the response
- Handle errors with <kbd>try-catch</kbd> and error event listeners
- Use <kbd>https</kbd> module for HTTPS requests
- The HTTP module is low-level; consider Express.js for complex applications