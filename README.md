<p align="center">
    <img src="docudoodle.png" width="200" />	
</p>
<h1 align="center">
    Docudoodle v2.0.0
</h1>


This is Docudoodle! 👋 The PHP documentation generator that analyzes your codebase and creates comprehensive documentation using AI. It's perfect for helping you and your team understand your code better through detailed insights into your application's structure and functionality.

Docudoodle is fab if you've taken on an application with no existing documentation allowing your team to get up to speed right away.

Docudoodle writes Markdown files which show up great in Github and other source control providers allowing you to get teams up to speed in a matter of moments.

Better yet, Docudoodle skips already existing documentation files. Allowing a quick top-up run after you have concluded a feature, meaning that the entire process of getting good documentation written is a thing of the past 🚀

## Examples
If you want to see what the output of some documentation looks like, check out the [examples folder](https://github.com/genericmilk/docudoodle/tree/main/examples) in this repo which contains a few examples 🥰

## Features

- **Automatic Documentation Generation**: Effortlessly generates documentation for PHP files by analyzing their content.
- **Flexible AI Integration**: Choose between OpenAI's powerful cloud API, Claude API, Google's Gemini API, or run locally with Ollama models for complete privacy.
- **Ollama Support**: Generate documentation completely offline using your own local Ollama models - perfect for private codebases or when you need to work without an internet connection.
- **Customizable**: Easily configure source directories, output folders, and other settings to match your workflow.
- **Command-Line Interface**: Includes a simple command-line script for quick documentation generation.

## Installation

Getting started with Docudoodle is super easy! Just use Composer with this command:

```
composer require genericmilk/docudoodle
```

This will set up all the necessary dependencies defined in the `composer.json` file.

## Usage

Ready to create some amazing documentation? Just run this simple command:

```
php artisan docudoodle:generate
```

If you're using OpenAI, make sure to set your API key which looks a bit like this: `sk-XXXXXXXX` in the application configuration file. If you're using Ollama, ensure it's running on your system and properly configured in your settings. For Claude, set your API key in the configuration file.

## Configuration

Docudoodle is highly customizable! The package includes a configuration file at `config/docudoodle.php` that lets you tailor everything to your needs:

### OpenAI API Key
```php
'openai_api_key' => env('OPENAI_API_KEY', ''),
```
Set your OpenAI API key here or in your `.env` file as `OPENAI_API_KEY`. Keys typically start with `sk-XXXXXXXX`.

### Claude API Key
```php
'claude_api_key' => env('CLAUDE_API_KEY', ''),
```
Set your Claude API key here or in your `.env` file as `CLAUDE_API_KEY`.

### Gemini API Key
```php
'gemini_api_key' => env('GEMINI_API_KEY', ''),
```
Set your Gemini API key here or in your `.env` file as `GEMINI_API_KEY`.

### Model Selection
```php
'default_model' => env('DOCUDOODLE_MODEL', 'gpt-4o-mini'),
```
Choose which model to use. The default is `gpt-4o-mini` for OpenAI, but you can specify any OpenAI model, Claude model, Gemini model, or Ollama model name in your `.env` file with the `DOCUDOODLE_MODEL` variable.

### API Provider
```php
'default_api_provider' => env('DOCUDOODLE_API_PROVIDER', 'openai'),
```
Choose which API provider to use: 'openai' for cloud-based generation, 'claude' for Claude API, 'gemini' for Gemini API, or 'ollama' for local generation. Set in your `.env` file with `DOCUDOODLE_API_PROVIDER`.

### Ollama Configuration
```php
'ollama_host' => env('OLLAMA_HOST', 'localhost'),
'ollama_port' => env('OLLAMA_PORT', '11434'),
```
Configure your Ollama host and port if using Ollama as the API provider. The defaults work with standard Ollama installations.

### Token Limits
```php
'max_tokens' => env('DOCUDOODLE_MAX_TOKENS', 10000),
```
Control the maximum number of tokens for API calls. Adjust this in your `.env` file with `DOCUDOODLE_MAX_TOKENS` if needed.

### File Extensions
```php
'default_extensions' => ['php', 'yaml', 'yml'],
```
Specify which file types Docudoodle should process. By default, it handles PHP and YAML files.

### Skip Directories
```php
'default_skip_dirs' => ['vendor/', 'node_modules/', 'tests/', 'cache/'],
```
Define directories that should be excluded from documentation generation.

You can publish the configuration file to your project using:

```
php artisan vendor:publish --tag=docudoodle-config
```

## Template Variables

When creating custom prompt templates for documentation generation, you can use the following variables:

| Variable | Description |
|----------|-------------|
| `{FILE_PATH}` | The full path to the file being documented |
| `{FILE_CONTENT}` | The content of the file being processed |
| `{FILE_NAME}` | The filename with extension (e.g., `User.php`) |
| `{EXTENSION}` | The file extension (e.g., `php`) |
| `{BASE_NAME}` | The filename without extension (e.g., `User`) |
| `{DIRECTORY}` | The directory containing the file |

## Custom Template Example

Create a markdown file for your custom prompt template:

```markdown
# My Custom Documentation Template

Please document this {EXTENSION} file: {FILE_PATH}

Here's the code:
```{EXTENSION}
{FILE_CONTENT}
```

Focus on explaining what this file does in simple terms.
```

Then specify the custom template path when initializing Docudoodle:

```php
$docudoodle = new Docudoodle(
    promptTemplate: '/path/to/your/custom-template.md'
);
```

## Running Tests

Want to make sure everything's working perfectly? Run the tests with:

```
./vendor/bin/phpunit
```

Or if you're using Laravel's test runner:

```
php artisan test
```

## License

This project is licensed under the MIT License. Check out the LICENSE file for all the details.

## Contributing

We'd love your help making Docudoodle even better! Feel free to submit a pull request or open an issue for any enhancements or bug fixes. Everyone's welcome! 🎉
