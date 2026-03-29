# Articulate — OpenCode Installation

Add Articulate to your OpenCode configuration by including it in your `opencode.json`:

```json
{
  "plugin": ["articulate@git+https://github.com/hristo2612/articulate.git"]
}
```

OpenCode will clone the plugin and register the skill automatically. Once installed, type `/articulate` in any session to begin.

## Uninstall

Remove the `articulate@git+...` entry from the `plugin` array in your `opencode.json`.
