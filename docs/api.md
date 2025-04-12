---
layout: page
title: API Reference
permalink: /docs/api/
---

# API Reference

This page documents the full API for Colloquy.

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

All chatbots provide a consistent interface, so the remainder of these examples will the custom bot `SampleBot`. If you wish to try these examples out, instructions on how to create this bot are included in the documentation on creating custom bots (TODO: add a link), but you can also just sub in `ClaudeBot` or `OpenAIBot` depending on your preference.

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

{% include tabs.html group="instructions" names="TypeScript|Python" typescript=typescript_instructions python=python_instructions %}
