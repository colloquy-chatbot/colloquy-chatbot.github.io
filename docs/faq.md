---
layout: page
title: FAQ
permalink: /docs/faq/
---

# Frequently Asked Questions

## General Questions

### What is Colloquy?

Colloquy is an open source library that provides a clean, consistent interface for working with different chatbot APIs. It simplifies the process of building applications with large language models by handling the low-level details of API communication, conversation history, and function calling.

### When should I use Colloquy?

Colloquy is ideal for developers who:
- Wish to get up and running quickly with an LLM
- Want to build applications that use multiple LLM providers (like OpenAI and Claude)
- Need to let chatbots call application functions to retrieve data or perform actions
- Want to reduce boilerplate code when working with chatbot APIs
- Prefer strong typing and a clean, consistent API

### Which chatbot providers are supported?

Currently, Colloquy supports:
- OpenAI's ChatGPT
- Anthropic's Claude

We plan to add support for more providers in the future based on community feedback.

## Installation & Setup

### How do I install Colloquy?

{% capture typescript_install %}
```bash
npm install colloquy_chatbot
```
{% endcapture %}

{% capture python_install %}
```bash
pip install colloquy_chatbot
```
{% endcapture %}

{% include tabs.html group="install" names="TypeScript|Python" typescript=typescript_install python=python_install %}

### How do I set up API keys?

Colloquy looks for API keys in your environment variables. We recommend using a `.env` file or your environment's secret management system.

Required environment variables depend on which providers you want to use:

```bash
# For OpenAI
OPENAI_API_KEY=your_openai_key_here

# For Claude
ANTHROPIC_API_KEY=your_anthropic_key_here
```

You can also pass API keys directly in code, but this is not recommended for security reasons.

## Usage Questions

### How do I switch between different chatbot providers?

Switching between providers is as simple as using a different bot class:

{% capture typescript_switch %}
```typescript
import { OpenAIBot, ClaudeBot } from "colloquy_chatbot"

// Use OpenAI
const openaiBot = new OpenAIBot()
const openaiResponse = await openaiBot.prompt("Hello")

// Use Claude
const claudeBot = new ClaudeBot()
const claudeResponse = await claudeBot.prompt("Hello")
```
{% endcapture %}

{% capture python_switch %}
```python
from colloquy_chatbot import OpenAIBot, ClaudeBot

# Use OpenAI
openai_bot = OpenAIBot()
openai_response = await openai_bot.prompt("Hello")

# Use Claude
claude_bot = ClaudeBot()
claude_response = await claude_bot.prompt("Hello")
```
{% endcapture %}

{% include tabs.html group="switching" names="TypeScript|Python" typescript=typescript_switch python=python_switch %}

### How does conversation history work?

Colloquy automatically manages conversation history for you. Each prompt is added to the conversation history, along with the response. This context is used for subsequent prompts.

The conversation history is maintained within the bot instance. If you need to start a fresh conversation, create a new bot instance.

## Function Calling

### How does function calling work in Colloquy?

Colloquy simplifies function calling by automatically handling the conversion between your code functions and the format expected by the LLM API. The basic steps are:

1. Define your functions
2. Wrap them using `PromptFunction` (TypeScript) or `@prompt_function` (Python)
3. Pass them to the bot constructor
4. Use the bot normally - it will call your functions when appropriate

See the [Function Calling section](/docs/getting-started/#function-calling) in the Getting Started guide for examples.

### What types of parameters are supported?

Colloquy supports all standard JSON types for function parameters:
- Strings
- Numbers
- Booleans
- Arrays
- Objects
- null

Type information can be inferred from default values in your function definitions.

### Do I need to handle the function calls manually?

No, Colloquy handles the entire function calling flow automatically:
1. Sends your function definitions to the LLM
2. Recognizes when the LLM wants to call a function
3. Calls your function with the parameters from the LLM
4. Sends the function results back to the LLM
5. Returns the final response

This happens transparently when you call `bot.prompt()`.

## Troubleshooting

### I'm getting "No API key provided" errors

Make sure you've set the appropriate environment variables:
- `OPENAI_API_KEY` for OpenAI
- `ANTHROPIC_API_KEY` for Claude

### My function isn't being called correctly

Common issues with function calling:
1. **Parameter naming**: Make sure parameter names match between your function definition and how they're referred to in prompts
2. **Type issues**: The LLM might provide data in a different format than expected
3. **Specificity**: Make your function descriptions clear and specific about when they should be used
4. **Context**: Ensure your prompt gives enough context for the LLM to know when to use the function

### How do I report bugs or request features?

Please open an issue on our GitHub repositories:
- [TypeScript Implementation](https://github.com/colloquy-chatbot/colloquy/issues)
- [Python Implementation](https://github.com/colloquy-chatbot/colloquy-python/issues)

Include as much detail as possible: steps to reproduce, expected vs. actual behavior, and your environment details.
