# 🐙 Git & GitHub Master Cheat Sheet 🛠️
Here is your complete, combined guide for essential commands and error troubleshooting.
### 💻 1. Essential Git Commands

| Command | Action | Description |
| :--- | :--- | :--- |
| 
```bash git init ```| 📁 | Starts a brand new, empty repository in your folder. |
|
```bash git clone https://github.com/WHOIAM27/name.git ```| ⬇️ | Downloads an existing project from GitHub to your computer. |
|
```bash git status ```| 🔍 | Checks which files you have changed or added. |
|
```bash git add . ```| ➕ | Prepares all your changed files to be saved (staging). |
|
```bash git commit -m "..." ```| 💾 | Saves a local snapshot of your changes with a message. |
|
```bash git push -u origin main ```| ⬆️ | Uploads your saved changes to GitHub for the first time. |
|
```bash git push ```| ☁️ | Uploads your saved changes to GitHub (after the first time). |
|
```bash git pull origin main ```| 🔄 | Downloads any new updates from GitHub to your computer. |
|
```bash cd <folder> ```| 📂 | Moves your terminal into a specific folder. |

### 🚨 2. GitHub Error Troubleshooting Guide
**🌐 1. The Internet Connection Error**
 * **Error:** Temporary failure resolving 'in.archive.ubuntu.com'
 * **Why:** Your terminal lost internet connection or DNS is stuck.
 * **The Fix:** Restart your network manager.

```bash
sudo systemctl restart NetworkManager
```
```bash
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
```

```bash
git add .
```

```bash
git commit -m "Initial commit"
```

```bash
git push -u origin main
```


**🛑 4. The Blocked Push (Secret Leak) Error**
 * **Error:** Push declined due to repository rule violations / Push cannot contain secrets
 * **Why:** You accidentally pasted a password/token inside your actual code.
 * **The Fix:** Delete the password text from your code, then wipe the corrupted history.
**The Fix (Clean Slate Method):**

 1. Open the .cpp file in a text editor and physically delete the password text. Save the file.
 2. Delete the corrupted local Git history:
   ```bash
rm -rf .git   
   ```

 3. Re-initialize and push fresh:
```bash
git init
```

```bash
git branch -M main
```

```bash
git add .
```

```bash
git commit -m "Clean commit"
```

```bash
git remote add origin https://github.com/WHOIAM27/name.git
```

```bash
git push -u origin main --force
```

**⚠️ 5. The "Fetch First" / Unrelated Histories Error**
 * **Error:** [rejected] main -> main (fetch first) OR fatal: refusing to merge unrelated histories
 * **Why:** Files were created on GitHub (like a README) and locally at the same time.
 * **The Fix:** Force Git to download and merge the online files.
```bash
git config pull.rebase false
```

```bash
git pull origin main --allow-unrelated-histories
```

```bash
git push -u origin main

```
**❌ 6. The "Not a Git Repository" Error**
 * **Error:** fatal: not a git repository (or any of the parent directories): .git
 * **Why:** You are trying to run Git commands in a folder that hasn't been initialized.
 * **The Fix:** Move into the correct folder first or initialize it.
   ```bash
cd name-of-your-folder
```
```bash
git init
   
   ```
