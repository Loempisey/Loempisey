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

---

## Docker Compose: Port 3306 already in use

### Error

```
ERROR: for db  Cannot start service db: driver failed programming external connectivity on endpoint
cpbank_db (...): failed to bind port 0.0.0.0:3306/tcp: Error starting userland proxy: listen tcp4
0.0.0.0:3306: bind: address already in use
```

### Cause

Port 3306 (the default MySQL port) is already occupied by another process on the host machine. This typically happens when:

- A local MySQL server is already running on the host
- Another Docker container is already using port 3306

### Solution

1. **Find and stop the process using port 3306**

   On Linux/macOS:
   ```bash
   sudo lsof -i :3306
   # or
   sudo ss -tlnp | grep 3306
   ```
   On Windows (PowerShell):
   ```powershell
   netstat -ano | findstr :3306
   ```
   Then stop the conflicting process:
   ```bash
   # If it's a local MySQL service
   sudo systemctl stop mysql
   # or
   sudo service mysql stop
   ```

2. **Stop any conflicting Docker container**
   ```bash
   docker ps --filter "publish=3306"
   docker stop <container_id>
   ```

3. **Or change the host port mapping in `docker-compose.yml`**

   If you want to keep the existing MySQL running, remap the container's port to a different host port:
   ```yaml
   services:
     db:
       ports:
         - "3307:3306"   # Maps host port 3307 to container port 3306
   ```
   Then connect to MySQL on port `3307` instead of `3306`.
