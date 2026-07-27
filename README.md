# GITHUB-ERRORS
Here is the ultimate master guide to every error we encountered today and exactly how to fix them. You can save this as a permanent cheat sheet for your Ubuntu terminal!
### 1. The Internet Connection Error
**The Error:** Temporary failure resolving 'in.archive.ubuntu.com'

**Why it happens:** Your Ubuntu terminal has lost connection to the internet or its DNS is stuck, preventing you from installing or updating packages like git.
**The Fix:**
Restart your network manager to force it to reconnect, then try your update again:
```bash
sudo systemctl restart NetworkManager
```
```bash
sudo apt update
```

### 2. The Authentication / Password Error
**The Error:** **remote: Invalid username or token. Password authentication is not supported for Git operations.**

**Why it happens:** You typed in your normal GitHub account password, or you pasted a Personal Access Token (PAT) that had a typo or was expired.
**The Fix:**
GitHub requires a token for terminal uploads.
 1. Go to GitHub **Settings** > **Developer settings** > **Personal access tokens** > **Tokens (classic)**.
 2. Generate a new token and check the **repo** box.
 3. Run git push origin main again, and paste that token when asked for the password.
   *(Bonus permanent fix: Run git config --global credential.helper store so Git saves the token and stops asking you for it).*
### 3. The Empty Branch Error
**The Error: **error: src refspec main does not match any**
**Why it happens:** You tried to push code, but your folder was completely empty. Git cannot create a branch or a save point without at least one file.
**The Fix:**
Create a simple dummy file, save it, and then push:
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

### 4. The Blocked Push (Secret Leak) Error
**The Error: **Push declined due to repository rule violations / Push cannot contain secrets**

**Why it happens:** You accidentally pasted your GitHub Personal Access Token (or another password) inside your actual .cpp code files. GitHub's security scanner caught it and blocked the upload to protect your account.
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

### 5. The "Fetch First" / Unrelated Histories Error
**The Error: **[rejected] main -> main (fetch first) OR fatal: refusing to merge unrelated histories**

**Why it happens:** You created files locally on your computer AND you created files online on GitHub (like a README) at the same time. Git refuses to overwrite the online files because it doesn't know how they connect to your local files.
**The Fix:**
Force Git to download the online files and merge them with your local code:
```bash
git config pull.rebase false
```

```bash
git pull origin main --allow-unrelated-histories
```

```bash
git push -u origin main

```
*(To prevent this permanently: Always create a completely empty repository on GitHub without checking any README/License boxes if you already have local code).*
### 6. The "Not a Git Repository" Error
**The Error: **fatal: not a git repository (or any of the parent directories): .git**

**Why it happens:** You are trying to run commands like git add . in a normal computer folder that hasn't been turned into a Git project, or you are sitting outside of your cloned project folder.
**The Fix:**
Move into the correct folder first using the cd command, or initialize the folder:
```bash
cd name-of-your-folder

```
*(If it's a brand new folder, run git init inside it first).*
