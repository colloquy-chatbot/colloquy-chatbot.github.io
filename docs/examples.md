---
layout: page
title: Examples
permalink: /docs/examples/
---

# Project Examples

This page provides examples of common use cases for Project.

## Basic Example

A simple example demonstrating the core functionality:

```javascript
// Import the library
const project = require('project');

// Initialize a new instance
const app = project.create();

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
const project = require('project');
const customPlugin = require('./my-plugin');

// Initialize with plugins
const app = project.create({
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
const project = require('project');

// Initialize with advanced configuration
const app = project.create({
  name: 'advanced-app',
  version: '1.0.0',
  port: 8080,
  middlewares: ['logger', 'security'],
  storage: {
    type: 'database',
    connection: {
      host: 'localhost',
      port: 5432,
      database: 'project_db',
      user: 'admin',
      password: '********'
    }
  },
  logging: {
    level: 'info',
    format: 'json',
    destination: '/var/log/project.log'
  }
});

// Start with custom callback
app.start(() => {
  console.log('Application started successfully!');
});
```

## Command Line Usage

Example of using Project from the command line:

```bash
# Initialize a new project
project init --template basic

# Start development server
project start --port 3000 --watch

# Build for production
project build --minify --output ./dist

# Deploy application
project deploy --target production
```

## Integration with Other Tools

Example showing integration with other popular tools:

```javascript
// Import libraries
const project = require('project');
const express = require('express');

// Create Express app
const expressApp = express();

// Create Project instance
const app = project.create();

// Integrate Express with Project
app.use(expressApp);

// Add Express routes
expressApp.get('/api', (req, res) => {
  res.json({ status: 'ok' });
});

// Start both together
app.start();
```