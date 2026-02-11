# Troubleshooting

## Copilot Chat: "the specified API version is no longer supported"

### Error

```
Sorry, your request failed. Please try again.

Reason: client not supported: bad request: the specified API version is no longer supported.
You may need to update your client to a newer version.
```

### Cause

This error occurs when the GitHub Copilot extension in VS Code is using a deprecated API version that is no longer supported by GitHub's servers.

### Solution

1. **Update the GitHub Copilot extension**
   - Open VS Code
   - Go to the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`)
   - Search for "GitHub Copilot" and "GitHub Copilot Chat"
   - Click **Update** on both extensions if an update is available

2. **Update VS Code itself**
   - Go to `Help` > `Check for Updates`
   - Install any available updates and restart VS Code

3. **If the issue persists, reinstall the extensions**
   - Uninstall both "GitHub Copilot" and "GitHub Copilot Chat" extensions
   - Restart VS Code
   - Reinstall both extensions from the Extensions Marketplace

4. **Sign out and sign back in**
   - Click on the account icon in the bottom-left corner of VS Code
   - Sign out of your GitHub account
   - Sign back in and try Copilot Chat again
