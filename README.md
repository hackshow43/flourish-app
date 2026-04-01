# 🌿 Flourish

A home care and plant watering app for two. Built with Firebase Auth + Firestore, hosted on GitHub Pages.

## Features

- 🧹 **Cleaning schedules** — organized by room and frequency (daily / weekly / monthly / custom)
- 🔄 **Rotating assignments** — rooms auto-swap between household members each Monday, with manual override
- 📌 **Per-task assignment** — pin tasks to always be yours, your partner's, or shared
- 💤 **Snooze** — push any task to a future date
- 🌿 **Plant care tracker** — add plants with custom watering intervals, seasonal mode, and a built-in knowledge base of 35+ common houseplants
- 🔥 **Streak tracking** — household streak resets if weekly tasks go undone
- 🌱 **Week rollover** — on Monday, choose what to do with unfinished tasks
- 👤 **My Tasks filter** — focus on just your assigned tasks

## Setup

1. Create a Firebase project and enable **Google Auth** and **Firestore**
2. Copy your `firebaseConfig` into `index.html` (already done if you're reading this from the built repo)
3. Add Firestore security rules (see below)
4. Push to GitHub and enable Pages from **Settings → Pages → main branch → / (root)**

## Firestore Security Rules

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }

    match /households/{householdId} {
      allow read, write: if request.auth != null &&
        request.auth.uid in resource.data.members;
      allow create: if request.auth != null;
    }

    match /inviteCodes/{code} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
    }
  }
}
```

## File Structure

```
flourish/
├── index.html        ← Main app (all-in-one)
├── plants.json       ← Plant knowledge base (35+ species)
├── README.md
└── .gitignore
```

## .gitignore

```
firebase-config.js
.DS_Store
```

> Built with ❤️ for Jake & Em
