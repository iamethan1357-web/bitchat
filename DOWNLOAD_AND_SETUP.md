# 📥 How to Download ToothChat Android Files

You need to get the files onto your computer first. Here are 3 easy methods:

---

## 🎯 METHOD 1: Download from GitHub (EASIEST!) ⭐

Since I already pushed the iOS changes, let's use a similar approach for Android.

### Step 1: Fork the Original Android Repo

1. Go to: **https://github.com/permissionlesstech/bitchat-android**
2. Look at the TOP RIGHT corner
3. Click **"Fork"** button
4. You'll see "Create a new fork" page
5. **Repository name**: Leave it as `bitchat-android` OR change to `toothchat-android`
6. Click **"Create fork"**
7. Wait 10-20 seconds for it to fork

✅ Now you have your own copy!

### Step 2: Download the Forked Repo

**Option A: Download as ZIP**
1. Go to YOUR forked repo: `https://github.com/YOUR_USERNAME/bitchat-android`
2. Click the green **"Code"** button (top right of file list)
3. Click **"Download ZIP"**
4. Wait for download to complete
5. Find the ZIP file in your Downloads folder
6. **Extract/Unzip it** (right-click → Extract on Windows, or double-click on Mac)

**Option B: Clone with GitHub Desktop (Recommended for Beginners)**
1. Download GitHub Desktop: **https://desktop.github.com/**
2. Install it and sign in with your GitHub account
3. Click **"File"** → **"Clone Repository"**
4. Select your forked repo from the list
5. Choose where to save it on your computer
6. Click **"Clone"**

---

## 🎯 METHOD 2: I'll Create a Simple Rebranding Script

Since the original files are large, here's a simpler approach:

### Step 1: Download Original Repo
Follow the steps in Method 1 to download the original bitchat-android repo

### Step 2: Apply These Changes Manually

I'll give you exact commands to change "bitchat" to "ToothChat":

**For Windows (PowerShell):**
```powershell
# Navigate to the folder
cd C:\Users\YourName\Downloads\bitchat-android

# Change app name in strings.xml
(Get-Content app\src\main\res\values\strings.xml) -replace 'bitchat', 'ToothChat' | Set-Content app\src\main\res\values\strings.xml

# Change package name in build.gradle.kts
(Get-Content app\build.gradle.kts) -replace 'com\.bitchat\.droid', 'com.toothchat.app' | Set-Content app\build.gradle.kts
```

**For Mac/Linux (Terminal):**
```bash
# Navigate to the folder
cd ~/Downloads/bitchat-android

# Change app name
sed -i '' 's/bitchat/ToothChat/g' app/src/main/res/values/strings.xml

# Change package name
sed -i '' 's/com\.bitchat\.droid/com.toothchat.app/g' app/build.gradle.kts
```

### Step 3: Replace the App Icon
1. Download the ToothChat icon I created (it's in the bitchat repo)
2. Go to: `app/src/main/res/mipmap-xxxhdpi/`
3. Replace `ic_launcher.png` with the new icon
4. Do the same for all mipmap folders (hdpi, mdpi, xhdpi, xxhdpi, xxxhdpi)

---

## 🎯 METHOD 3: Use GitHub Web Editor (No Download Needed!)

### Step 1: Fork the Repo
1. Go to: **https://github.com/permissionlesstech/bitchat-android**
2. Click **"Fork"** (top right)
3. Wait for it to fork

### Step 2: Edit Files Online
1. Go to YOUR forked repo
2. Navigate to: `app/src/main/res/values/strings.xml`
3. Click the **pencil icon** (Edit this file) at top right
4. Use Ctrl+F (or Cmd+F) to find: `bitchat`
5. Replace with: `ToothChat`
6. Scroll down and click **"Commit changes"**
7. Repeat for other files

**Files to Edit:**
- `app/src/main/res/values/strings.xml` - Change "bitchat" to "ToothChat"
- `app/build.gradle.kts` - Change `com.bitchat.droid` to `com.toothchat.app`
- `app/src/main/AndroidManifest.xml` - Change URL scheme and permissions

### Step 3: Add GitHub Actions Workflow
1. In your fork, click **"Add file"** → **"Create new file"**
2. Type: `.github/workflows/build-apk.yml`
3. Copy the workflow content I created (I'll provide it below)
4. Click **"Commit new file"**

---

## 📋 COMPLETE WORKFLOW FILE

Copy this entire content and save it as `.github/workflows/build-apk.yml`:

```yaml
name: Build APK for Download

on:
  workflow_dispatch:
  push:
    branches: [main, master]
    tags:
      - "v*.*.*"

permissions:
  contents: write

env:
  SETUP_JAVA_VERSION: 21.0.11+10.0.LTS

jobs:
  build-apk:
    name: Build Release APK
    runs-on: ubuntu-24.04

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '21'

      - name: Set up Gradle
        uses: gradle/actions/setup-gradle@v3

      - name: Build debug APK
        run: ./gradlew assembleDebug

      - name: Upload APK to Actions
        uses: actions/upload-artifact@v4
        with:
          name: ToothChat-APK
          path: app/build/outputs/apk/debug/*.apk

      - name: Create GitHub Release with APK
        if: startsWith(github.ref, 'refs/tags/')
        uses: softprops/action-gh-release@v2
        with:
          files: app/build/outputs/apk/debug/*.apk
          name: "ToothChat ${{ github.ref_name }}"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

  create-latest-release:
    name: Update Latest Release
    runs-on: ubuntu-24.04
    if: github.ref == 'refs/heads/main' || github.ref == 'refs/heads/master'
    needs: build-apk

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '21'

      - name: Set up Gradle
        uses: gradle/actions/setup-gradle@v3

      - name: Build debug APK
        run: ./gradlew assembleDebug

      - name: Rename APK
        run: |
          mkdir -p release
          cp app/build/outputs/apk/debug/*.apk release/ToothChat-latest.apk

      - name: Delete old latest release
        run: |
          gh release delete latest --yes 2>/dev/null || true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Create latest release
        uses: softprops/action-gh-release@v2
        with:
          tag_name: latest
          name: "ToothChat - Latest Build"
          body: |
            ## 📲 ToothChat APK Download
            
            **Download the APK file below to install on your Android device.**
            
            ### Installation Instructions
            1. Tap the `ToothChat-latest.apk` file below to download
            2. Open the downloaded file on your Android phone
            3. If prompted, allow "Install from unknown sources"
            4. Tap Install
          files: release/ToothChat-latest.apk
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

## 🎯 MY RECOMMENDATION: Use Method 3!

**Why Method 3 is best:**
- ✅ No need to download large files
- ✅ No need for terminal/Git knowledge
- ✅ Everything happens in your browser
- ✅ GitHub automatically saves your changes
- ✅ You can see changes immediately

---

## 📝 Step-by-Step for Method 3 (Web Editor)

### Phase 1: Fork the Repository

1. **Open browser** and go to: https://github.com/permissionlesstech/bitchat-android

2. **Find the Fork button** (top right, next to "Watch" and "Star")

3. **Click "Fork"**

4. **Wait** for GitHub to create your copy (10-20 seconds)

5. You'll be redirected to: `https://github.com/YOUR_USERNAME/bitchat-android`

✅ **You now have your own copy!**

---

### Phase 2: Change the App Name

1. **Navigate to strings.xml**:
   - Click on `app` folder
   - Click on `src` folder
   - Click on `main` folder
   - Click on `res` folder
   - Click on `values` folder
   - Click on `strings.xml`

2. **Edit the file**:
   - Look at the TOP RIGHT of the file
   - Click the **pencil icon** (✏️) that says "Edit this file"

3. **Find and replace**:
   - Press `Ctrl+F` (Windows) or `Cmd+F` (Mac) to open search
   - Type: `bitchat`
   - Press Enter to find all occurrences
   - For each one, change it to: `ToothChat`
   
   **Most important one:**
   - Find this line: `<string name="app_name">bitchat</string>`
   - Change to: `<string name="app_name">ToothChat</string>`

4. **Save the changes**:
   - Scroll DOWN to the bottom of the page
   - You'll see a box that says "Commit changes"
   - Leave the default message or type: "Rebrand to ToothChat"
   - Click the green button: **"Commit changes"**

✅ **App name changed!**

---

### Phase 3: Change the Package Name

1. **Navigate to build.gradle.kts**:
   - Click on the repository name at the top to go back to root
   - Click on `app` folder
   - Click on `build.gradle.kts`

2. **Edit the file**:
   - Click the **pencil icon** (Edit this file) at top right

3. **Find and change**:
   - Press `Ctrl+F` or `Cmd+F`
   - Find: `com.bitchat.droid`
   - Replace with: `com.toothchat.app`
   
   - Find: `com.bitchat.android`
   - Replace with: `com.toothchat.android`

4. **Commit changes**:
   - Scroll down
   - Click **"Commit changes"**

✅ **Package name changed!**

---

### Phase 4: Add the Build Workflow

1. **Go back to the root of your repo**:
   - Click on your repository name at the top

2. **Create new file**:
   - Click **"Add file"** button (green, near top right)
   - Click **"Create new file"**

3. **Name the file**:
   - In the text box that says "Name your file...", type:
   ```
   .github/workflows/build-apk.yml
   ```
   - Note: This creates folders automatically!

4. **Paste the workflow content**:
   - Copy the entire YAML content I provided above (in the "COMPLETE WORKFLOW FILE" section)
   - Paste it into the large text box

5. **Commit the file**:
   - Scroll down
   - Type: "Add APK build workflow"
   - Click **"Commit new file"**

✅ **Workflow added!**

---

### Phase 5: Trigger the Build

1. **Go to Actions tab**:
   - Click **"Actions"** at the top of your repo

2. **You might see a message**:
   - "Workflows aren't being run on this forked repository"
   - Click **"I understand my workflows, go ahead and enable them"**

3. **Manual trigger**:
   - Click **"Build APK for Download"** on the left
   - Click **"Run workflow"** (blue button on the right)
   - Click the green **"Run workflow"** button in the dropdown

4. **Wait for build**:
   - Refresh the page
   - You'll see the workflow running (yellow circle)
   - Wait 5-10 minutes
   - It will turn green when complete ✅

---

### Phase 6: Download the APK

1. **Go to Releases**:
   - Click **"Releases"** on the right sidebar
   - Or go to: `https://github.com/YOUR_USERNAME/bitchat-android/releases`

2. **Find the latest release**:
   - Look for "ToothChat - Latest Build"
   - Click on it

3. **Download the APK**:
   - Scroll down to "Assets"
   - Click **`ToothChat-latest.apk`**
   - Wait for download

✅ **You have the APK!**

---

## 🎉 That's It!

You've successfully:
- ✅ Forked the original repo
- ✅ Changed the app name to ToothChat
- ✅ Changed the package name
- ✅ Added automatic APK building
- ✅ Downloaded the APK

Now share the download link with your users!

---

## 📱 Share the APK

Your APK download link:
```
https://github.com/YOUR_USERNAME/bitchat-android/releases/download/latest/ToothChat-latest.apk
```

Replace `YOUR_USERNAME` with your actual GitHub username!

---

## ❓ Troubleshooting

**Can't find the Fork button?**
- Make sure you're logged into GitHub
- The button is at the very top right, next to "Watch" and "Star"

**Changes not saving?**
- Make sure you scroll down and click "Commit changes"
- Wait for the page to reload

**Build not starting?**
- Go to Actions tab
- Click "I understand my workflows, go ahead and enable them"
- Manually trigger the workflow

**Can't find the APK?**
- Make sure the build completed (green checkmark)
- Go to Releases tab, not Actions tab

---

## 🆘 Need More Help?

Let me know which step you're stuck on and I'll walk you through it!
