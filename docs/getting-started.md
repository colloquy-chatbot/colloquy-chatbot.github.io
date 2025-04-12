---
layout: page
title: Getting Started
permalink: /docs/getting-started/
---

# Getting Started with Colloquy

Colloquy provides a clean, consistent interface for working with different chatbot libraries. This guide will help you get started quickly.

## Installation

Install Colloquy using your preferred package manager:

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

{% include tabs.html group="installation" names="TypeScript|Python" typescript=typescript_install python=python_install %}

## Prerequisites

To use Colloquy effectively, you'll need:

1. An API key for at least one supported chatbot service:
   - OpenAI (for ChatGPT)
   - Anthropic (for Claude)

2. Environment variables set up for your API keys:

{% capture typescript_env %}
```bash
# Add to your .env file or environment
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
```
{% endcapture %}

{% capture python_env %}
```bash
# Add to your .env file or environment
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
```
{% endcapture %}

{% include tabs.html group="env-setup" names="TypeScript|Python" typescript=typescript_env python=python_env %}

## Basic Usage

Here's a simple example to get you started with either OpenAI's GPT or Anthropic's Claude:

{% capture typescript_basic %}
```typescript
import { OpenAIBot, ClaudeBot } from "colloquy_chatbot"

// Choose which bot to use
const bot = new OpenAIBot()
// Or: const bot = new ClaudeBot()

// Send a message and get a response
const response = await bot.prompt("Hello, can you help me with a question?")
console.log(response) // "How can I help you?"

// Continue the conversation
const followUp = await bot.prompt("What is Colloquy?")
console.log(followUp) // "Colloquy is a chatbot library..."
```
{% endcapture %}

{% capture python_basic %}
```python
from colloquy_chatbot import OpenAIBot, ClaudeBot

# Choose which bot to use
bot = OpenAIBot()
# Or: bot = ClaudeBot()

# Send a message and get a response
response = await bot.prompt("Hello, can you help me with a question?")
print(response) # "How can I help you?"

# Continue the conversation
follow_up = await bot.prompt("What is Colloquy?")
print(follow_up) # "Colloquy is a chatbot library..."
```
{% endcapture %}

{% include tabs.html group="basic-usage" names="TypeScript|Python" typescript=typescript_basic python=python_basic %}

## Providing Instructions

You can guide the bot's behavior by providing system instructions during initialization:

{% capture typescript_instructions %}
```typescript
import { OpenAIBot } from "colloquy_chatbot"

// Create bot with specific instructions
const bot = new OpenAIBot({
  instructions: "You are a helpful assistant specialized in JavaScript. Keep responses concise."
})

// The bot will follow these instructions
const response = await bot.prompt("How do I sort an array?")
console.log(response) // "Use array.sort() method..."
```
{% endcapture %}

{% capture python_instructions %}
```python
from colloquy_chatbot import OpenAIBot

# Create bot with specific instructions
bot = OpenAIBot(
    instructions="You are a helpful assistant specialized in Python. Keep responses concise."
)

# The bot will follow these instructions
response = await bot.prompt("How do I sort a list?")
print(response) # "Use list.sort() method..."
```
{% endcapture %}

{% include tabs.html group="instructions" names="TypeScript|Python" typescript=typescript_instructions python=python_instructions %}

## Function Calling

One of Colloquy's most powerful features is the ability to let the chatbot call functions to retrieve information or perform actions:

{% capture typescript_functions %}
```typescript
import { ClaudeBot, PromptFunction } from "colloquy_chatbot"

// Define a function for the bot to use
function getWeather(location: string, unit: string = "celsius") {
  // In a real app, this would call a weather API
  return `Weather in ${location}: 22°${unit === "celsius" ? "C" : "F"}, Sunny`
}

// Create bot with access to this function
const bot = new ClaudeBot({
  functions: [
    new PromptFunction(getWeather, {
      description: "Get current weather for a location"
    })
  ]
})

// Bot will call the function when needed
const response = await bot.prompt("What's the weather in Tokyo?")
console.log(response) // "22°C and sunny in Tokyo."
```
{% endcapture %}

{% capture python_functions %}
```python
from colloquy_chatbot import ClaudeBot, prompt_function

# Define a function for the bot to use
@prompt_function(description="Get current weather for a location")
def get_weather(location: str, unit: str = "celsius"):
    # In a real app, this would call a weather API
    return f"Weather in {location}: 22°{'C' if unit == 'celsius' else 'F'}, Sunny"

# Create bot with access to this function
bot = ClaudeBot(
    functions=[get_weather]
)

# Bot will call the function when needed
response = await bot.prompt("What's the weather in Tokyo?")
print(response) # "22°C and sunny in Tokyo."
```
{% endcapture %}

{% include tabs.html group="functions" names="TypeScript|Python" typescript=typescript_functions python=python_functions %}

## Next Steps

Now that you understand the basics, you can:

1. Explore the [API Reference](/docs/api) for detailed documentation
2. Check out more [Examples](/docs/examples) for common use cases
3. Read the [FAQ](/docs/faq) for answers to common questions

For advanced usage, consider:
- Creating custom bot implementations
- Using advanced function parameter customization
- Building multi-modal applications