# 🐙 Git & GitHub Master Cheat Sheet 🛠️
Here is your complete, combined guide for essential commands and error troubleshooting.
### 💻 1. Essential Git Commands

| Command | Action | Description |
| :--- | :--- | :--- |
| git init | 📁 | Starts a brand new, empty repository in your folder. |
| git clone <url> | ⬇️ | Downloads an existing project from GitHub to your computer. |
| git status | 🔍 | Checks which files you have changed or added. |
| git add . | ➕ | Prepares all your changed files to be saved (staging). |
| git commit -m "..." | 💾 | Saves a local snapshot of your changes with a message. |
| git push -u origin main | ⬆️ | Uploads your saved changes to GitHub for the first time. |
| git push | ☁️ | Uploads your saved changes to GitHub (after the first time). |
| git pull origin main | 🔄 | Downloads any new updates from GitHub to your computer. |
| cd <folder> | 📂 | Moves your terminal into a specific folder. |

### 🚨 2. GitHub Error Troubleshooting Guide
**🌐 1. The Internet Connection Error**
 * **Error:** Temporary failure resolving 'in.archive.ubuntu.com'
 * **Why:** Your terminal lost internet connection or DNS is stuck.
 * **The Fix:** Restart your network manager.
   ```bash
   sudo systemctl restart NetworkManager
   sudo apt update
   
   ```
**🔑 2. The Authentication / Password Error**
 * **Error:** remote: Invalid username or token. Password authentication is not supported...
 * **Why:** You used your account password instead of a Personal Access Token (PAT).
 * **The Fix:** Generate a PAT in GitHub Settings. To make Git remember it forever:
   ```bash
   git config --global credential.helper store
   
   ```
**📭 3. The Empty Branch Error**
 * **Error:** error: src refspec main does not match any
 * **Why:** Your folder is empty. Git cannot create a save point without files.
 * **The Fix:** Create a dummy file and commit it.
   ```bash
   touch README.md
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   
   ```
**🛑 4. The Blocked Push (Secret Leak) Error**
 * **Error:** Push declined due to repository rule violations / Push cannot contain secrets
 * **Why:** You accidentally pasted a password/token inside your actual code.
 * **The Fix:** Delete the password text from your code, then wipe the corrupted history.
   ```bash
   rm -rf .git
   git init
   git branch -M main
   git add .
   git commit -m "Clean commit"
   git remote add origin https://github.com/WHOIAM27/name.git
   git push -u origin main --force
   
   ```
**⚠️ 5. The "Fetch First" / Unrelated Histories Error**
 * **Error:** [rejected] main -> main (fetch first) OR fatal: refusing to merge unrelated histories
 * **Why:** Files were created on GitHub (like a README) and locally at the same time.
 * **The Fix:** Force Git to download and merge the online files.
   ```bash
   git config pull.rebase false
   git pull origin main --allow-unrelated-histories
   git push -u origin main
   
   ```
**❌ 6. The "Not a Git Repository" Error**
 * **Error:** fatal: not a git repository (or any of the parent directories): .git
 * **Why:** You are trying to run Git commands in a folder that hasn't been initialized.
 * **The Fix:** Move into the correct folder first or initialize it.
   ```bash
   cd name-of-your-folder
   git init
   
   ```