
Claude Code using a project-level settings file at .claude/settings.json in your project root:
```
open ~/.claude/settings.local.json
```
```
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "sk-or-v1-7fd9ae6b5a888cac60a91b5b73c15c36afe19....",
    "ANTHROPIC_API_KEY": "",
    "ANTHROPIC_MODEL": "openrouter/free"
  }
}
```
or
```
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "YOUR OPEN ROUTER API KEY",
    "ANTHROPIC_API_KEY": "",
    "ANTHROPIC_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "openrouter/free",
    "ANTHROPIC_SMALL_FAST_MODEL": "openrouter/free",
    "CLAUDE_CODE_SUBAGENT_MODEL": "openrouter/free"
  }
}
```
Use CLI commands in wsl/linux
```
export ANTHROPIC_BASE_URL="https://openrouter.ai/api"
export ANTHROPIC_AUTH_TOKEN="sk-or-v1-7fd9ae6b.......85bdffac60a91b5b73c15c36afe19ef045a7d"
export ANTHROPIC_API_KEY=""
```
In windows powershell
```
$env:ANTHROPIC_BASE_URL="https://openrouter.ai/api"
$env:ANTHROPIC_AUTH_TOKEN="sk-or-v1-7fd9ae6b5a888c2e148.....60a91b5b73c15c36afe19ef045a7d"
$env:ANTHROPIC_API_KEY=""
claude
```
```
/status
/logout
```
Ref: <https://openrouter.ai/docs/guides/coding-agents/claude-code-integration>
```
 curl -fsSL https://ollama.com/install.sh | sh
 sudo apt-get install zstd
 curl -fsSL https://ollama.com/install.sh | sh
 ollama ls
 ollama ps
 ollama stop
 1997  curl -fsSL https://ollama.com/install.sh | sh
 1998  ollama pull gemma4:e2b
 1999  ollama
 2000  ollama pull gemma4:e2b
 2001  ollama ps
 2002  ollama run gemma4:e2b
 2003  ollama ps
 2004  ollama
 2005  ollama pull llama3.2:1b
 2006  ollama run llama3.2:1b
 2007  ollama ls
```
Claude Code with local model Gemma4
.claude/settings.json in your project root
```
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://localhost:11434",    
    "model": "gemma4:e2b"
  }
}
```
Open VS Code, open claude code ext > setting> setting.json
```
{"name": "ANTHROPIC_BASE_URL", "value": "http://localhost:1234"},
      {"name": "ANTHROPIC_API_KEY", "value": "lmstudio"}
```
Ref: <https://ollama.com/blog/claude>
