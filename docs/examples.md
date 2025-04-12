---
layout: page
title: Examples
permalink: /docs/examples/
---

# Colloquy Examples

This page provides examples of common use cases for Colloquy.

## Basic Example

A simple example demonstrating the core functionality:

```javascript
// Import the library
const colloquy = require('colloquy');

// Initialize a new instance
const app = colloquy.create();

// Configure options
app.configure({
  port: 3000,
  debug: true
});

// Start the application
app.start();
```

## Custom Plugins

Example showing how to use custom plugins:

```javascript
// Import the library
const colloquy = require('colloquy');
const customPlugin = require('./my-plugin');

// Initialize with plugins
const app = colloquy.create({
  plugins: [customPlugin]
});

// Use plugin features
app.use(customPlugin.middleware);

// Start the application
app.start();
```

## Advanced Configuration

Example with advanced configuration options:

```javascript
// Import the library
const colloquy = require('colloquy');

// Initialize with advanced configuration
const app = colloquy.create({
  name: 'my-chatbot',
  version: '1.0.0',
  port: 8080,
  middlewares: ['logger', 'security'],
  storage: {
    type: 'database',
    connection: {
      host: 'localhost',
      port: 5432,
      database: 'colloquy_db',
      user: 'admin',
      password: '********'
    }
  },
  logging: {
    level: 'info',
    format: 'json',
    destination: '/var/log/colloquy.log'
  }
});

// Start with custom callback
app.start(() => {
  console.log('Chatbot started successfully!');
});
```

## Command Line Usage

Example of using Colloquy from the command line:

```bash
# Initialize a new project
colloquy init --template basic

# Start development server
colloquy start --port 3000 --watch

# Build for production
colloquy build --minify --output ./dist

# Deploy application
colloquy deploy --target production
```

## Integration with Other Tools

Example showing integration with other popular tools:

```javascript
// Import libraries
const colloquy = require('colloquy');
const express = require('express');

// Create Express app
const expressApp = express();

// Create Colloquy instance
const app = colloquy.create();

// Integrate Express with Colloquy
app.use(expressApp);

// Add Express routes
expressApp.get('/api', (req, res) => {
  res.json({ status: 'ok' });
});

// Start both together
app.start();
```