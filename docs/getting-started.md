---
layout: page
title: Getting Started
permalink: /docs/getting-started/
---

# Getting Started with Colloquy

This guide will help you install Colloquy and get up and running quickly.

## Prerequisites

Before installing Colloquy, make sure you have the following prerequisites:

{% capture tab_typescript %}
- Node.js (v14 or later)
- npm (v7 or later)
{% endcapture %}

{% capture tab_python %}
- Python (v3.8 or later)
- pip (latest version)
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

## Installation

### npm

The easiest way to install Colloquy is via npm:

{% capture tab_typescript %}
```bash
npm install -g colloquy
```
{% endcapture %}

{% capture tab_python %}
```bash
pip install colloquy
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

### From Source

You can also install Colloquy from source:

{% capture tab_typescript %}
```bash
# Clone TypeScript repository
git clone https://github.com/colloquy-chatbot/colloquy.git
cd colloquy
npm install
npm run build
npm link
```
{% endcapture %}

{% capture tab_python %}
```bash
# Clone Python repository
git clone https://github.com/colloquy-chatbot/colloquy-python.git
cd colloquy-python
pip install -e .
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

## Basic Configuration

After installation, you'll need to set up a basic configuration file:

{% capture tab_typescript %}
```bash
colloquy init
```

This will create a `colloquy.config.json` file in your current directory with default settings.
{% endcapture %}

{% capture tab_python %}
```bash
colloquy init
```

This will create a `colloquy.yaml` file in your current directory with default settings.
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

## Your First Project

Let's create a simple project to demonstrate the basic functionality:

{% capture tab_typescript %}
```bash
mkdir my-chatbot-ts
cd my-chatbot-ts
colloquy init
colloquy start
```
{% endcapture %}

{% capture tab_python %}
```bash
mkdir my-chatbot-py
cd my-chatbot-py
colloquy init
colloquy start
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

## Next Steps

- Explore the [API Reference](/docs/api) to learn about available commands
- Check out the [Examples](/docs/examples) for common use cases
- Read the [FAQ](/docs/faq) for answers to common questions