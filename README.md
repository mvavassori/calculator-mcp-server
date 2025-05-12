# Calculator MCP Server

A comprehensive calculator implemented as a Model Context Protocol (MCP) server using TypeScript.

This server exposes a wide range of mathematical functions as MCP tools, allowing language models connected via MCP clients (like Claude for Desktop, Cursor, etc.) to perform calculations.

## Features

Provides MCP tools for:

*   **Basic Arithmetic:** Addition, Subtraction, Multiplication, Division
*   **Exponents & Roots:** Power (`^`), Square Root
*   **Trigonometry:** Sine, Cosine, Tangent (input in radians)
*   **Inverse Trigonometry:** Arcsine, Arccosine, Arctangent, Arctan2 (output in radians)
*   **Degree/Radian Conversion:** Convert between degrees and radians
*   **Logarithms:** Natural Log (ln), Base-10 Log (log10), Log with arbitrary base
*   **Constants:** Pi (π), Euler's number (e)
*   **Factorial:** `n!`
*   **Percentage:** Calculate percentage of a number
*   **Modulo:** Remainder operation
*   **Absolute Value:** `abs()`
*   **Rounding:** Floor, Ceiling, Round to nearest integer

## Prerequisites

*   [Node.js](https://nodejs.org/) (v16 or higher recommended)
*   [npm](https://www.npmjs.com/) (usually included with Node.js)

## Installation

1.  Clone the repository:
    ```bash
    git clone https://github.com/mvavassori/calculator-mcp-server.git
    ```

2.  Navigate into the project directory:
    ```bash
    cd calculator-mcp-server
    ```

3.  Install dependencies:
    ```bash
    npm install
    ```

## Building the Server

- Build the TypeScript code:
    ```bash
    npm run build
    ```
    This compiles the code into the `build` directory.

## Connecting to Clients (Claude Desktop Example)

This server communicates using the MCP stdio transport. To connect it to Claude for Desktop:

1.  **Find Claude Desktop's MCP Configuration File:**
    *   **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
    *   **Windows:** `%APPDATA%\Claude\claude_desktop_config.json` (You can paste this path into the File Explorer address bar).
    *   **Linux:** `~/.config/Claude/claude_desktop_config.json`
    *   If the file or the `Claude` directory doesn't exist, you might need to create it, or open Claude Desktop's Settings (`Claude Menu > Settings... > Developer > Edit Config`) which should create the file for you.

2.  **Edit the Configuration File:** Open the `claude_desktop_config.json` file in a text editor.

3.  **Add the Server Configuration:** Modify the file to include the `mcpServers` object with your calculator server entry. If the file was empty or didn't exist, its entire content should look like this:

    ```json
    {
      "mcpServers": {
        "calculator": {
          "command": "node",
          "args": [
            "/home/marco/code/calculator-mcp-server/build/index.js"
            // IMPORTANT: Replace this path with the ACTUAL ABSOLUTE PATH
            // to the 'build/index.js' file on YOUR system.
          ]
        }
        // You can add other servers here under different keys, like:
        // "another_server": { ... }
      }
    }
    ```

    **Notes:**
    *   **CRITICAL:** Replace `/home/marco/code/calculator-mcp-server/build/index.js` with the correct *absolute path* to the `build/index.js` file within your cloned project directory on your computer.
    *   On Windows, use double backslashes (`\\`) for the path separators, e.g., `"C:\\Users\\YourUser\\path\\to\\calculator-mcp-server\\build\\index.js"`.
    *   The key `"calculator"` is just a name you give this server connection within Claude's config; it can be anything descriptive.
    *   If the `mcpServers` object already exists, just add the `"calculator": { ... }` entry inside it, separated by a comma if other servers are present.

4.  **Restart Claude for Desktop:** Ensure Claude for Desktop is fully closed and reopened for the new configuration to take effect.

Claude for Desktop should now show the MCP tools icon (a hammer <img src="https://mintlify.s3.us-west-1.amazonaws.com/mcp/images/claude-desktop-mcp-hammer-icon.svg" style="display: inline; margin: 0; height: 1em;"/> ) and be able to use the calculator tools when you ask it to perform calculations.

## License

MIT License
