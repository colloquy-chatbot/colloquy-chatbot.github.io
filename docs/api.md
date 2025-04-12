---
layout: page
title: API Reference
permalink: /docs/api/
---

# API Reference

This page documents the full API for Colloquy.

## Command Line Interface

### Global Options

| Option | Description |
| ------ | ----------- |
| `--help`, `-h` | Display help information |
| `--version`, `-v` | Display version information |
| `--config <path>` | Specify configuration file path |
| `--verbose` | Enable verbose output |

### Commands

#### `colloquy init`

Initializes a new project with default configuration.

{% capture tab_typescript %}
```bash
colloquy init [options]
```
{% endcapture %}

{% capture tab_python %}
```bash
colloquy init [options]
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

Options:

| Option | Description |
| ------ | ----------- |
| `--template <name>` | Use a specific template |
| `--force` | Overwrite existing configuration |

#### `colloquy start`

Starts the project in development mode.

{% capture tab_typescript %}
```bash
colloquy start [options]
```
{% endcapture %}

{% capture tab_python %}
```bash
colloquy start [options]
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

Options:

| Option | Description |
| ------ | ----------- |
| `--port <port>` | Specify port number (default: 3000) |
| `--host <host>` | Specify host (default: localhost) |

#### `colloquy build`

Builds the project for production.

{% capture tab_typescript %}
```bash
colloquy build [options]
```
{% endcapture %}

{% capture tab_python %}
```bash
colloquy build [options]
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

Options:

| Option | Description |
| ------ | ----------- |
| `--output <dir>` | Specify output directory |
| `--minify` | Enable minification |

## Configuration Reference

Colloquy uses configuration files to customize behavior - JSON for TypeScript and YAML for Python.

{% capture tab_typescript %}
```json
{
  "name": "my-chatbot",
  "version": "1.0.0",
  "port": 3000,
  "plugins": ["plugin-a", "plugin-b"],
  "options": {
    "debug": false,
    "timeout": 5000
  }
}
```
{% endcapture %}

{% capture tab_python %}
```yaml
name: my-chatbot
version: 1.0.0
port: 3000
plugins:
  - plugin-a
  - plugin-b
options:
  debug: false
  timeout: 5000
```
{% endcapture %}

{% include tabs.html tabs="TypeScript|Python" content=tab_typescript|tab_python %}

### Configuration Options

| Option | Type | Description |
| ------ | ---- | ----------- |
| `name` | string | Project name |
| `version` | string | Project version |
| `port` | number | Development server port |
| `plugins` | array | List of plugins to use |
| `options` | object | Additional configuration options |