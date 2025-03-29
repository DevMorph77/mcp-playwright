
# Playwright MCP Automation Server  

This project integrates **Playwright** with the **MCP (Modular Command Protocol)** framework to enable web automation and testing through natural language or programmatic interaction. It allows you to:  
- Open websites and extract information.  
- Click elements and perform actions.  
- Take screenshots.  
- Generate test cases.  
- Create JSON test reports.  

You can prompt tools like **Claude** (or any other LLM) to perform browser automation, generate tests, and provide feedback.

---

## Features  
- Web Automation: Interact with websites using Playwright.  
- Test Case Generation: Create automated test scripts.  
- Screenshots: Capture web pages for reporting.  
- JSON Reports: Save test outcomes for analysis.  

---

## Project Structure  
playwright-mcp/  
- **playwright_mcp.py** — MCP Server for Playwright automation  
- **mcp-config.json** — MCP Server configuration  
- **playwright_tests/** — Generated test cases  
- **reports/** — Screenshots and test reports  
- **requirements.txt** — Required dependencies  
- **README.md** — Project documentation  

---

## Prerequisites  
Make sure you have **Python 3.8+** installed.

1. Clone the Repository:  
```bash
git clone https://github.com/yourusername/playwright-mcp.git
cd playwright-mcp
```

2. Set Up a Virtual Environment (Optional):  
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install Required Dependencies:  
```bash
pip install -r requirements.txt
playwright install
```

---

## Configuration  

**mcp-config.json** — MCP configuration file.  

```json
{
    "mcpServers": {
        "playwright-mcp": {
            "command": "python",
            "args": ["playwright_mcp.py"],
            "host": "127.0.0.1",
            "port": 8080,
            "timeout": 30000
        }
    }
}
```

---

## Usage  

1. Run the MCP Server:  
```bash
python playwright_mcp.py
```

You should see:  
```
🚀 Starting Playwright MCP server on 127.0.0.1:8080
```

---

## Available Tools  

**1. Open Website**  
```json
{
  "tool": "open_website",
  "inputs": {
    "url": "https://example.com"
  }
}
```

Result:  
```json
{
  "result": "Page title: Example Domain"
}
```

---

**2. Click Element**  
```json
{
  "tool": "click_element",
  "inputs": {
    "url": "https://example.com",
    "selector": "button#submit"
  }
}
```

Result:  
```json
{
  "result": "Clicked element with selector: button#submit"
}
```

---

**3. Extract Text**  
```json
{
  "tool": "extract_text",
  "inputs": {
    "url": "https://example.com",
    "selector": "h1"
  }
}
```

Result:  
```json
{
  "result": "Extracted text: Example Domain"
}
```

---

**4. Take Screenshot**  
```json
{
  "tool": "take_screenshot",
  "inputs": {
    "url": "https://example.com",
    "filename": "example_screenshot.png"
  }
}
```

Result:  
```json
{
  "result": "Screenshot saved to reports/example_screenshot.png"
}
```

---

**5. Generate Test Case**  
```json
{
  "tool": "generate_test_case",
  "inputs": {
    "url": "https://example.com",
    "action": "click",
    "selector": "button#submit"
  }
}
```

Result:  
```json
{
  "result": "Test case saved to playwright_tests/test_123456.py"
}
```

---

**6. Generate Report**  
```json
{
  "tool": "generate_report",
  "inputs": {
    "status": "Passed",
    "details": "All tests passed successfully."
  }
}
```

Result:  
```json
{
  "result": "Report saved to reports/report_123456.json"
}
```

---

## Stopping the Server  
Press **CTRL+C** to stop the MCP server.

---

## Extending the Project  
You can create additional tools by adding more `@mcp.tool()` functions to the **playwright_mcp.py** file.  

For example:  

```python
@mcp.tool()
async def get_url(page_url: str) -> str:
    """Returns the current URL."""
    async with async_playwright() as pw:
        browser = await pw.chromium.launch(headless=False)
        page = await browser.new_page()
        await page.goto(page_url)
        current_url = page.url
        await browser.close()
        return current_url
```

---

## Contributing  
Contributions are welcome! Feel free to open issues or submit pull requests.

---

## Troubleshooting  
- **Playwright Not Found?**  
  Run:  
  ```bash
  playwright install
  ```
  
- **Port Already in Use?**  
  Modify the **port** in **mcp-config.json**.

---

## Contact  
For any issues or suggestions, feel free to reach out!  

---

