# Morgan Middleware

### Purpose:

Morgan is an HTTP request logger middleware for Node.js applications, particularly those built with Express.js. It logs details about incoming requests, such as HTTP methods, URLs, status codes, and response times, aiding in monitoring and debugging. 
EXPRESSJS.COM

### When to Use Morgan Middleware:

- **Development Environments**: To monitor HTTP requests and responses for debugging purposes.
- **Production Environments**: To maintain logs of client interactions, which can be useful for analyzing usage patterns and troubleshooting issues.

### Implementing Morgan Middleware in Express.js with ES6 Modules:

To integrate Morgan into an Express.js application using modern JavaScript (ES6 modules), follow these steps:

### 1. Install Morgan:

First, install Morgan using npm:

```bash
npm install morgan
```

### 2. Import Morgan and Express:

Import the necessary modules using ES6 `import` statements:

```javascript
import express from 'express';
import morgan from 'morgan';
```

### 3. Create the Express Application:

Initialize your Express application:

```javascript
const app = express();
```

### 4. Use Morgan Middleware:

Apply Morgan as middleware to your Express application. Morgan provides several predefined formats for logging:

- **'combined'**: Standard Apache combined log output.
- **'common'**: Standard Apache common log output.
- **'dev'**: Concise output colored by response status for development use.
- **'short'**: Shorter than 'common' but more information than 'tiny'.
- **'tiny'**: Minimal output.

For example, to use the 'dev' format:

```javascript
app.use(morgan('dev'));
```

### 5. Create a Custom Token:

Morgan allows the creation of custom tokens to log additional request information. For example, to log the hostname:

```javascript
morgan.token('host', (req) => req.hostname);
app.use(morgan(':method :url :status :host - :response-time ms'));
```

### 6. Write Logs to a File:

To write logs to a file instead of the console, use Node.js's fs module:

```javascript
import fs from 'fs';
import path from 'path';

const __dirname = path.resolve();
const accessLogStream = fs.createWriteStream(path.join(__dirname, 'access.log'), { flags: 'a' });

app.use(morgan('combined', { stream: accessLogStream }));
```

### 7. Start the Server:

Set up your server to listen on a specified port:

```javascript
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

### Conclusion:

Integrating Morgan into your Express.js application provides a straightforward method for logging HTTP requests, enhancing your ability to monitor and debug your application. By customizing Morgan's configurations, you can tailor the logging to fit the specific needs of your application, thereby maintaining efficient and informative logs.