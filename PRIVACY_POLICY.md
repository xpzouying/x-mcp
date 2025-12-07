# Privacy Policy

**X-MCP Browser Extension**

*Last Updated: December 7, 2024*

## Introduction

This Privacy Policy explains how X-MCP ("we", "our", or "the Extension"), developed by Zouying, collects, uses, and protects your information when you use our Chrome browser extension.

X-MCP is an AI-powered assistant that helps users create and publish content on Xiaohongshu (Little Red Book). The extension connects to our backend service to enable automation features through the Model Context Protocol (MCP).

- **Homepage**: https://x.zouying.work/
- **GitHub**: https://github.com/xpzouying/x-mcp

## Information We Collect

### 1. Xiaohongshu Account Information

When you use the extension on Xiaohongshu pages, we may access:

- **Username/Nickname**: To display your login status
- **User ID**: To identify your account for operations
- **Login Status**: To verify you are logged in before performing actions

This information is read from the Xiaohongshu page you are viewing and is used only to execute the operations you request.

### 2. Configuration Data

The extension stores the following configuration locally in your browser:

- **API Key**: Your authentication token for connecting to our service
- **Server URL**: The backend server address (default: wss://mcp.zouying.work/ws)
- **Auto-reconnect preference**: Whether to automatically reconnect when disconnected

### 3. Operation Data

When you use the extension's features:

- **Tool execution history**: A record of operations performed (stored locally, limited to 50 entries)
- **Execution parameters**: The inputs you provide for each operation
- **Execution results**: The outcomes of operations

This data is stored locally in your browser's memory and local storage.

## How We Use Your Information

We use the collected information to:

1. **Execute Automation Operations**: Perform the content creation and publishing tasks you request
2. **Maintain Connection**: Keep a stable connection between your browser and our backend service
3. **Display Status**: Show you the current connection status and operation history
4. **Authenticate**: Verify your identity using your API Key

## Data Storage

### Local Storage

The following data is stored locally in your Chrome browser:

- API Key (encrypted in Chrome's local storage)
- Server URL and connection preferences
- Connection status information

### Temporary Storage

- Operation history is stored in memory and cleared when you close the browser
- Page data accessed during operations is not permanently stored

### We Do NOT Store

- Your Xiaohongshu password or login credentials
- The content of your posts (only transmitted to execute your requests)
- Your browsing history outside of Xiaohongshu

## Data Sharing

### Backend Service

When you use the extension, the following data is transmitted to our backend server at `mcp.zouying.work`:

- Your API Key (for authentication)
- Tool execution requests and parameters
- Operation results

### Third Parties

We do **NOT** share your personal information with any third parties. Specifically:

- We do not sell your data
- We do not share your Xiaohongshu account information
- We do not use your data for advertising

## Data Security

We implement the following security measures:

- **Encrypted Connection**: All communication uses encrypted WebSocket (wss://)
- **Local Storage**: Sensitive data like API Key is stored only in your browser
- **Code Protection**: Production code is obfuscated to prevent tampering
- **No Server-side Storage**: We do not store your personal data on our servers

## Permissions Explained

The extension requests the following Chrome permissions:

| Permission | Purpose |
|------------|---------|
| `tabs` | Access tab information to locate and operate on Xiaohongshu pages |
| `activeTab` | Get the current active tab to perform operations |
| `scripting` | Inject scripts to automate actions on Xiaohongshu pages |
| `storage` | Store your API Key and preferences locally |
| `webRequest` | Monitor network activity to determine when pages finish loading |
| `webNavigation` | Detect when page navigation completes for proper operation timing |

### Host Permissions

The extension only accesses the following websites:

- `*.xiaohongshu.com` - Required to perform automation on Xiaohongshu
- `localhost` / `127.0.0.1` - For local development only

## Your Rights

You have the right to:

1. **Access Your Data**: View what data the extension has stored by checking Chrome's extension storage
2. **Delete Your Data**: Clear all extension data by:
   - Going to Chrome Settings > Extensions > X-MCP > Remove
   - Or clearing the extension's local storage
3. **Revoke Access**: Generate a new API Key on https://x.zouying.work/ to invalidate the old one
4. **Disable Features**: Turn off auto-reconnect in the extension settings
5. **Uninstall**: Remove the extension at any time to stop all data collection

## Children's Privacy

This extension is not intended for use by children under 13 years of age. We do not knowingly collect personal information from children.

## Changes to This Policy

We may update this Privacy Policy from time to time. We will notify you of any changes by:

- Updating the "Last Updated" date at the top of this policy
- Posting the new policy on our GitHub repository

We encourage you to review this Privacy Policy periodically.

## Contact Us

If you have any questions or concerns about this Privacy Policy, please contact us:

- **GitHub Issues**: https://github.com/xpzouying/x-mcp/issues
- **Email**: xpzouying@gmail.com

---

By using the X-MCP browser extension, you agree to the collection and use of information in accordance with this Privacy Policy.
