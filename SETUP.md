# Setup Guide

This guide explains how to publish the watchlist website and optionally enable private admin adding.

## 1. Publish the public watchlist on GitHub Pages

1. Go to GitHub.
2. Create a new repository, for example `ananth-watchlist`.
3. Upload these files:
   - `index.html`
   - `README.md`
   - `SETUP.md`
   - `LICENSE`
   - `.gitignore`
   - `firebase.rules`
   - `firestore.indexes.json`
4. Open the repository.
5. Go to **Settings → Pages**.
6. Select:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/root`
7. Click **Save**.
8. Wait until GitHub shows your live website URL.

Your page will work immediately as a public view-only website.

---

## 2. Optional: Enable Google login and add movie/TV show feature

Use this only if you want to log in and add new items from the website.

### Step A: Create a Firebase project

1. Go to Firebase Console.
2. Click **Add project**.
3. Create a project, for example `ananth-watchlist`.
4. Go to **Project settings → General**.
5. Under **Your apps**, add a Web app.
6. Copy the Firebase config.

Paste the config into `index.html` here:

```js
const FIREBASE_CONFIG = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### Step B: Enable Google Sign-In

1. In Firebase, go to **Authentication → Sign-in method**.
2. Enable **Google**.
3. Add your GitHub Pages domain to authorized domains if needed.

Example domain:

```text
ananthroi92.github.io
```

### Step C: Create Firestore database

1. Go to **Firestore Database**.
2. Create database.
3. Start in production mode.
4. Use the rules from `firebase.rules`.

The page stores new items in a Firestore collection named:

```text
watchlist
```

### Step D: Add your admin email

Inside `index.html`, keep only your allowed email:

```js
const ADMIN_EMAILS = ["ananthroi92@gmail.com"];
```

Only this Google account will see the admin add panel after sign-in.

### Step E: Add OMDb API key

1. Create an OMDb API key.
2. Paste it inside `index.html`:

```js
const OMDB_API_KEY = "YOUR_OMDB_API_KEY";
```

This lets the page look up title, genre, year, IMDb ID, and IMDb rating.

---

## 3. Important security note

The OMDb API key placed in `index.html` is visible to users because GitHub Pages is static.

For a personal watchlist project this may be acceptable. For a production-grade app, use a backend or serverless function so the API key is not exposed.

---

## 4. How adding works after setup

1. You open your GitHub Pages website.
2. You click **Sign in with Google**.
3. If your email matches `ADMIN_EMAILS`, the admin panel appears.
4. Enter a movie or TV show title.
5. Click **Lookup source**.
6. The page fills genre and IMDb rating from OMDb.
7. Click **Save item**.
8. The new item is saved in Firestore.
9. Public visitors can see the updated item, but they cannot add or edit.
