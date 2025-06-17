# fs

The fs (File System) module is one of the most important built-in modules in Node.js, allowing you to work with files and directories on your system.

# Table of Contents

- [Basic Usage](#basic-usage)
- [Reading Files](#reading-files)
  - [Asynchronous](#asynchronous)
  - [Synchronous](#synchronous)
  - [Promise-based](#promise-based)
- [Writing Files](#writing-files)
  - [Basic Writing](#basic-writing)
- [Appending to Files](#appending-to-files)
- [Working with Directories](#working-with-directories)
- [File-Directory Information](#file-directory-information)
- [File Operations](#file-operations)
- [Watching Files-Directories](#watching-files-directories)
- [Error Handling](#error-handling)

# Basic Usage

```js
const fs = require('fs');
// For promise-based operations
const fsPromises = require('fs').promises;
// or
const fs = require('fs/promises');
```

# Reading Files

# Asynchronous

```js
// Read entire file
fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log(data);
});

// Read binary file
fs.readFile('image.jpg', (err, data) => {
  if (err) throw err;
  console.log('File size:', data.length, 'bytes');
});
```

# Synchronous

```js
try {
  const data = fs.readFileSync('data.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error('Error:', err);
}
```

# Promise-based

```js
async function readFile() {
  try {
    const data = await fsPromises.readFile('data.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error:', err);
  }
}
```

# Writing Files

# Basic Writing

```js
// Asynchronous
fs.writeFile('output.txt', 'Hello World!', 'utf8', (err) => {
  if (err) throw err;
  console.log('File saved!');
});

// Synchronous
fs.writeFileSync('output.txt', 'Hello World!', 'utf8');

// Promise-based
await fsPromises.writeFile('output.txt', 'Hello World!', 'utf8');
```

# Appending to Files

```js
fs.appendFile('log.txt', 'New log entry\n', (err) => {
  if (err) throw err;
  console.log('Log entry added!');
});
```

# Working with Directories

```js
// Create directory
fs.mkdir('new-folder', (err) => {
  if (err && err.code !== 'EEXIST') throw err;
  console.log('Directory created!');
});

// Create nested directories
fs.mkdir('path/to/nested/folder', { recursive: true }, (err) => {
  if (err) throw err;
});

// Read directory contents
fs.readdir('.', (err, files) => {
  if (err) throw err;
  console.log('Files:', files);
});

// Remove directory
fs.rmdir('folder-name', (err) => {
  if (err) throw err;
  console.log('Directory removed!');
});

// Remove directory and contents (Node.js 14.14+)
fs.rm('folder-name', { recursive: true, force: true }, (err) => {
  if (err) throw err;
});
```

# File-Directory Information

```js
// Check if file/directory exists
fs.access('file.txt', fs.constants.F_OK, (err) => {
  if (err) {
    console.log('File does not exist');
  } else {
    console.log('File exists');
  }
});

// Get file stats
fs.stat('file.txt', (err, stats) => {
  if (err) throw err;
  
  console.log('Is file:', stats.isFile());
  console.log('Is directory:', stats.isDirectory());
  console.log('File size:', stats.size, 'bytes');
  console.log('Created:', stats.birthtime);
  console.log('Modified:', stats.mtime);
});
```

# File Operations

```js
// Copy file
fs.copyFile('source.txt', 'destination.txt', (err) => {
  if (err) throw err;
  console.log('File copied!');
});

// Rename/move file
fs.rename('old-name.txt', 'new-name.txt', (err) => {
  if (err) throw err;
  console.log('File renamed!');
});

// Delete file
fs.unlink('file-to-delete.txt', (err) => {
  if (err) throw err;
  console.log('File deleted!');
});
```

# Watching Files-Directories

```js
// Watch for file changes
fs.watchFile('config.txt', (curr, prev) => {
  console.log('File changed!');
  console.log('Previous size:', prev.size);
  console.log('Current size:', curr.size);
});

// Watch directory
fs.watch('.', (eventType, filename) => {
  console.log(`Event: ${eventType}, File: ${filename}`);
});
```

# Error Handling

Common error codes:

- <kbd>ENOENT</kbd> - File/directory doesn't exist
- <kbd>EACCES</kbd> - Permission denied
- <kbd>EEXIST</kbd> - File/directory already exists
- <kbd>EISDIR</kbd> - Expected file but found directory
- <kbd>ENOTDIR</kbd> - Expected directory but found file