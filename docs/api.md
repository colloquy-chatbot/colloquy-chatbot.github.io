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

All chatbots provide a consistent interface, so the remainder of these examples will use the custom bot `SampleBot`. If you wish to try these examples out, instructions on how to create this bot are included in the documentation on creating custom bots (TODO: add a link), but you can also just sub in `ClaudeBot` or `OpenAIBot` depending on your preference.

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
  function test(a=5, b="foo", c="bar") { return a + b + c },
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
def test(a=5, b="foo", c="bar"):
  return str(a) + b + c
```
{% endcapture %}

{% include tabs.html group="overlay" typescript=typescript_overlay python=python_overlay %}
