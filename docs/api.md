---
layout: page
title: API Reference
permalink: /docs/api/
---

# API Reference

This page documents the full API for Project.

## Command Line Interface

### Global Options

| Option | Description |
| ------ | ----------- |
| `--help`, `-h` | Display help information |
| `--version`, `-v` | Display version information |
| `--config <path>` | Specify configuration file path |
| `--verbose` | Enable verbose output |

### Commands

#### `project init`

Initializes a new project with default configuration.

```bash
project init [options]
```

Options:

| Option | Description |
| ------ | ----------- |
| `--template <name>` | Use a specific template |
| `--force` | Overwrite existing configuration |

#### `project start`

Starts the project in development mode.

```bash
project start [options]
```

Options:

| Option | Description |
| ------ | ----------- |
| `--port <port>` | Specify port number (default: 3000) |
| `--host <host>` | Specify host (default: localhost) |

#### `project build`

Builds the project for production.

```bash
project build [options]
```

Options:

| Option | Description |
| ------ | ----------- |
| `--output <dir>` | Specify output directory |
| `--minify` | Enable minification |

## Configuration Reference

Project uses a JSON configuration file (`project.config.json`) to customize behavior.

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "port": 3000,
  "plugins": ["plugin-a", "plugin-b"],
  "options": {
    "debug": false,
    "timeout": 5000
  }
}
```

### Configuration Options

| Option | Type | Description |
| ------ | ---- | ----------- |
| `name` | string | Project name |
| `version` | string | Project version |
| `port` | number | Development server port |
| `plugins` | array | List of plugins to use |
| `options` | object | Additional configuration options |