# Firebase Cloud Sync Setup Guide

## Step 1: Create a Firebase Account

1. Go to https://firebase.google.com
2. Click "Get started" or "Go to console"
3. Sign in with your Google account

## Step 2: Create a New Firebase Project

1. Click "Add project" or "Create a project"
2. Enter a project name (e.g., "dictionary-tool")
3. Click "Continue"
4. Disable Google Analytics (not needed) or keep it enabled
5. Click "Create project"
6. Wait for the project to be created, then click "Continue"

## Step 3: Set Up Realtime Database

1. In the left sidebar, click "Build" → "Realtime Database"
2. Click "Create Database"
3. Choose a location (select one closest to you):
   - United States (us-central1)
   - Europe (europe-west1)
   - Asia (asia-southeast1)
4. Click "Next"
5. **Important:** Select "Start in test mode" (we'll secure it later)
6. Click "Enable"

## Step 4: Get Your Firebase Configuration

1. Click the gear icon (⚙️) next to "Project Overview" in the left sidebar
2. Click "Project settings"
3. Scroll down to "Your apps"
4. Click the web icon (</>) to add a web app
5. Give your app a nickname (e.g., "Dictionary Tool")
6. **Do NOT** check "Also set up Firebase Hosting"
7. Click "Register app"
8. You'll see a code snippet with your config. Copy the values:

```javascript
const firebaseConfig = {
  apiKey: "AIza...",              // Copy this
  authDomain: "your-project.firebaseapp.com",  // Copy this
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",  // Copy this
  projectId: "your-project",      // Copy this
  storageBucket: "your-project.appspot.com",  // Copy this
  messagingSenderId: "123456789",  // Copy this
  appId: "1:123456789:web:..."    // Copy this
};
```

## Step 5: Update Your HTML File

1. Open the `dictionary_tool_cloud_sync.html` file in a text editor
2. Find this section (around line 640):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

3. Replace it with YOUR values from Step 4
4. Save the file

## Step 6: Upload to GitHub Pages

1. Go to your GitHub repository (the one you created earlier)
2. Click "Add file" → "Upload files"
3. Upload the **updated** `dictionary_tool_cloud_sync.html` file
4. **Rename it to `index.html`** (replace the old one)
5. Commit the changes

Wait 1-2 minutes, then your auto-sync version will be live!

## Step 7: Secure Your Database (Important!)

Right now, anyone can read/write to your database. Let's secure it:

1. Go back to Firebase Console
2. Click "Realtime Database" in the left sidebar
3. Click the "Rules" tab
4. Replace the rules with this:

```json
{
  "rules": {
    "users": {
      "$userId": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

5. Click "Publish"

This allows anyone with a User ID to read and write their own data.

## How to Use

1. Open your website on any device
2. **Create a User ID** (e.g., "jerry_vocab_2025")
3. Use the SAME User ID on all your devices
4. That's it! Your vocabulary now syncs automatically! ✨

## Important Notes

- Use the SAME User ID on all devices to sync
- Don't share your User ID with others (they'll see your words)
- Export backups regularly just in case
- The free Firebase plan allows 100,000 simultaneous connections (more than enough!)

## Troubleshooting

**Problem:** "Translation failed" error
**Solution:** Check your internet connection

**Problem:** Records not syncing
**Solution:** 
1. Make sure you're using the exact same User ID on all devices
2. Check that you updated the Firebase config correctly
3. Open browser console (F12) and check for errors

**Problem:** Can't save records
**Solution:** Check Firebase Database rules are set correctly

---

Need help? The Firebase config is the most important step - make sure you copy all values correctly!
