---
layout: page
title: FAQ
permalink: /docs/faq/
---

# Frequently Asked Questions

## General Questions

### What is Project?

Project is an open source tool designed to help developers solve common problems efficiently. It provides a streamlined workflow for setting up, developing, and deploying applications.

### Who should use Project?

Project is ideal for developers who want to automate repetitive tasks, standardize their development workflows, and increase productivity.

### Is Project free to use?

Yes, Project is open source and free to use under the MIT License. You can use it for both personal and commercial projects.

## Installation

### Why am I getting permission errors during installation?

If you're seeing permission errors when installing Project globally, you might need to use sudo or adjust your npm permissions:

```bash
sudo npm install -g project
```

Alternatively, you can configure npm to install global packages in your user directory without requiring sudo:

```bash
npm config set prefix ~/.npm-global
```

Then add `export PATH=~/.npm-global/bin:$PATH` to your `~/.profile` or `~/.bashrc`.

### How do I update Project to the latest version?

To update Project to the latest version, run:

```bash
npm update -g project
```

## Configuration

### Where should I put my configuration file?

The configuration file (`project.config.json`) should be placed in the root directory of your project. You can also specify a custom location using the `--config` flag.

### Can I use environment variables in my configuration?

Yes, Project supports using environment variables in your configuration file. Use the syntax `${ENV_VAR_NAME}` and the values will be replaced at runtime.

## Troubleshooting

### Project won't start - what should I check?

If Project won't start, check the following:

1. Verify that your configuration file is valid JSON
2. Check for port conflicts (another service might be using the same port)
3. Review the console output for error messages
4. Check system requirements (Node.js version, etc.)

### How do I debug Project?

To enable debug logging, use the `--verbose` flag when running Project commands:

```bash
project start --verbose
```

You can also set the environment variable `DEBUG=project:*` to see all debug logs.

## Contributing

### How can I contribute to Project?

We welcome contributions! Start by checking out our [contribution guidelines](https://github.com/username/project/blob/main/CONTRIBUTING.md). You can help by:

1. Reporting bugs
2. Suggesting new features
3. Improving documentation
4. Submitting pull requests

### Where can I get help if I'm stuck?

If you're stuck or have questions, you can:

1. Check the [documentation](/docs/)
2. Open an issue on [GitHub](https://github.com/username/project/issues)
3. Join our [Discord community](https://discord.gg/project)
4. Ask a question on [Stack Overflow](https://stackoverflow.com/questions/tagged/project) with the 'project' tag