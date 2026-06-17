# Adeptly — Cloud version (real logins + cross-device sharing)

This version uses **Firebase** for real accounts and a shared database, so a teacher can
assign a test on her device and a student opens it on **their own** device — and results
flow back to the teacher automatically.

You set this up once. It's free for this scale (Firebase Spark plan).

---

## Step 1 — Create a Firebase project (5 min)
1. Go to **console.firebase.google.com** and sign in with a Google account.
2. Click **Add project** → name it `masar` → continue (you can disable Google Analytics) → **Create project**.

## Step 2 — Turn on Email/Password login
1. In the left menu: **Build → Authentication → Get started**.
2. Open the **Sign-in method** tab → click **Email/Password** → toggle **Enable** → **Save**.

## Step 3 — Create the database
1. Left menu: **Build → Firestore Database → Create database**.
2. Choose a location (e.g. `eur3` or nearest) → start in **Production mode** → **Create**.
3. Open the **Rules** tab, delete what's there, paste the contents of **`firestore.rules`** (in this folder), and click **Publish**.

## Step 4 — Get your config and paste it in
1. Click the **gear icon** (top-left) → **Project settings**.
2. Scroll to **Your apps** → click the **</>** (Web) icon → register an app called `masar` (you do NOT need Hosting here) → **Register app**.
3. You'll see a `firebaseConfig = { ... }` block. Copy those values into **`firebase-config.js`** in this folder (replace every `PASTE_...`).

## Step 5 — Put it online (so people can reach it)
Easiest: **Netlify Drop**.
1. Go to **app.netlify.com/drop**.
2. Drag this whole **Adeptly-Cloud** folder onto the page.
3. You get a live URL like `https://your-name.netlify.app` — that's your app.

(Alternatively use Firebase Hosting or any static host.)

## Step 6 — Allow your web address to log in
1. Back in Firebase → **Authentication → Settings → Authorized domains → Add domain**.
2. Add your Netlify domain (e.g. `your-name.netlify.app`). `localhost` is allowed by default.

## Done — try it
- Open your URL, **Register** as a **Teacher**, add a student + assign a test.
- On another device (or browser), open the same URL, **Register** as that **Student** (same email) → the test is on their dashboard → they take it → the result appears on your teacher dashboard.

---

## Notes
- The student's full practice/plan/tracker data stays on the device where they take the test; the **result summary** (scores, level, skills, written response) syncs to the cloud so the teacher sees it anywhere.
- The included rules are fine for a school pilot. For wider use, tighten them (e.g. restrict assignment reads to the matching teacher/student). I can harden them when you're ready.
- Files in this folder: `index.html` (the app), `curriculum.js`, `questions.js`, `firebase-config.js` (your keys), `firestore.rules`, `sw.js`.
