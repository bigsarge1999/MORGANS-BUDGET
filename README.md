# Family Mission Budget (plain HTML/CSS/JS — no Node, no npm)

A budget app for your household with the **official 2026 Army pay chart** built in, so you can
pull your wife's Captain (O-3) pay straight into the budget. This version is plain HTML, CSS,
and JavaScript — nothing to install on your computer, no build step. You just push the files to
GitHub and turn on GitHub Pages, and it connects to Firebase directly from the browser.

**What it does:**
- Auto-fills base pay from the real DFAS 2026 pay tables (pick rank + years of service)
- Tracks all household income, expenses (with a pie chart), and savings goals
- Signs in with email/password and syncs across devices in real time via Firebase

---

## Step 1: Create your free Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com), sign in with any
   Google account, click **Add project** → name it `family-budget` → Create.
2. Left sidebar → **Build → Authentication** → **Get started** → click **Email/Password** →
   toggle **Enabled** → **Save**.
3. Left sidebar → **Build → Firestore Database** → **Create database** → pick a location →
   **Production mode** → **Enable**.
4. Click the gear icon (top-left) → **Project settings** → scroll to **Your apps** → click the
   **</>** (web) icon → nickname it `budget-web` → **Register app**. It'll show you a code block
   with `apiKey`, `authDomain`, `projectId`, etc. Keep that tab open.
5. Still in Project settings, click the **Rules** tab under Firestore Database (or find it in
   the Firestore Database section), and paste in the contents of `firestore.rules` from this
   folder, replacing whatever's there. Click **Publish**. This makes sure only you and your wife
   can ever read your own budget data.

## Step 2: Drop your Firebase keys into the code

1. Open `js/firebase-init.js` in any text editor (even Notepad or TextEdit works).
2. Replace the placeholder values (`YOUR_API_KEY`, `YOUR_PROJECT_ID`, etc.) with the real values
   Firebase showed you in Step 1.4. Save the file.

## Step 3: Push it to GitHub

1. Go to [github.com](https://github.com), create a free account if needed.
2. Click **+** → **New repository** → name it `family-budget` → you can leave it Public (a
   Private repo can't use the free version of GitHub Pages) → **Create repository**.
3. On the empty repo's page, click **uploading an existing file**, then drag in every file and
   folder from this project (`index.html`, the `js` folder, `firestore.rules`, `README.md`).
   Scroll down, click **Commit changes**.
   - (If you prefer the command line instead of drag-and-drop, GitHub shows those exact commands
     on that same page — `git init`, `git add .`, `git commit`, `git push`.)

## Step 4: Turn on GitHub Pages (this is your live website)

1. In your repo, click **Settings** (top menu) → **Pages** (left sidebar).
2. Under "Build and deployment," set **Source** to **Deploy from a branch**.
3. Set **Branch** to `main` and folder to `/ (root)`, click **Save**.
4. Wait about a minute, then refresh the page — GitHub will show you a live link like:
   `https://YOUR-USERNAME.github.io/family-budget/`
   That's your permanent website. Bookmark it on both phones.

## Step 5: Tell Firebase to trust your new website

Firebase blocks sign-in from domains it doesn't recognize, so one last step:

1. Back in the Firebase console → **Build → Authentication** → **Settings** tab →
   **Authorized domains** → **Add domain**.
2. Enter `YOUR-USERNAME.github.io` (just the domain, no `https://` and no trailing slash) →
   **Add**.

Now open your GitHub Pages link, create an account, and you should see the budget dashboard.

---

## Using the pay chart

The **2026 Military Pay Chart** card lets you pick Pay Scale, Rank, and Years of Service, shows
the exact DFAS monthly base pay, and drops it into your income list with one tap ("Apply to
Income") along with the 2026 BAS rate. **BAH isn't on the chart** because it depends on duty
station ZIP code and dependents — look it up on the
[DoD BAH calculator](https://www.travel.dod.mil/Allowances/Basic-Allowance-for-Housing/BAH-Calculator/)
or the LES and type it into the BAH row.

Pay charts update once a year, usually every January. When 2027 rates are out, just ask Claude
to update the numbers in `js/payData.js`, re-upload that one file to GitHub, and GitHub Pages
updates automatically within a minute or two.

---

## Making changes later

Any time you want to change something, edit the file, then on the GitHub repo page click into
that file → the pencil (edit) icon → make your change → **Commit changes**. GitHub Pages
re-publishes automatically, usually within a minute.

## Notes

- Both of you can sign into the same account (same email/password) from your own phones, or ask
  to have this set up as two separate logins sharing one household budget instead.
- If you ever see a blank page again, the most common cause is a typo in the Firebase keys in
  `js/firebase-init.js`, or forgetting Step 5 (authorized domain). Open the page, right-click →
  **Inspect** → **Console** tab, and the red error text there will usually say exactly what's wrong.
