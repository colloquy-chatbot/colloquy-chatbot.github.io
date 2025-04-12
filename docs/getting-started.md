---
layout: page
title: Getting Started
permalink: /docs/getting-started/
---

# Getting Started with Project

This guide will help you install Project and get up and running quickly.

## Prerequisites

Before installing Project, make sure you have the following prerequisites:

- Node.js (v14 or later)
- npm (v7 or later)

## Installation

### npm

The easiest way to install Project is via npm:

```bash
npm install -g project
```

### From Source

You can also install Project from source:

```bash
git clone https://github.com/username/project.git
cd project
npm install
npm run build
npm link
```

## Basic Configuration

After installation, you'll need to set up a basic configuration file:

```bash
project init
```

This will create a `project.config.json` file in your current directory with default settings.

## Your First Project

Let's create a simple project to demonstrate the basic functionality:

```bash
mkdir my-project
cd my-project
project init
project start
```

## Next Steps

- Explore the [API Reference](/docs/api) to learn about available commands
- Check out the [Examples](/docs/examples) for common use cases
- Read the [FAQ](/docs/faq) for answers to common questions