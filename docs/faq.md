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

{% capture tab_typescript %}
```bash
sudo npm install -g colloquy
```
{% endcapture %}

{% capture tab_python %}
```bash
sudo pip install colloquy
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

{% capture tab_typescript %}
Alternatively, you can configure npm to install global packages in your user directory without requiring sudo:

```bash
npm config set prefix ~/.npm-global
```

Then add `export PATH=~/.npm-global/bin:$PATH` to your `~/.profile` or `~/.bashrc`.
{% endcapture %}

{% capture tab_python %}
Alternatively, you can install packages to your user directory without requiring sudo:

```bash
pip install --user colloquy
```

Or create and use a virtual environment:

```bash
python -m venv venv
source venv/bin/activate
pip install colloquy
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

### How do I update Colloquy to the latest version?

To update Colloquy to the latest version, run:

{% capture tab_typescript %}
```bash
npm update -g colloquy
```
{% endcapture %}

{% capture tab_python %}
```bash
pip install --upgrade colloquy
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

## Configuration

### Where should I put my configuration file?

{% capture tab_typescript %}
The configuration file (`colloquy.config.json`) should be placed in the root directory of your project. You can also specify a custom location using the `--config` flag.
{% endcapture %}

{% capture tab_python %}
The configuration file (`colloquy.yaml`) should be placed in the root directory of your project. You can also specify a custom location using the `--config` flag.
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

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

{% capture tab_typescript %}
```bash
colloquy start --verbose
```
{% endcapture %}

{% capture tab_python %}
```bash
colloquy start --verbose
```
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

{% capture tab_typescript %}
You can also set the environment variable `DEBUG=colloquy:*` to see all debug logs.
{% endcapture %}

{% capture tab_python %}
You can also enable debug logging in your configuration file by setting `logging.level: debug` or use the environmental variable `COLLOQUY_LOG_LEVEL=debug`.
{% endcapture %}

{% include tabs.html names="TypeScript|Python" typescript=tab_typescript python=tab_python %}

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