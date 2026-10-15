# ai-plugins

MCP servers for AI tools on this Mac, defined in [`.mcp.json`](.mcp.json).

Claude Code reads the root `.mcp.json` automatically. Other tools use their own locations (Cursor: `.cursor/mcp.json`, VS Code: `.vscode/mcp.json`), so copy the entries there if needed.

## OmniFocus Operator

Read and edit OmniFocus tasks, projects, tags and perspectives.

- Repo: https://github.com/HelloThisIsFlo/omnifocus-operator
- Docs and setup wizard: https://hellothisisflo.github.io/omnifocus-operator

**Requirements:** macOS, OmniFocus 4, Python 3.12+, and [uv](https://github.com/astral-sh/uv) (for `uvx`).

**Install:** nothing to install. `uvx omnifocus-operator` downloads and runs the server from PyPI on first use. If `uv` is missing:

```bash
brew install uv
```

**First run:** OmniFocus shows a one-time permission dialog. Tick the "Automatically run" checkbox and click **Run Script**.

## Apple PIM

Calendar, Reminders, Contacts and Mail.app through native macOS frameworks.

- Repo: https://github.com/omarshahine/apple-pim

**Requirements:** macOS 13+, Swift 5.9+ (Xcode 15+), Node.js.

**Install:** it's distributed as a Claude Code plugin, not on npm. Inside Claude Code:

```
/plugin marketplace add omarshahine/apple-pim
/plugin install apple-pim@apple-pim
```

Then build the Swift CLIs it relies on (once):

```bash
bash ~/.claude/plugins/cache/*/apple-pim/*/setup.sh --install
```

`.mcp.json` runs the server from the plugin's install folder (`~/.claude/plugins/marketplaces/apple-pim/mcp-server/dist/server.js`), so the plugin must be installed for this entry to work. The path is absolute; update it if your home folder differs.

**Permissions:** on first use, macOS asks for Calendar, Reminders and Contacts access. For mail, also allow your terminal or AI app to control Mail.app under System Settings > Privacy & Security > Automation. Full Disk Access is optional and makes mail reads faster.

**Note:** with the plugin enabled, Claude Code sessions in this repo also get Apple PIM from the plugin, so it may load twice.
