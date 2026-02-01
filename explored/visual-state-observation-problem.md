# The Visual State Observation Problem

**Date**: 2026-02-01
**Context**: Debugging Zellij tab duplication bug, exploring better workflows for visual/UI debugging

---

## The Problem

When debugging anything with visual state (terminal UIs, desktop apps, web UIs), current workflow requires:

1. Observe current state
2. Make changes
3. Observe what changed
4. Iterate

Steps 1 and 3 currently require manual screenshot-taking and sharing. This breaks iteration speed and makes visual debugging painfully slow.

---

## Screenshot MCP Server

**Goal**: Let Claude proactively take screenshots.

**Setup**:
- Built Node.js MCP server using `screenshot-desktop` library
- Added configuration to VSCode settings: `claudeCode.mcpServers`
- Expected Claude Code extension to load and expose screenshot tool

**Result**:
- MCP server did not load
- No screenshot tool appeared in Claude's available tools
- No error messages in Claude Code output logs
- Unclear if VSCode extension supports MCP servers or requires different configuration

**Limitations Even If Working**:
- Still discrete snapshots, not continuous observation
- Reactive (Claude requests screenshot after the fact)
- Can't observe state transitions, only states
- Would improve manual workflow but not fundamentally change it

---

## Computer Use API

**Goal**: Autonomous Claude instance that can see virtual desktop and debug issues independently.

**Setup**:
- Docker container running Ubuntu desktop with X11
- Web interface at localhost:9080 (combined chat + desktop view)
- Mounted user's ~/.config/zellij into container
- Claude can take screenshots, control mouse/keyboard, run bash commands, edit files

**Actual Experience**:

Started promising:
- Container launched successfully
- Web UI loaded
- Claude began installing Zellij
- Understood the debugging task

Then hit issues:

**Websocket Instability**:
```
StreamClosedError: Stream is closed
WebSocketClosedError
```
- Frequent connection drops in container logs
- Messages sometimes don't get through to Claude
- Communication becomes unreliable

**No Feedback When Stuck**:
- Claude attempted keyboard shortcut (Ctrl+t) to create new tab
- Nothing visibly happened on desktop
- Claude stopped responding with no indication why
- Can't tell if: command failed, Claude is processing, waiting for something, encountered error
- Sent clarification message ("the keybinding is Ctrl+t then n") - unclear if received
- No visible thinking or reasoning process

**Opacity**:
- Can see what actions Claude takes (via tool use in chat)
- Can see desktop view
- Cannot see Claude's reasoning when stuck
- Cannot see if Claude received your messages
- Difficult to provide course corrections

**When This Approach Might Work**:
- Long-running automation where occasional hiccups acceptable
- Tasks that don't require tight feedback loop
- Scenarios where human can wait for eventual completion

**Our Use Case**:
- Interactive debugging needs fast iteration
- When stuck, need to quickly guide Claude
- Current stability insufficient for tight feedback loop

---

## Playwright MCP

**Note**: Researched but not hands-on tested. Coworkers have used it.

**What It Is**:
- MCP server exposing Playwright browser automation
- Uses browser accessibility tree (structured data), not screenshots
- Can navigate pages, interact with elements, fill forms, take screenshots when needed

**Use Cases**:
- AI-powered test generation for web apps
- Web scraping and automation
- Form filling and navigation
- Load testing
- GitHub Copilot integration for verifying generated code
- API testing within browser context

**Scope**:
- Web content only
- Relies on browser accessibility APIs
- Works with semantic HTML/ARIA

**Why Not Applicable**:
- Terminal UIs don't have accessibility trees
- Zellij is not browser-accessible
- Domain-specific (web) tool

**Interesting Aspect**:
- Uses structured state representation instead of visual parsing
- AI-native approach: gives AI the data it actually needs, not human-centric visual representation
- Works very well within its domain

---

## Gap

No tested approach provides:
- Continuous observation of state changes (not discrete snapshots)
- Works in actual development environment
- Reliable, low-latency feedback loop
- Can observe state transitions, not just end states
- Stable communication channel

Current options:
- Manual screenshots: works, reliable, but slow and breaks flow
- MCP screenshot: doesn't load in VSCode
- Computer Use: works in principle, but websocket stability and opacity issues make it frustrating for interactive debugging
- Playwright: works great but web-only

---

## Potential Direction Worth Exploring

Could a terminal state streaming tool work?
- Stream PTY output + rendered state continuously
- AI observes state changes in real-time
- Direct interaction with actual terminal session (not isolated container)
- Structured state (PTY stream) + visual rendering when needed

---

## Sources

- [GitHub - microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp)
- [Playwright MCP Explained: AI-Powered Test Automation 2026](https://www.testleaf.com/blog/playwright-mcp-ai-test-automation-2026/)
- [Using Playwright MCP with Claude Code | Simon Willison's TILs](https://til.simonwillison.net/claude-code/playwright-mcp-claude-code)
- [Anthropic Computer Use API Documentation](https://platform.claude.com/docs/en/docs/agents-and-tools/computer-use)
- [anthropics/anthropic-quickstarts computer-use-demo](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo)
