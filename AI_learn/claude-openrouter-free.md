
Claude Code using a project-level settings file at .claude/settings.json in your project root:
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
 "ANTHROPIC_BASE_URL": "https://openrouter.ai/api",
    "ANTHROPIC_AUTH_TOKEN": "YOUR OPEN ROUTER API KEY",
    "ANTHROPIC_API_KEY": "",
    "ANTHROPIC_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "openrouter/free",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "openrouter/free",
    "ANTHROPIC_SMALL_FAST_MODEL": "openrouter/free",
    "CLAUDE_CODE_SUBAGENT_MODEL": "openrouter/free"
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
