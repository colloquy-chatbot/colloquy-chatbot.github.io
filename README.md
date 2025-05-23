# Colloquy Documentation

This repository contains the documentation website for Colloquy, an open source tool for interacting with chatbots. The site is built with Jekyll and hosted on GitHub Pages.

## Local Development

### Prerequisites

- Ruby version 2.5.0 or higher
- RubyGems

### Setup

1. Install Jekyll and Bundler gems
   ```
   gem install jekyll bundler
   ```

2. Clone this repository
   ```
   git clone https://github.com/colloquy-chatbot/colloquy-chatbot.github.io.git
   cd colloquy-chatbot.github.io
   ```

3. Install dependencies
   ```
   bundle install
   ```

4. Start the local server
   ```
   bundle exec jekyll serve
   ```

5. Browse to http://localhost:4000

## Customizing

To customize this template for your own project:

1. Edit `_config.yml` to update site settings
2. Modify content in the `docs/` directory
3. Update the homepage in `index.markdown`
4. Add your project information to the `about.markdown` page
5. Customize styling in `_sass/minima-override/` directory and `assets/main.scss`

## Documentation Structure

- `docs/getting-started.md` - Installation and basic usage
- `docs/api.md` - API reference documentation
- `docs/examples.md` - Usage examples
- `docs/faq.md` - Frequently asked questions

## Tabs Component

The documentation uses a custom tabs component to display both TypeScript and Python implementation examples. The component:

- Allows switching between language implementations
- Synchronizes tab selections across all examples on a page
- Remembers user's language preference using localStorage
- Can be used with the following syntax:

```liquid
{% capture tab_typescript %}
```typescript
// TypeScript code here
```
{% endcapture %}

{% capture tab_python %}
```python
# Python code here
```
{% endcapture %}

{% include tabs.html group="example" typescript=tab_typescript python=tab_python %}
```

## Contributing

Contributions to the documentation are welcome! Please see the [contribution guidelines](https://github.com/colloquy-chatbot/colloquy/blob/main/CONTRIBUTING.md) for more information.

## License

This documentation is licensed under the MIT License - see the LICENSE file for details.
