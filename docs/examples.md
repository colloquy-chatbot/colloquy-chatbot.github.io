---
layout: page
title: Examples
permalink: /docs/examples/
---

# Colloquy Examples

This page provides practical examples of using Colloquy for common chatbot scenarios.

## Basic Usage

Getting started with a simple conversation:

{% capture typescript_basic %}
```typescript
import { OpenAIBot } from "colloquy_chatbot"

// Create a bot instance
const bot = new OpenAIBot()

// Send a message and get a response
const response = await bot.prompt("Tell me about chatbots")
console.log(response) // "Chatbots are AI programs designed to simulate conversation with human users..."

// Continue the conversation
const followUp = await bot.prompt("What are their limitations?")
console.log(followUp) // "Current chatbots face several limitations including contextual understanding..."
```
{% endcapture %}

{% capture python_basic %}
```python
from colloquy_chatbot import OpenAIBot

# Create a bot instance
bot = OpenAIBot()

# Send a message and get a response
response = await bot.prompt("Tell me about chatbots")
print(response) # "Chatbots are AI programs designed to simulate conversation with human users..."

# Continue the conversation
follow_up = await bot.prompt("What are their limitations?")
print(follow_up) # "Current chatbots face several limitations including contextual understanding..."
```
{% endcapture %}

{% include tabs.html group="basic" names="TypeScript|Python" typescript=typescript_basic python=python_basic %}

## Working with Instructions

Customizing bot behavior with system instructions:

{% capture typescript_instructions %}
```typescript
import { ClaudeBot } from "colloquy_chatbot"

// Create a bot with specific instructions
const bot = new ClaudeBot({
  instructions: `You are a helpful assistant specialized in Python programming.
  Always include code examples in your answers when relevant.
  Keep explanations concise and beginner-friendly.`
})

// The bot will follow these instructions in all responses
const response = await bot.prompt("How can I read a CSV file?")
console.log(response) // "To read a CSV file in Python, you can use the csv module or pandas: import pandas as pd\ndf = pd.read_csv('file.csv')..."
```
{% endcapture %}

{% capture python_instructions %}
```python
from colloquy_chatbot import ClaudeBot

# Create a bot with specific instructions
bot = ClaudeBot(
    instructions="""You are a helpful assistant specialized in Python programming.
    Always include code examples in your answers when relevant.
    Keep explanations concise and beginner-friendly."""
)

# The bot will follow these instructions in all responses
response = await bot.prompt("How can I read a CSV file?")
print(response) # "To read a CSV file in Python, you can use the csv module or pandas: import pandas as pd\ndf = pd.read_csv('file.csv')..."
```
{% endcapture %}

{% include tabs.html group="instructions" names="TypeScript|Python" typescript=typescript_instructions python=python_instructions %}

## Function Calling

Enabling the bot to call functions to perform actions or retrieve information:

{% capture typescript_functions %}
```typescript
import { OpenAIBot, PromptFunction } from "colloquy_chatbot"

// Define functions the bot can use
function getWeather(location: string, unit: string = "celsius") {
  // In a real app, this would call a weather API
  return `Weather in ${location}: 22°${unit === "celsius" ? "C" : "F"}, Sunny`
}

function searchDatabase(query: string, limit: number = 5) {
  // Simulate database search
  return [`Result 1 for "${query}"`, `Result 2 for "${query}"`, `Result 3 for "${query}"`]
}

// Create bot with these functions
const bot = new OpenAIBot({
  functions: [
    new PromptFunction(getWeather, {
      description: "Get current weather for a location"
    }),
    new PromptFunction(searchDatabase, {
      description: "Search the knowledge database for information"
    })
  ]
})

// Bot will automatically call functions when needed
const response = await bot.prompt("What's the weather like in Paris?")
console.log(response) // "The weather in Paris is currently 22°C and sunny."
```
{% endcapture %}

{% capture python_functions %}
```python
from colloquy_chatbot import OpenAIBot, prompt_function

# Define functions the bot can use
@prompt_function(description="Get current weather for a location")
def get_weather(location: str, unit: str = "celsius"):
    # In a real app, this would call a weather API
    return f"Weather in {location}: 22°{'C' if unit == 'celsius' else 'F'}, Sunny"

@prompt_function(description="Search the knowledge database for information")
def search_database(query: str, limit: int = 5):
    # Simulate database search
    return [f"Result 1 for '{query}'", f"Result 2 for '{query}'", f"Result 3 for '{query}'"]

# Create bot with these functions
bot = OpenAIBot(
    functions=[get_weather, search_database]
)

# Bot will automatically call functions when needed
response = await bot.prompt("What's the weather like in Paris?")
print(response) # "The weather in Paris is currently 22°C and sunny."
```
{% endcapture %}

{% include tabs.html group="functions" names="TypeScript|Python" typescript=typescript_functions python=python_functions %}

## Advanced Function Configuration

Customizing function definitions with parameter metadata:

{% capture typescript_advanced_functions %}
```typescript
import { ClaudeBot, PromptFunction } from "colloquy_chatbot"

// Define a function with custom metadata
function searchProducts(
  query: string,
  category: string = "all",
  minPrice: number = 0,
  maxPrice: number = 1000,
  inStock: boolean = true
) {
  // Simulate product search
  return [`Product 1 matching "${query}"`, `Product 2 matching "${query}"`]
}

const bot = new ClaudeBot({
  functions: [
    new PromptFunction(
      searchProducts,
      {
        name: "findProducts", // Override function name
        description: "Search product catalog with various filters",
        parameters: {
          query: {
            description: "Search terms for finding products",
            type: "string",
            required: true
          },
          category: {
            description: "Product category to filter by",
            type: "string",
            enum: ["electronics", "clothing", "books", "home", "all"]
          },
          minPrice: {
            description: "Minimum price filter",
            type: "number"
          },
          maxPrice: {
            description: "Maximum price filter",
            type: "number"
          },
          inStock: {
            description: "Filter to only in-stock items",
            type: "boolean"
          }
        }
      }
    )
  ]
})

// Bot will use the enhanced function definition
const response = await bot.prompt("Find me electronics under $500")
console.log(response) // "I found several electronics under $500: Product 1 matching 'electronics', Product 2 matching 'electronics'..."
```
{% endcapture %}

{% capture python_advanced_functions %}
```python
from colloquy_chatbot import ClaudeBot, prompt_function

# Define a function with custom metadata
@prompt_function(
    name="findProducts", # Override function name
    description="Search product catalog with various filters",
    parameters={
        "query": {
            "description": "Search terms for finding products",
            "type": "string",
            "required": True
        },
        "category": {
            "description": "Product category to filter by",
            "type": "string",
            "enum": ["electronics", "clothing", "books", "home", "all"]
        },
        "minPrice": {
            "description": "Minimum price filter",
            "type": "number"
        },
        "maxPrice": {
            "description": "Maximum price filter",
            "type": "number"
        },
        "inStock": {
            "description": "Filter to only in-stock items",
            "type": "boolean"
        }
    }
)
def search_products(
    query: str,
    category: str = "all",
    min_price: float = 0,
    max_price: float = 1000,
    in_stock: bool = True
):
    # Simulate product search
    return [f"Product 1 matching '{query}'", f"Product 2 matching '{query}'"]

bot = ClaudeBot(
    functions=[search_products]
)

# Bot will use the enhanced function definition
response = await bot.prompt("Find me electronics under $500")
print(response) # "I found several electronics under $500: Product 1 matching 'electronics', Product 2 matching 'electronics'..."
```
{% endcapture %}

{% include tabs.html group="advanced-functions" names="TypeScript|Python" typescript=typescript_advanced_functions python=python_advanced_functions %}

## Creating Custom Bots

Implementing a custom bot backend:

{% capture typescript_custom %}
```typescript
import { Bot, ChatMessage } from "colloquy_chatbot"

// Create a custom bot implementation
class CustomBot extends Bot {
  private apiKey: string
  private endpoint: string

  constructor(options: { 
    apiKey: string, 
    endpoint: string,
    instructions?: string 
  }) {
    super(options)
    this.apiKey = options.apiKey
    this.endpoint = options.endpoint
  }

  async generateResponse(messages: ChatMessage[]): Promise<string> {
    // Implement custom API call to your bot backend
    const response = await fetch(this.endpoint, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${this.apiKey}`
      },
      body: JSON.stringify({ messages })
    })

    const data = await response.json()
    return data.response
  }
}

// Use the custom bot
const myBot = new CustomBot({
  apiKey: "your-api-key",
  endpoint: "https://api.your-llm-service.com/chat",
  instructions: "You are a helpful assistant."
})

const response = await myBot.prompt("Hello, can you help me?")
console.log(response) // "Yes, I'm here to help! What do you need assistance with today?"
```
{% endcapture %}

{% capture python_custom %}
```python
import aiohttp
from colloquy_chatbot import Bot, ChatMessage

# Create a custom bot implementation
class CustomBot(Bot):
    def __init__(self, api_key, endpoint, instructions=None):
        super().__init__(instructions=instructions)
        self.api_key = api_key
        self.endpoint = endpoint

    async def generate_response(self, messages: list[ChatMessage]) -> str:
        # Implement custom API call to your bot backend
        async with aiohttp.ClientSession() as session:
            async with session.post(
                self.endpoint,
                headers={
                    "Content-Type": "application/json",
                    "Authorization": f"Bearer {self.api_key}"
                },
                json={"messages": [m.to_dict() for m in messages]}
            ) as response:
                data = await response.json()
                return data["response"]

# Use the custom bot
my_bot = CustomBot(
    api_key="your-api-key",
    endpoint="https://api.your-llm-service.com/chat",
    instructions="You are a helpful assistant."
)

response = await my_bot.prompt("Hello, can you help me?")
print(response) # "Yes, I'm here to help! What do you need assistance with today?"
```
{% endcapture %}

{% include tabs.html group="custom" names="TypeScript|Python" typescript=typescript_custom python=python_custom %}

## Dictionary Examples

Working with dictionary structures in Python:

```python
# Creating a dictionary
user = {
    "name": "Alice",
    "age": 28,
    "email": "alice@example.com",
    "is_active": True,
    "preferences": {
        "theme": "dark",
        "notifications": True
    }
}

# Accessing values
print(user["name"])  # Alice
print(user["preferences"]["theme"])  # dark

# Adding or updating values
user["role"] = "Admin"
user["age"] = 29

# Dictionary methods
keys = user.keys()
values = user.values()
items = user.items()

# Checking if a key exists
if "email" in user:
    print(f"Email: {user['email']}")

# Get value with default fallback
phone = user.get("phone", "Not provided")

# Iterating over items
for key, value in user.items():
    print(f"{key}: {value}")
```