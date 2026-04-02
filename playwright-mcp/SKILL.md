---
name: playwright-mcp
description: Playwright MCP integration for full browser automation — navigate, click, type, screenshot, evaluate JS, handle dialogs, upload files, fill forms, and run custom Playwright code snippets. Use for end-to-end testing, scraping, form automation, or any browser interaction beyond the simpler workspace browser. Triggers on mentions of Playwright, browser automation, E2E testing, or headless browser scripting.
---

# Playwright MCP Integration

## When to use this skill
- End-to-end browser testing with full Playwright API access
- Complex browser automation (multi-step flows, form fills, file uploads)
- Running custom Playwright code snippets
- Taking screenshots for visual regression testing
- Evaluating JavaScript in the browser context
- Handling dialogs (alert, confirm, prompt)
- Network request monitoring and interception
- Drag-and-drop interactions

## How to access tools
All tools are prefixed with `mcp__plugin_playwright_playwright__`. Use `ToolSearch` with query `"+playwright"` to fetch schemas.

## Tool Inventory

### Navigation & Pages

| Tool | Purpose |
|------|---------|
| `browser_navigate` | Navigate to a URL |
| `browser_navigate_back` | Go back in history |
| `browser_tabs` | List open browser tabs |
| `browser_close` | Close the page |
| `browser_resize` | Resize the browser viewport |
| `browser_wait_for` | Wait for a condition (selector, text, timeout) |

### Interaction

| Tool | Purpose |
|------|---------|
| `browser_click` | Click an element by ref |
| `browser_type` | Type text into an element |
| `browser_hover` | Hover over an element |
| `browser_drag` | Drag and drop between elements |
| `browser_press_key` | Press a keyboard key |
| `browser_select_option` | Select dropdown option |
| `browser_file_upload` | Upload files to file input |
| `browser_fill_form` | Fill an entire form at once |
| `browser_handle_dialog` | Accept/dismiss browser dialogs |

### Observation

| Tool | Purpose |
|------|---------|
| `browser_snapshot` | Get accessibility tree snapshot of the page |
| `browser_take_screenshot` | Take a screenshot (full page or element) |
| `browser_console_messages` | Get console log messages |
| `browser_network_requests` | Get network request/response data |
| `browser_evaluate` | Run JavaScript in page context |

### Advanced

| Tool | Purpose |
|------|---------|
| `browser_run_code` | Run arbitrary Playwright code snippet |

## Common Patterns

### Basic page interaction flow
```
1. browser_navigate(url="https://example.com")
2. browser_snapshot() -> get element refs
3. browser_click(ref="element-ref")
4. browser_type(ref="input-ref", text="hello")
5. browser_take_screenshot()
```

### Element references
Playwright MCP uses `ref` attributes from the accessibility snapshot, NOT CSS selectors. Always call `browser_snapshot()` first to get the current element refs.

### Running custom Playwright code
Use `browser_run_code` for complex automation:
```javascript
async (page) => {
  await page.goto('https://example.com');
  await page.getByRole('button', { name: 'Submit' }).click();
  return await page.title();
}
```

### Form automation
```
1. browser_navigate(url) -> go to form page
2. browser_snapshot() -> get element refs
3. browser_fill_form(fields=[{ref, value}, ...]) -> fill all fields at once
4. browser_click(ref="submit-button-ref")
5. browser_wait_for(condition) -> wait for success state
```

### Visual testing workflow
```
1. browser_navigate(url)
2. browser_resize(width=1280, height=720)
3. browser_take_screenshot(filename="desktop.png")
4. browser_resize(width=375, height=812)
5. browser_take_screenshot(filename="mobile.png")
```

## Playwright MCP vs Workspace Browser

| Feature | Playwright MCP | Workspace Browser |
|---------|---------------|-------------------|
| Element refs | Accessibility tree refs | CSS selectors |
| Custom code | `browser_run_code` | Not available |
| Form filling | `browser_fill_form` | Manual per-field |
| File uploads | `browser_file_upload` | Not available |
| Network monitoring | `browser_network_requests` | Not available |
| Dialog handling | `browser_handle_dialog` | Not available |
| Shared across agents | Yes (MCP) | Yes (MCP) |
| Best for | Complex automation, E2E tests | Quick checks, simple interactions |

## Important Notes
- Always call `browser_snapshot()` before interacting — you need element `ref` values
- `browser_run_code` accepts an async function with `page` parameter (full Playwright Page API)
- Screenshots can be saved to files with the `filename` parameter
- Console messages can be filtered by level: error, warning, info, debug
- Network requests include full request/response data for debugging
