# chrome-devtools-mcp (fork)

Fork of [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) — general-purpose browser automation, plus our own custom tools on top.

## Remotes
- `origin` → `rahul38832/chrome-devtools-mcp` (our fork)
- `upstream` → `ChromeDevTools/chrome-devtools-mcp` (push disabled)

## Wired into Claude Code
Registered as the user-scoped MCP server `chrome` (`~/.claude.json`):

```
node build/src/bin/chrome-devtools-mcp.js --browserUrl http://127.0.0.1:9222 --no-usage-statistics
```

It attaches to a Chrome already listening on `:9222` — start one with `~/data/scripts/chrome-debug.sh` (persistent profile) or `-n` (throwaway). Browser connection is lazy, so the server is healthy even when no Chrome is running.

## Build & run
- `npm ci` — install (first time / after upstream sync)
- `npm run build` — compile to `build/`; **required after any `src/` change** for the `chrome` MCP to pick it up
- Reload Claude Code (`/mcp` or restart) to load tool changes into the running session

## Sync upstream
```
git fetch upstream && git merge upstream/main && npm ci && npm run build
```

## Customizations
Tools live in `src/tools/`. Add new ones there; rebuild; reload. Upstream already ships `src/tools/extensions.ts` (`--categoryExtensions`), but those tools only work over a pipe connection, not `--browserUrl`, until Chrome 149.
