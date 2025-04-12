---
layout: page
title: Getting Started
permalink: /docs/getting-started/
---

# Getting Started with Colloquy

This guide will help you install Colloquy and get up and running quickly.

## Prerequisites

Before installing Colloquy, make sure you have the following prerequisites:

- Node.js (v14 or later)
- npm (v7 or later)

## Installation

### npm

The easiest way to install Colloquy is via npm:

```bash
npm install -g colloquy
```

### From Source

You can also install Colloquy from source:

```bash
git clone https://github.com/colloquy-chatbot/colloquy.git
cd colloquy
npm install
npm run build
npm link
```

## Basic Configuration

After installation, you'll need to set up a basic configuration file:

```bash
colloquy init
```

This will create a `colloquy.config.json` file in your current directory with default settings.

## Your First Project

Let's create a simple project to demonstrate the basic functionality:

```bash
mkdir my-chatbot
cd my-chatbot
colloquy init
colloquy start
```

## Next Steps

- Explore the [API Reference](/docs/api) to learn about available commands
- Check out the [Examples](/docs/examples) for common use cases
- Read the [FAQ](/docs/faq) for answers to common questions