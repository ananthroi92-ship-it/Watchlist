# Ananth's Watchlist

A public, view-only GitHub Pages website for TV shows and movies grouped by genre and sorted by IMDb rating.

## What is included

- **Part 1 - TV Shows** grouped by genre
- **Part 2 - Movies** grouped by genre
- IMDb rating shown where available
- `NA` shown where the rating is not available or not confidently matched
- Search by title or genre
- Filter by genre
- TV Shows / Movies tabs
- Admin add panel structure for future Google login setup

## Project files

```text
.
├── index.html
├── README.md
├── SETUP.md
├── firebase.rules
├── firestore.indexes.json
├── .gitignore
└── LICENSE
```

## How to upload to GitHub

1. Create a new GitHub repository, for example:
   `ananth-watchlist`
2. Upload all files from this folder.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, choose:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/root`
5. Save.
6. GitHub will give you a public website URL.

## Public access

Everyone can view the page. Visitors cannot edit the page unless you configure the optional Firebase admin setup.

## Optional admin add feature

The `index.html` file already contains placeholders for:

- Firebase Google Sign-In
- Firestore database
- OMDb API lookup
- Admin email restriction

Open `SETUP.md` for full steps.

## Admin values to update inside `index.html`

```js
const FIREBASE_CONFIG = {
  apiKey: "",
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: ""
};

const ADMIN_EMAILS = ["ananthroi92@gmail.com"];
const OMDB_API_KEY = "";
```

## Notes

This is a static GitHub Pages project. GitHub Pages can display the site, but it cannot securely save new items by itself. Firebase/Firestore is recommended for login and saving new movies or TV shows.
