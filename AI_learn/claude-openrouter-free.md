
Claude Code using a project-level settings file at .claude/settings.local.json in your project root:
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
Use CLI commands in wsl/linux
```
$ export ANTHROPIC_BASE_URL="https://openrouter.ai/api"
$ export ANTHROPIC_AUTH_TOKEN="sk-or-v1-7fd9ae6b.......85bdffac60a91b5b73c15c36afe19ef045a7d"
$ export ANTHROPIC_API_KEY=""
```
In cmd
```
$env:ANTHROPIC_BASE_URL="https://openrouter.ai/api"
   $env:ANTHROPIC_AUTH_TOKEN="sk-or-v1-7fd9ae6b5a888c2e148.....60a91b5b73c15c36afe19ef045a7d"
   $env:ANTHROPIC_API_KEY=""
```
