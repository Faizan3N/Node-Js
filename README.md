# 🟢 Node.js Important Points


## 📌 Table of Contents

1. [What is Node.js?](#what-is-nodejs)
2. [How Node.js Works](#how-nodejs-works)
3. [Core Modules](#core-modules)
4. [npm & package.json](#npm--packagejson)
5. [File System (fs)](#file-system-fs)
6. [HTTP Module](#http-module)

---

## What is Node.js?

- **Node.js** is a runtime environment that lets you run JavaScript **outside the browser**, on the server side.
- Built on **Chrome's V8 JavaScript engine**.
- Uses an **event-driven, non-blocking I/O model** — making it fast and lightweight.
- Great for building: REST APIs, real-time apps, CLI tools, microservices.

```bash
# Check Node.js version
node -v

# Run a JavaScript file
node app.js
```

### Key Concepts
| Term | Meaning |
|------|---------|
| **Non-blocking** | Node doesn't wait for I/O to complete; it moves on |
| **Callback** | Function called when an async task finishes |
| **Event Emitter** | Node's built-in pub/sub mechanism |
| **Single-threaded** | One thread, but async tasks offloaded via libuv |

---

## Core Modules

Node.js comes with built-in modules — no installation needed.

```js
const fs   = require('fs');       // File system
const path = require('path');     // File paths
const os   = require('os');       // OS info
const http = require('http');     // Create HTTP servers
const url  = require('url');      // URL parsing
const events = require('events'); // Event emitter
```

> ⚠️ In modern Node.js you can also use **ES Modules**:
> ```js
> import fs from 'fs';
> ```
> Add `"type": "module"` in `package.json` to enable this.

---

## npm & package.json

### Essential Commands

```bash
npm init -y                  # Create package.json with defaults
npm install express          # Install a package (saved to dependencies)
npm install nodemon --save-dev  # Dev-only dependency
npm uninstall express        # Remove a package
npm update                   # Update all packages
npm run <script>             # Run a script defined in package.json
npx <tool>                   # Run a package without installing globally
```

### package.json Explained

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

> 💡 Always add `node_modules/` to your `.gitignore` file.

---

## File System (fs)

```js
const fs = require('fs');

// ✅ Read file (async)
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

// ✅ Write file (async)
fs.writeFile('output.txt', 'Hello World', (err) => {
  if (err) throw err;
  console.log('File written!');
});

// ✅ Using Promises (cleaner)
const fs = require('fs').promises;

async function readFile() {
  const data = await fs.readFile('file.txt', 'utf8');
  console.log(data);
}
```

## HTTP Module

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello from Node.js!');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000');
});
```
