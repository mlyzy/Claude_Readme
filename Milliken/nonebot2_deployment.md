# NoneBot2 Deployment and Testing Process

## Overview

This document describes the process of deploying and testing the [NoneBot2](https://github.com/nonebot/nonebot2) project, a Python-based asynchronous chatbot framework. NoneBot2 is designed to be cross-platform and supports multiple messaging platforms through adapters.

## System Requirements

- Python 3.9 or higher
- pip (Python package manager)
- Git (for cloning the repository)
- Virtual environment (recommended)

## Installation Process

### 1. Clone the Repository

```bash
git clone https://github.com/nonebot/nonebot2.git
cd nonebot2
```

### 2. Set Up a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install NoneBot2

#### Method 1: Install from the cloned repository (for development)

```bash
pip install -e .  # Install in development mode
```

#### Method 2: Install from PyPI (for general use)

```bash
pip install nonebot2
```

### 4. Install Required Dependencies

#### Basic Dependencies

```bash
pip install fastapi uvicorn  # For FastAPI driver
```

#### Adapter Installation

```bash
pip install nonebot-adapter-console  # For console testing
# Other adapters can be installed as needed:
# pip install nonebot-adapter-onebot  # For OneBot protocol
# pip install nonebot-adapter-telegram  # For Telegram
```

## Creating a Simple Bot

### 1. Create Project Structure

```
my_bot/
├── .env            # Environment configuration
└── bot.py          # Main bot file
```

### 2. Configure the Environment File (.env)

```
DRIVER=~fastapi     # Use FastAPI as the driver
HOST=127.0.0.1      # Listen on localhost
PORT=8080           # Port to use
LOG_LEVEL=INFO      # Logging level
```

### 3. Create the Bot Script (bot.py)

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import nonebot
from nonebot.adapters.console import Adapter as ConsoleAdapter

# Initialize NoneBot
nonebot.init()

# Register adapter
driver = nonebot.get_driver()
driver.register_adapter(ConsoleAdapter)

# Register plugins
nonebot.load_builtin_plugins("echo")  # Load echo plugin

if __name__ == "__main__":
    nonebot.run()
```

## Running the Bot

```bash
python bot.py
```

When using the Console adapter, you'll be presented with an interactive terminal interface where you can test commands like:

```
/echo hello world
```

## Testing

### Testing with Built-in Plugins

1. The built-in "echo" plugin is useful for basic testing:
   - Send a message `/echo hello world` in the console
   - The bot should respond with `hello world`

### Creating Custom Plugins

1. Create a plugins directory:
   ```
   my_bot/
   ├── .env
   ├── bot.py
   └── plugins/
       ├── __init__.py
       └── my_plugin.py
   ```

2. Create a simple plugin (my_plugin.py):
   ```python
   from nonebot import on_command
   from nonebot.adapters import Message
   from nonebot.params import CommandArg
   from nonebot.plugin import PluginMetadata

   __plugin_meta__ = PluginMetadata(
       name="My Plugin",
       description="A simple test plugin",
       usage="/hello [name]"
   )

   hello = on_command("hello", priority=10, block=True)

   @hello.handle()
   async def handle_hello(args: Message = CommandArg()):
       name = args.extract_plain_text().strip()
       if name:
           await hello.finish(f"Hello, {name}!")
       else:
           await hello.finish("Hello, World!")
   ```

3. Load your plugin in bot.py:
   ```python
   # Add this line after loading built-in plugins
   nonebot.load_plugin("plugins.my_plugin")
   ```

## Common Issues and Solutions

1. **Module Not Found Errors**
   - Ensure your Python path is correctly set
   - Make sure the plugins directory is in the Python path
   - Use absolute imports or adjust sys.path

2. **Adapter Connection Issues**
   - Verify adapter-specific configuration
   - Check network connectivity if using remote services
   - Ensure correct credentials are provided

3. **Interactive Console Not Working**
   - The console adapter requires a proper terminal environment
   - May not work in all environments (e.g., some CI/CD systems)
   - Use non-interactive adapters for automated testing

## Further Resources

- [NoneBot2 Documentation](https://nonebot.dev/)
- [NoneBot2 GitHub Repository](https://github.com/nonebot/nonebot2)
- [Plugin Store](https://nonebot.dev/store)

---

*This deployment guide was created on June 4, 2025.*