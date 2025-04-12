---
layout: page
title: Examples
permalink: /docs/examples/
---

# Colloquy Examples

This page provides examples of common use cases for Colloquy.

## Basic Example

A simple example demonstrating the core functionality:

{% capture tab_typescript %}
```typescript
// Import the library
import { create } from 'colloquy';

// Initialize a new instance
const app = create();

// Configure options
app.configure({
  port: 3000,
  debug: true
});

// Start the application
app.start();
```
{% endcapture %}

{% capture tab_python %}
```python
# Import the library
from colloquy import create

# Initialize a new instance
app = create()

# Configure options
app.configure({
  "port": 3000,
  "debug": True
})

# Start the application
app.start()
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

## Custom Plugins

Example showing how to use custom plugins:

{% capture tab_typescript %}
```typescript
// Import the library
import { create } from 'colloquy';
import customPlugin from './my-plugin';

// Initialize with plugins
const app = create({
  plugins: [customPlugin]
});

// Use plugin features
app.use(customPlugin.middleware);

// Start the application
app.start();
```
{% endcapture %}

{% capture tab_python %}
```python
# Import the library
from colloquy import create
from my_plugin import custom_plugin

# Initialize with plugins
app = create(
  plugins=[custom_plugin]
)

# Use plugin features
app.use(custom_plugin.middleware)

# Start the application
app.start()
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

## Advanced Configuration

Example with advanced configuration options:

{% capture tab_typescript %}
```typescript
// Import the library
import { create } from 'colloquy';

// Initialize with advanced configuration
const app = create({
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
{% endcapture %}

{% capture tab_python %}
```python
# Import the library
from colloquy import create

# Initialize with advanced configuration
app = create({
  "name": "my-chatbot",
  "version": "1.0.0",
  "port": 8080,
  "middlewares": ["logger", "security"],
  "storage": {
    "type": "database",
    "connection": {
      "host": "localhost",
      "port": 5432,
      "database": "colloquy_db",
      "user": "admin",
      "password": "********"
    }
  },
  "logging": {
    "level": "info",
    "format": "json",
    "destination": "/var/log/colloquy.log"
  }
})

# Start with custom callback
def on_start():
    print("Chatbot started successfully!")

app.start(on_start)
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

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

{% capture tab_typescript %}
```typescript
// Import libraries
import { create } from 'colloquy';
import express from 'express';

// Create Express app
const expressApp = express();

// Create Colloquy instance
const app = create();

// Integrate Express with Colloquy
app.use(expressApp);

// Add Express routes
expressApp.get('/api', (req, res) => {
  res.json({ status: 'ok' });
});

// Start both together
app.start();
```
{% endcapture %}

{% capture tab_python %}
```python
# Import libraries
from colloquy import create
from flask import Flask, jsonify

# Create Flask app
flask_app = Flask(__name__)

# Create Colloquy instance
app = create()

# Add Flask routes
@flask_app.route('/api')
def api_endpoint():
    return jsonify({"status": "ok"})

# Integrate Flask with Colloquy
app.use(flask_app)

# Start both together
app.start()
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}