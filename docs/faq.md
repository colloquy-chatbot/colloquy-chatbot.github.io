---
layout: page
title: FAQ
permalink: /docs/faq/
---

# Frequently Asked Questions

## General Questions

### What is Colloquy?

Colloquy is an open source conversational AI tool designed to help create engaging chat experiences. It provides a streamlined framework for building, training, and deploying chatbots.

### Who should use Colloquy?

Colloquy is ideal for developers and organizations who want to build sophisticated conversational interfaces, chatbots, or dialogue systems without extensive AI expertise.

### Is Colloquy free to use?

Yes, Colloquy is open source and free to use under the MIT License. You can use it for both personal and commercial projects.

## Installation

### Why am I getting permission errors during installation?

If you're seeing permission errors when installing Colloquy globally, you might need to use sudo or adjust your npm permissions:

```bash
sudo npm install -g colloquy
```

Alternatively, you can configure npm to install global packages in your user directory without requiring sudo:

```bash
npm config set prefix ~/.npm-global
```

Then add `export PATH=~/.npm-global/bin:$PATH` to your `~/.profile` or `~/.bashrc`.

### How do I update Colloquy to the latest version?

To update Colloquy to the latest version, run:

```bash
npm update -g colloquy
```

## Configuration

### Where should I put my configuration file?

The configuration file (`colloquy.config.json`) should be placed in the root directory of your project. You can also specify a custom location using the `--config` flag.

### Can I use environment variables in my configuration?

Yes, Colloquy supports using environment variables in your configuration file. Use the syntax `${ENV_VAR_NAME}` and the values will be replaced at runtime.

## Troubleshooting

### Colloquy won't start - what should I check?

If Colloquy won't start, check the following:

1. Verify that your configuration file is valid JSON
2. Check for port conflicts (another service might be using the same port)
3. Review the console output for error messages
4. Check system requirements (Node.js version, etc.)

### How do I debug Colloquy?

To enable debug logging, use the `--verbose` flag when running Colloquy commands:

```bash
colloquy start --verbose
```

You can also set the environment variable `DEBUG=colloquy:*` to see all debug logs.

## Contributing

### How can I contribute to Colloquy?

We welcome contributions! Start by checking out our [contribution guidelines](https://github.com/colloquy-chatbot/colloquy/blob/main/CONTRIBUTING.md). You can help by:

1. Reporting bugs
2. Suggesting new features
3. Improving documentation
4. Submitting pull requests

### Where can I get help if I'm stuck?

If you're stuck or have questions, you can:

1. Check the [documentation](/docs/)
2. Open an issue on [GitHub](https://github.com/colloquy-chatbot/colloquy/issues)
3. Join our [Discord community](https://discord.gg/colloquy)
4. Ask a question on [Stack Overflow](https://stackoverflow.com/questions/tagged/colloquy) with the 'colloquy' tag