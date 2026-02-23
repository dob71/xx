# xx - Simple Bash Command Line AI Assistant

A simple bash wrapper for interacting with a fast local LLM (Large Language Model) directly from the command line. Get instant command suggestions and execute them with minimal friction.

## Overview

`xx` translates natural language descriptions into executable bash commands using a local LLM API. It's designed for speed and convenience - no need to open a browser or chat interface.

## Features

- **Natural language to command**: Describe what you want to do in plain English
- **Instant execution**: Copy commands to primary selection (Shift+Insert) and run immediately
- **Local LLM support**: Works with self-hosted models (tested with Qwen2.5-Coder-32B-Instruct)
- **File context**: Include file contents in your prompts using `@filename` or `@ filename` syntax
- **Clean output**: Removes code blocks from text, shows only the essential information

## Installation

1. Save the script to a directory in your PATH (e.g., `~/bin/xx` or `/usr/local/bin/xx`)
2. Make it executable: `chmod +x xx`
3. Install required dependencies:
   - `jq` - JSON processor
   - `curl` - HTTP client
   - `xclip` or `xsel` - Clipboard utilities (Linux)

```bash
# Ubuntu/Debian
sudo apt-get install jq curl xclip

# Or use xsel instead
sudo apt-get install jq curl xsel
```

## Configuration

Edit the script to configure your LLM API endpoint:

```bash
URL="http://192.168.0.123:5000/v1/chat/completions"  # Your API endpoint
API_KEY="your-api-key-here"                          # Your API key
MODEL="Qwen2.5-Coder-32B-Instruct-q8.0"              # Model name
```

## Usage

### Basic Command Generation

```bash
xx list all files in current directory
```

Output:
```
Here is the command to list all files in the current directory:
ls -la
```

The command `ls -la` is copied to your primary selection. Press **Shift+Insert** then **Enter** to execute.

### With File Context

Include file contents in your prompt using the `@` prefix:

```bash
xx analyze this file @config.json
```

The content of `config.json` will be included in the LLM prompt.

## Workflow

1. **Describe** what you want to do:
   ```bash
   xx find all Python files modified in the last 24 hours
   ```

2. **Review** the generated command (shown in green text)

3. **Execute** using Shift+Insert paste:
   - Press **Shift+Insert** to paste the command
   - Press **Enter** to execute

## Examples

```bash
# File operations
xx create a tar archive of the current directory
xx find all files larger than 100MB

# System commands
xx show disk usage for all mounted filesystems
xx list all running processes sorted by memory usage

# Git operations
xx show the last 10 commits with graph
xx create a new branch and switch to it

# With file context
xx explain what this script does @xx
xx convert this JSON to CSV @data.json
```

## Requirements

- Bash shell
- `jq` for JSON parsing
- `curl` for API requests
- `xclip` or `xsel` for clipboard operations (Linux)
- Access to a local LLM API (OpenAI-compatible endpoint)

## Tips

- The script uses **primary selection** (not clipboard) for Linux, so use **Shift+Insert** to paste
- Multiline commands are supported and properly formatted
- The LLM response text is displayed without code blocks for readability
- If no command is found in the response, the full text is shown instead

## Remote SSH Sessions

When connecting to a remote system over SSH, the clipboard sync requires:
- A terminal that supports **OSC 52 escape sequences** (e.g., [KiTTY](https://www.9bis.net/kitty/), iTerm2, Windows Terminal, or modern terminals)
- The script automatically detects SSH sessions and uses OSC 52 to sync clipboard

**To paste from the Linux clipboard:** Use `Ctrl+Shift+V`

## License

MIT License - Feel free to modify and distribute.

