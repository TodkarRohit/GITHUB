# 🐙 Git & GitHub Master Cheat Sheet 🛠️
Here is your complete, combined guide for essential commands and error troubleshooting.
### 💻 1. Essential Git Commands

| Command | Action | Description |
| :--- | :--- | :--- |
| git init | 📁 | Starts a brand new, empty repository in your folder. |
| git clone https://github.com/WHOIAM27/name.git | ⬇️ | Downloads an existing project from GitHub to your computer. |
| git status | 🔍 | Checks which files you have changed or added. |
| git add . | ➕ | Prepares all your changed files to be saved (staging). |
| git commit -m "..." | 💾 | Saves a local snapshot of your changes with a message. |
| git push -u origin main  | ⬆️ | Uploads your saved changes to GitHub for the first time. |
| git push | ☁️ | Uploads your saved changes to GitHub (after the first time). |
|  git pull origin main | 🔄 | Downloads any new updates from GitHub to your computer. |
| cd <folder> | 📂 | Moves your terminal into a specific folder. |

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


### 7. The "Non-Fast-Forward" Error
**The Error:** ! [rejected] main -> main (non-fast-forward)
**Why it happens:** Your local repository on your computer is behind the online repository on GitHub (usually because changes were made directly on the GitHub website, or pushed from a different computer). Git blocks your push to prevent you from accidentally deleting those newer online changes.
**The Fix:**
Download the latest changes from GitHub to your computer first, let Git combine them, and then push again:
```bash
git pull origin main

```
```bash
git push origin main

```
*(If you DO NOT care about the online files and want to completely overwrite the GitHub repository with your current local code, use the force push command instead):*
```bash
git push -u origin main --force

```


### 8. The Merge Conflict Error
**The Error:** Automatic merge failed; fix conflicts and then commit the result. (or CONFLICT (add/add))
**Why it happens:** Git noticed that the code you have on your computer is different from the code currently sitting on GitHub for the exact same files. It doesn't know which version to keep, so it hits the "pause" button and locks your terminal from pushing until you make a decision.
**The Fix:**
If your goal is to completely overwrite the GitHub files with your local, clean files, you can cancel the stuck merge and force the push:
 1. Cancel the confusing merge process and unfreeze the terminal:
```bash
git merge --abort

```
 2. Force your computer's files to overwrite the GitHub repository:
```bash
git push -u origin main --force

```

### 9. The "Diverged Branches & Unsaved Changes" Error
**The Error:** Your branch and 'origin/main' have diverged AND error: Your local changes to the following files would be overwritten by merge
**Why it happens:** GitHub has new updates that your computer doesn't have, and your computer has new saved commits that GitHub doesn't have. Git wants to sync them up using git pull, but it refuses to do so because you have *unsaved* edits in some of your files. Git freezes to protect your unsaved work from being deleted.
**The Fix:**
Use the stash command to temporarily hide your unsaved edits in a "magic drawer", sync the branches, push your code, and then bring your unsaved edits back.
 1. Hide your unsaved changes so Git stops complaining:
```bash
git stash

```
 2. Download the missing files from GitHub and sync everything:
```bash
git pull origin main

```
 3. Upload your saved code to GitHub:
```bash
git push origin main

```
 4. *(Optional)* Bring your unsaved edits back out of the "magic drawer" so you can keep working on them:
```bash
git stash pop

```


