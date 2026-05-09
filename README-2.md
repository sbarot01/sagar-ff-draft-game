# Sagar's Gridiron Dash — Setup Guide

A football endless runner for determining fantasy draft order. Players dodge defenders, accumulate yards, and the leaderboard sets the draft picks.

---

## What you'll need

- A Google account (for Firebase)
- A GitHub account (for hosting)
- Roughly 20 minutes total

---

## Part 1: Firebase Setup (10 min)

### 1. Create a Firebase project
1. Go to https://console.firebase.google.com
2. Click **"Add project"**
3. Name it: `sagars-gridiron-dash` (or whatever you want)
4. **Disable Google Analytics** when asked (not needed)
5. Click **"Create project"** and wait ~30 seconds

### 2. Create the Firestore database
1. In the project dashboard, click **"Build" → "Firestore Database"** in the left sidebar
2. Click **"Create database"**
3. Select **"Start in production mode"** (we'll set rules in step 4)
4. Pick the **`us-east1` (South Carolina)** region — closest to NC
5. Click **"Enable"** and wait ~30 seconds

### 3. Register the web app and get your config
1. Click the **gear icon** (top left) → **"Project settings"**
2. Scroll down to **"Your apps"** and click the **`</>`** (web) icon
3. Nickname: `gridiron-dash-web`
4. **DO NOT** check "Set up Firebase Hosting" — we're using GitHub Pages
5. Click **"Register app"**
6. You'll see a `firebaseConfig` object — **copy the whole thing**, it looks like:
   ```javascript
   const firebaseConfig = {
     apiKey: "AIzaSyD...",
     authDomain: "sagars-gridiron-dash.firebaseapp.com",
     projectId: "sagars-gridiron-dash",
     storageBucket: "sagars-gridiron-dash.appspot.com",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abc123"
   };
   ```
7. Save this somewhere — you'll paste it into `index.html` in Part 3

### 4. Set the security rules
1. Go back to **"Firestore Database"** → click the **"Rules"** tab at the top
2. Delete what's there
3. Paste the contents of the `firestore.rules` file from this folder
4. Click **"Publish"**

✅ **Firebase done.**

---

## Part 2: GitHub Pages Setup (5 min)

### 1. Create the repo
1. Go to https://github.com/new
2. Repository name: `sagars-gridiron-dash`
3. Set to **Public** (required for free GitHub Pages)
4. Check **"Add a README file"**
5. Click **"Create repository"**

### 2. Upload the game
1. In your new repo, click **"Add file" → "Upload files"**
2. Drag `index.html` from this folder (after you've pasted your Firebase config — see Part 3)
3. Commit message: `Initial game upload`
4. Click **"Commit changes"**

### 3. Enable GitHub Pages
1. In the repo, click **"Settings"** (top right of the repo)
2. In the left sidebar, click **"Pages"**
3. Under "Build and deployment":
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `(root)`
4. Click **"Save"**
5. Wait ~1 minute, then refresh the page
6. Your URL will appear at the top: `https://YOUR_USERNAME.github.io/sagars-gridiron-dash/`

✅ **Hosting done.** Share that URL with your league.

---

## Part 3: Paste Your Firebase Config Into the Game

Open `index.html` and find this block near the top:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY_HERE",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

Replace it with the config you copied from Firebase in Part 1, Step 3.

Save the file, then upload it to your GitHub repo (or push it via git).

---

## Updating the game later

Just edit `index.html` locally, then upload the new version to GitHub (or `git push`). GitHub Pages auto-redeploys in ~30 seconds.

---

## Viewing all scores

Anytime you want to see every score ever submitted (not just the top per player):
1. Firebase Console → Firestore Database → Data tab
2. Click the `scores` collection
3. You'll see every entry with player, yards, and timestamp

---

## Resetting the leaderboard

If you want to wipe scores before the real draft order competition:
1. Firebase Console → Firestore Database → Data tab
2. Click the `scores` collection
3. Three-dot menu → "Delete collection"

---

## Roster

The 12 preset names are baked in. To change them, edit the `ROSTER` array in `index.html`:

```javascript
const ROSTER = [
  'Sagar', 'Devon', 'Vishal', 'Kishan', 'Daanyal', 'Drew',
  'Will', 'Phil', 'Josh', 'Kaleb', 'Shyam', 'Fletch'
];
```
