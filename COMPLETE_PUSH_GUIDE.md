# 🦷 ToothChat Android - Complete Push Guide (Beginner Friendly)

This guide assumes you have NO experience with Git or GitHub. Follow every single step exactly.

---

## 📚 TABLE OF CONTENTS
1. [Create GitHub Account (if needed)](#part-1-create-github-account)
2. [Create the Repository](#part-2-create-the-repository)
3. [Push the Code](#part-3-push-the-code)
4. [Check the Build](#part-4-check-the-build)
5. [Download the APK](#part-5-download-the-apk)
6. [Share with Users](#part-6-share-with-users)

---

## PART 1: Create GitHub Account

### ⚠️ SKIP THIS PART if you already have a GitHub account

**Step 1:** Go to https://github.com/signup

**Step 2:** Enter your email address
- Use a real email you can access
- Click "Continue"

**Step 3:** Create a password
- Must be at least 8 characters
- Must have a number and lowercase letter
- Click "Continue"

**Step 4:** Choose a username
- This will be in your URL: `github.com/YOUR_USERNAME`
- Remember this username - you'll need it later!
- Click "Continue"

**Step 5:** Email preferences
- Type "y" for yes or "n" for no
- Click "Continue"

**Step 6:** Solve the puzzle
- Complete the robot check
- Click "Create account"

**Step 7:** Check your email
- Open the email from GitHub
- Click the verification link
- Enter the code on the GitHub page

✅ **You now have a GitHub account!**

---

## PART 2: Create the Repository

### Step 2.1: Go to GitHub

1. Open your web browser (Chrome, Firefox, Safari, etc.)
2. In the address bar, type: **github.com**
3. Press Enter
4. If not logged in, click **"Sign in"** at the top right
5. Enter your username and password
6. Click **"Sign in"**

### Step 2.2: Navigate to Create New Repository

**Method 1 (Easiest):**
1. Look at the TOP RIGHT corner of the page
2. You'll see a **"+"** icon (plus sign)
3. Click the **"+"** icon
4. Click **"New repository"** from the dropdown menu

**Method 2 (Direct URL):**
1. In your browser address bar, type: **github.com/new**
2. Press Enter

### Step 2.3: Fill in Repository Details

You'll now see a form. Fill it in EXACTLY like this:

#### Field 1: Repository name
- Find the text box labeled **"Repository name"**
- Type exactly: `toothchat-android`
- ⚠️ **IMPORTANT**: Use lowercase, no spaces, exact spelling

#### Field 2: Description (optional)
- Find the text box labeled **"Description"**
- Type: `ToothChat - Decentralized P2P mesh messaging for Android`
- This is optional but helpful

#### Field 3: Public or Private?
- You'll see two options:
  - 🔘 **Public** - Anyone on the internet can see this repository
  - 🔘 **Private** - You choose who can see and commit
- ✅ **SELECT: Public** (click the radio button next to "Public")
- ⚠️ **This MUST be public for users to download the APK!**

#### Field 4: Initialize this repository with
You'll see checkboxes:
- ☐ **Add a README file** - ❌ **DO NOT CHECK THIS**
- ☐ **Add .gitignore** - ❌ **DO NOT CHECK THIS**
  - Even if you click the dropdown, leave it as "None"
- ☐ **Choose a license** - ❌ **DO NOT CHECK THIS**

⚠️ **IMPORTANT**: None of these should be checked!

### Step 2.4: Create the Repository

1. Scroll down to the bottom of the page
2. Find the green button that says **"Create repository"**
3. Click it!

### Step 2.5: Copy Your Repository URL

After clicking, you'll see a new page. It will show:

**"Quick setup"**

Look for a section that says:
```
…or push an existing repository from the command line
```

Below that, you'll see a text box with a URL that looks like:
```
https://github.com/YOUR_USERNAME/toothchat-android.git
```

**YOUR_USERNAME** will be replaced with your actual GitHub username.

**Example:**
If your username is `johnsmith123`, the URL will be:
```
https://github.com/johnsmith123/toothchat-android.git
```

**COPY THIS URL!** You'll need it in the next part.

**How to copy:**
1. Click inside the text box with the URL
2. The entire URL should highlight (turn blue)
3. Right-click and select "Copy" OR press Ctrl+C (Windows) or Cmd+C (Mac)

✅ **Your repository is created and URL is copied!**

---

## PART 3: Push the Code

### Step 3.1: Open Terminal

**On Windows:**
1. Press `Windows key + X`
2. Select "Windows Terminal" or "PowerShell"

**On Mac:**
1. Press `Cmd + Space` to open Spotlight
2. Type "Terminal"
3. Press Enter

**On Linux:**
1. Press `Ctrl + Alt + T`

### Step 3.2: Navigate to the Android Folder

Type this command in the terminal and press Enter:

```bash
cd /home/user/toothchat-android
```

**What this does:** Changes to the toothchat-android folder where all the code is

**Verify you're in the right place:**
Type this and press Enter:
```bash
ls
```

You should see files like:
- app/
- gradle/
- README.md
- build.gradle.kts
- etc.

### Step 3.3: Update the Remote URL

**⚠️ IMPORTANT: Replace YOUR_USERNAME with your actual GitHub username!**

Type this command (but replace YOUR_USERNAME first!):

```bash
git remote set-url origin https://github.com/YOUR_USERNAME/toothchat-android.git
```

**Example:**
If your GitHub username is `johnsmith123`, type:
```bash
git remote set-url origin https://github.com/johnsmith123/toothchat-android.git
```

**What this does:** Tells Git where to push the code (your new GitHub repository)

### Step 3.4: Verify the URL Was Set

Type this command:
```bash
git remote -v
```

You should see output like:
```
origin  https://github.com/YOUR_USERNAME/toothchat-android.git (fetch)
origin  https://github.com/YOUR_USERNAME/toothchat-android.git (push)
```

If you see YOUR_USERNAME instead of the old URL, you're good!

### Step 3.5: Push the Code

Type this command and press Enter:
```bash
git push -u origin toothchat-rebrand:main
```

**What this does:**
- `git push` - Uploads code to GitHub
- `-u` - Sets up tracking (so future pushes are easier)
- `origin` - The remote repository (your GitHub repo)
- `toothchat-rebrand:main` - Pushes the local branch and renames it to "main"

### Step 3.6: GitHub Authentication Popup

When you run the push command, a popup will appear asking for your GitHub credentials.

**Popup 1: Username**
- A box will appear saying "Username for 'https://github.com':"
- Type your GitHub username
- Press Enter

**Popup 2: Password**
- A box will appear saying "Password for 'https://YOUR_USERNAME@github.com':"
- Here's where it gets tricky:

#### If you DON'T have Two-Factor Authentication (2FA):
- Type your GitHub password
- Press Enter

#### If you HAVE Two-Factor Authentication (2FA) enabled:
You need a Personal Access Token instead of your password.

**How to create a Personal Access Token:**

1. Open a NEW browser tab
2. Go to: **https://github.com/settings/tokens**
3. You might need to enter your password again
4. Click the green button **"Generate new token"**
5. Click **"Generate new token (classic)"**
6. Fill in the form:
   - **Note**: Type `toothchat-push` (or any name you want)
   - **Expiration**: Select "No expiration" (or 90 days, whatever you prefer)
   - **Select scopes**: Check the box next to **"repo"** (it should say "Full control of private repositories")
   - Scroll down if needed to see "repo"
7. Scroll to the bottom
8. Click the green button **"Generate token"**
9. **IMPORTANT**: You'll see a long string of letters and numbers like:
   ```
   ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   ```
10. **COPY THIS TOKEN IMMEDIATELY!**
    - Click the copy icon next to it
    - OR select it all and press Ctrl+C / Cmd+C
    - You WON'T see it again after you leave this page!

**Now go back to the terminal:**
- In the password field, paste your token (Ctrl+V or Cmd+V)
- The characters won't show as you paste - this is normal and secure!
- Press Enter

### Step 3.7: Wait for Push to Complete

You'll see output like this:
```
Enumerating objects: 1234, done.
Counting objects: 100% (1234/1234), done.
Delta compression using up to 8 threads
Compressing objects: 100% (890/890), done.
Writing objects: 100% (1234/1234), 45.67 MiB | 12.34 MiB/s, done.
Total 1234 (delta 234), reused 1000 (delta 200)
remote: Resolving deltas: 100% (234/234), done.
To https://github.com/YOUR_USERNAME/toothchat-android.git
 * [new branch]      toothchat-rebrand -> main
Branch 'toothchat-rebrand' set up to track 'main' from 'origin'.
```

✅ **SUCCESS!** Your code is now on GitHub!

---

## PART 4: Check the Build

### Step 4.1: Go to Your Repository

1. Open your browser
2. Go to: **github.com/YOUR_USERNAME/toothchat-android**
3. Replace YOUR_USERNAME with your actual username
4. Press Enter

You should see all your project files!

### Step 4.2: Check the Actions Tab

1. Look at the tabs at the top of the page:
   - **Code** | **Issues** | **Pull requests** | **Actions** | ...
2. Click on **"Actions"**

### Step 4.3: View the Build Progress

You should see a list of workflow runs:
- **"Build APK for Download"**
- It will have a yellow circle (⏳) or green checkmark (✅)
- Click on the workflow run to see details

### Step 4.4: Monitor the Build

The build takes 5-10 minutes. You'll see:
- **Queued** - Waiting to start
- **In progress** - Currently building (yellow circle)
- **Success** - Build completed! (green checkmark)

You can click on individual jobs to see the logs in real-time.

### Step 4.5: Wait for Completion

Just wait! The build will finish automatically.

✅ **Build complete when you see a green checkmark!**

---

## PART 5: Download the APK

### Step 5.1: Go to Releases

1. On your repository page, look at the RIGHT sidebar
2. Find **"Releases"**
3. Click **"latest"** (or the number of releases)

**Alternative:**
1. Go to: **github.com/YOUR_USERNAME/toothchat-android/releases**

### Step 5.2: Find the APK

You should see a release titled:
**"ToothChat - Latest Build"**

Below that, in the **"Assets"** section, you'll see:
- `ToothChat-latest.apk` (with a download icon)

### Step 5.3: Download the APK

1. Click on **`ToothChat-latest.apk`**
2. The download will start automatically
3. Wait for it to complete
4. The file will be in your Downloads folder

✅ **You now have the ToothChat APK!**

---

## PART 6: Share with Users

### Step 6.1: Direct Download Link

Your APK has a permanent download URL:
```
https://github.com/YOUR_USERNAME/toothchat-android/releases/download/latest/ToothChat-latest.apk
```

Replace YOUR_USERNAME with your actual username.

**Example:**
```
https://github.com/johnsmith123/toothchat-android/releases/download/latest/ToothChat-latest.apk
```

### Step 6.2: Share the Link

You can share this link via:
- **Email** - Send to friends/colleagues
- **WhatsApp/Telegram** - Share in groups
- **Social Media** - Post on Twitter, Facebook, etc.
- **Website** - Add a download button
- **QR Code** - Generate a QR code for the URL

### Step 6.3: How Users Install

Tell your users:
1. Click the link on their Android phone
2. The APK file will download
3. Open the downloaded file
4. If prompted, tap "Allow from this source" or "Allow unknown sources"
5. Tap "Install"
6. Wait for installation to complete
7. Tap "Open" to launch ToothChat!

---

## 🎯 QUICK REFERENCE COMMANDS

Copy and paste these commands (but replace YOUR_USERNAME!):

```bash
# Go to the folder
cd /home/user/toothchat-android

# Set your GitHub URL (REPLACE YOUR_USERNAME!)
git remote set-url origin https://github.com/YOUR_USERNAME/toothchat-android.git

# Push the code
git push -u origin toothchat-rebrand:main
```

---

## ❌ COMMON PROBLEMS & SOLUTIONS

### Problem: "Repository not found"
**Solution:**
- Check that you created the repository with the exact name: `toothchat-android`
- Make sure the repository is **Public**
- Verify you replaced YOUR_USERNAME with your actual username

### Problem: "Authentication failed"
**Solution:**
- Double-check your username spelling
- If using 2FA, make sure you're using a Personal Access Token, not your password
- Try creating a new token: https://github.com/settings/tokens

### Problem: "Permission denied"
**Solution:**
- Make sure you're logged into the correct GitHub account
- Verify the repository belongs to your account
- Try logging out and back into GitHub in your browser

### Problem: Build fails in GitHub Actions
**Solution:**
- Click on the failed workflow
- Read the error logs
- Common issues: missing dependencies, network timeouts
- Try re-running the workflow (click "Re-run jobs")

### Problem: Can't find the APK
**Solution:**
- Go to your repository
- Click "Actions" tab
- Wait for the build to complete (green checkmark)
- Then go to "Releases" tab
- The APK will be there

---

## 🆘 STILL NEED HELP?

If you're stuck:
1. Take a screenshot of the error
2. Check which step you're on
3. Review the troubleshooting section above
4. Try the solution provided

**Remember:**
- Replace YOUR_USERNAME everywhere with your actual GitHub username
- The repository must be PUBLIC
- Use a Personal Access Token if you have 2FA enabled

---

## ✅ CHECKLIST

Before you start, make sure you have:
- [ ] GitHub account
- [ ] Terminal/command prompt open
- [ ] Code is in /home/user/toothchat-android
- [ ] Enough time (15-20 minutes total)

After completing:
- [ ] Created GitHub repository
- [ ] Pushed code successfully
- [ ] Build completed (green checkmark)
- [ ] Downloaded APK
- [ ] Shared the link with users

---

**🎉 Congratulations! You've successfully deployed ToothChat!**
