---
layout: page
title: API Reference
permalink: /docs/api/
---

# API Reference

This page documents the full API for Colloquy. Here's a quick example to provide an overview of how the library works:

{% capture typescript_overview %}
```typescript
import { OpenAIBot } from "colloquy_chatbot"
const bot = new OpenAIBot()
await bot.prompt("Hello") // Returns a string with the chatbot's response
```
{% endcapture %}

{% capture python_overview %}
```python
from colloquy_chatbot import ClaudeBot
bot = ClaudeBot()
await bot.prompt("Hello") # Returns a string with the chatbot's response
```
{% endcapture %}

{% include tabs.html group="overview" names="TypeScript|Python" typescript=typescript_overview python=python_overview %}

## Create a Chatbot

With no advanced features, you can create a chatbot like this:

{% capture typescript_vanilla_constructor %}
```typescript
import { OpenAIBot, ClaudeBot } from "colloquy_chatbot"
const openai = new OpenAIBot()
const claude = new ClaudeBot()
```
{% endcapture %}

{% capture python_vanilla_constructor %}
```python
from colloquy_chatbot import ClaudeBot, OpenAIBot
claude = ClaudeBot()
openai = OpenAIBot()
```
{% endcapture %}

{% include tabs.html group="vanilla-constructor" names="TypeScript|Python" typescript=typescript_vanilla_constructor python=python_vanilla_constructor %}

All chatbots provide a consistent interface, so the remainder of these examples will use the custom bot `SampleBot`. If you wish to try these examples out, see the [Creating Custom Bot Adapters](#creating-custom-bot-adapters) section below, but you can also just substitute `ClaudeBot` or `OpenAIBot` depending on your preference.

### Providing Instructions

Here's how you can give the bot general instructions (a.k.a `system` prompts):

{% capture typescript_instructions %}
```typescript
const bot = new SampleBot({ instructions: "Do something interesting" })
```
{% endcapture %}

{% capture python_instructions %}
```python
bot = SampleBot(instructions="Do something interesting")
```
{% endcapture %}

{% include tabs.html group="instructions" typescript=typescript_instructions python=python_instructions %}

### Specifying Functions

If you want to provide tool functions to a chatbot, Colloquy will handle the resolution of those calls and reprompt with the results.

{% capture typescript_functions %}
```typescript
import { PromptFunction } from "colloquy_chatbot"
const bot = new SampleBot({ functions: [
  new PromptFunction(function test(a=5) { return a + 2 })
] })
```
{% endcapture %}

{% capture python_functions %}
```python
from colloquy_chatbot import prompt_function

@prompt_function()
def test(a=5):
    return a + 2

bot = SampleBot({ functions: [test] })
```
{% endcapture %}

{% include tabs.html group="functions" typescript=typescript_functions python=python_functions %}

The following context is directly inferred from the function:
* Function name
* Parameter names
* Parameter types
  - Typescript strips away type information during transcompilation, but if you provide a default parameter Colloquy can determine the type from that.

If you wish to augment or override information passed to the underlying library, you can do so by passing in an overlay as an additional parameter.

{% capture typescript_overlay %}
```typescript
new PromptFunction(
  async function test(a=5, b="foo", c="bar") { return a + b + c },
  {
    name: "concatenate",
    description: "Concatenate three strings",
    parameters: {
      a: {
        type: "string",
        description: "The first string",
      },
      b: { description: "The second string" },
    },
  },
)
```
{% endcapture %}

{% capture python_overlay %}
```python
@pytest.mark.asyncio
@prompt_function(
  description="A test function",
  name="concatenate",
  parameters={
    "a": {
      "type": "string",
      "description": "The first string",
    },
    "b": { "description": "The second string" },
})
async def test(a=5, b="foo", c="bar"):
  return str(a) + b + c
```
{% endcapture %}

{% include tabs.html group="overlay" typescript=typescript_overlay python=python_overlay %}

## Accessing History

Whenever an interaction occurs with the chatbot, the resulting information is added to `bot.history`. You can access this history to retrieve previous messages or to analyze the conversation flow.

{% capture typescript_history %}
```typescript
// Have a conversation
await bot.prompt("What is the capital of France?")
await bot.prompt("What about Germany?")

// Access the conversation history
console.log(bot.history) // Array of message objects with role and content

// Access specific messages
console.log(bot.history[0]) // First user message
console.log(bot.history[1]) // First bot response
```
{% endcapture %}

{% capture python_history %}
```python
# Have a conversation
await bot.prompt("What is the capital of France?")
await bot.prompt("What about Germany?")

# Access the conversation history
print(bot.history) # List of message objects with role and content

# Access specific messages
print(bot.history[0]) # First user message
print(bot.history[1]) # First bot response
```
{% endcapture %}

{% include tabs.html group="history" names="TypeScript|Python" typescript=typescript_history python=python_history %}

## Creating Custom Bot Adapters

You can create your own bot adapter by extending the base `Bot` class. This allows you to integrate any LLM provider with Colloquy's unified interface.

Here's how to create a custom `SampleBot` adapter:

{% capture typescript_custom_bot %}
```typescript
import { ChatBot, ChatMessage } from "colloquy_chatbot"

// Create your custom bot implementation
class SampleBot extends ChatBot {
  private apiKey: string

  constructor(options: { apiKey?: string, instructions?: string, functions?: any[] } = {}) {
    // Pass options to the parent Bot class
    super(options)

    // Store your API key
    this.apiKey = options.apiKey || process.env.SAMPLE_API_KEY || ""

    if (!this.apiKey) {
      console.warn("No API key provided for SampleBot. Set SAMPLE_API_KEY environment variable or pass apiKey option.")
    }
  }

  // Implement the required send_prompt method
  async send_prompt(): Promise<string> {
    // Format messages for your LLM provider's API
    const formattedMessages = this.history.map(msg => ({
      role: msg.role,
      content: msg.content
    }))

    try {
      // Make API call to your LLM provider
      // This is a simplified example - replace with actual API call
      const response = await fetch("https://api.your-llm-provider.com/v1/chat", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${this.apiKey}`
        },
        body: JSON.stringify({
          messages: formattedMessages,
          instructions: this.instructions,
          functions: this.functionsForProvider(),
          // Other provider-specific options
        })
      })

      const data = await response.json()

      if (!response.ok) {
        throw new Error(`API error: ${data.error?.message || response.statusText}`)
      }

      return data.response || data.message || data.text || ""
    } catch (error) {
      console.error("Error calling LLM API:", error)
      throw error
    }
  }

  private functionsForProvider() {
    if (!this.functions || this.functions.length === 0) {
      return undefined
    }

    // Transform functions to your provider's expected format
    return this.functions.map(fn => ({
      name: fn.name,
      description: fn.description,
      parameters: fn.parameters,
      // Any provider-specific properties
    }))
  }
}

// Use your custom bot
const bot = new SampleBot({
  apiKey: "your-api-key",
  instructions: "You are a helpful assistant"
})

const response = await bot.prompt("Hello, can you help me?")
console.log(response)
```
{% endcapture %}

{% capture python_custom_bot %}
```python
import os
import aiohttp
from typing import List, Optional, Any, Dict
from colloquy_chatbot import ChatBot, ChatMessage

# Create your custom bot implementation
class SampleBot(ChatBot):
  def __init__(
      self, 
      api_key: Optional[str] = None,
      instructions: Optional[str] = None, 
      functions: Optional[List[Any]] = None
  ):
      # Pass arguments to the parent Bot class
      super().__init__(instructions=instructions, functions=functions)

      # Store your API key
      self.api_key = api_key or os.environ.get("SAMPLE_API_KEY", "")

      if not self.api_key:
          print("Warning: No API key provided for SampleBot. Set SAMPLE_API_KEY environment variable or pass api_key argument.")

  # Implement the required send_prompt method
  async def send_prompt(self) -> str:
    # Format messages for your LLM provider's API
    formatted_messages = [
      {"role": msg.role, "content": msg.content}
      for msg in self.history
    ]

    try:
      # Make API call to your LLM provider
      # This is a simplified example - replace with actual API call
      async with aiohttp.ClientSession() as session:
        async with session.post(
          "https://api.your-llm-provider.com/v1/chat",
          headers={
            "Content-Type": "application/json",
            "Authorization": f"Bearer {self.api_key}"
          },
          json={
            "messages": formatted_messages,
            "instructions": self.instructions,
            "functions": self.functions_for_provider(),
            # Other provider-specific options
          }
        ) as response:
          if response.status != 200:
            error_text = await response.text()
            raise ValueError(f"API error: {error_text}")

          data = await response.json()
          return data.get("response", "") or data.get("message", "") or data.get("text", "")
    except Exception as e:
      print(f"Error calling LLM API: {e}")
      raise

  def functions_for_provider(self) -> Optional[List[Dict[str, Any]]]:
    if not self.functions:
      return None

    # Transform functions to your provider's expected format
    return [
      {
        "name": fn.name,
        "description": fn.description,
        "parameters": fn.parameters,
        # Any provider-specific properties
      }
      for fn in self.functions
    ]

# Use your custom bot
bot = SampleBot(
  api_key="your-api-key",
  instructions="You are a helpful assistant"
)

response = await bot.prompt("Hello, can you help me?")
print(response)
```
{% endcapture %}

{% include tabs.html group="custom-bot" names="TypeScript|Python" typescript=typescript_custom_bot python=python_custom_bot %}
