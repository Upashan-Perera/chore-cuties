# 🧸 Chore Cuties

A cute, phone-first chore tracker for two. Daily chores you can claim, weekly and monthly chores you both share, and a points scoreboard (week / month / all time).

## Put it online with GitHub Pages

1. Create a new repo on GitHub (e.g. `chore-cuties`).
2. Upload `index.html` to the repo root (Add file → Upload files).
3. Go to **Settings → Pages**, set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`, and save.
4. After a minute your site is live at `https://<your-username>.github.io/chore-cuties/`.
5. On each phone: open the link, then **Share → Add to Home Screen** (iPhone) or **⋮ → Add to Home screen** (Android) so it works like an app.

Without step "Sync" below, each phone keeps its own data. Do the sync setup so you both see the same points.

## Sync between your two phones (free, ~5 minutes)

GitHub Pages is static, so a tiny free database keeps you in sync.

1. Go to https://console.firebase.google.com and create a project (disable Analytics, it's not needed).
2. **Build → Firestore Database → Create database** (production mode, any region).
3. In the **Rules** tab, paste this and publish:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /households/{code} {
         allow read, write: if true;
       }
     }
   }
   ```
   This is open to anyone who knows the document name, so pick a hard-to-guess household code (e.g. `upa-and-bestie-7f3k9x`).
4. **Project settings (gear) → Your apps → Web (`</>`)**, register an app, and copy the `firebaseConfig` object.
5. In the chore app, open **Manage → Sync between phones**, enter your household code, paste the config, and tap **Connect sync**. Repeat on your partner's phone with the **same code and config**.

The "live" badge in Manage turns green when it's connected.

## Using it

- **Today**: the daily chores, all up for grabs. Tap **I've got it** to claim one, **Done** to finish it (whoever taps Done gets the points), or **Already done** to log it straight away.
- **Week / Month**: shared chores that reset every Monday / 1st of the month.
- **Points**: weekly, monthly and all-time scores, the effort split, and recent activity.
- **Manage**: add or remove chores, set points, rename the two of you, set up sync.
- Pick who you are with the toggle at the top of the screen (saved per phone).
