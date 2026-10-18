# Calorie Column

A personal diet planner. Each day is one vertical column whose height is your calorie budget. You fill it with food blocks sized by their calories. The protein bar fills as you go.

The app works as soon as you open `index.html`, saving data on that device. Follow the steps below to put it online and sync your iPhone and laptop.

## 1. Put it on GitHub Pages (about 5 minutes)

1. Create a new GitHub repository, for example `calorie-column`. It can be private if you have GitHub Pro; otherwise make it public (your food data is not stored in the repo).
2. Upload everything in this folder: `index.html`, `config.js`, `sw.js`, `manifest.webmanifest`, `firestore.rules`, and the `icons` folder.
3. Repository → **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.
4. After a minute your app is at `https://<your-username>.github.io/calorie-column/`.

## 2. Turn on sync with Firebase (about 10 minutes)

1. Go to <https://console.firebase.google.com> → **Add project** (Google Analytics not needed).
2. **Build → Authentication → Get started → Email/Password → Enable.**
3. **Build → Firestore Database → Create database** → production mode → pick a nearby region (e.g. `europe-west`).
4. Firestore → **Rules** tab → replace everything with the contents of `firestore.rules` → **Publish**.
5. **Project settings (gear) → Your apps → Web (`</>`)** → register the app → copy the `firebaseConfig` object.
6. Open `config.js`, replace `null` with that object (an example is in the file), and upload it to GitHub again.
7. **Authentication → Settings → Authorized domains → Add domain** → `<your-username>.github.io`.
8. Open the app → Settings → Sync → **Create account** with your email and a password. On the other device, use **Sign in**.
9. Optional but recommended: Authentication → Settings → **User actions** → turn off *Enable create (sign-up)* so nobody else can register.

Whatever you already entered on a device is uploaded the first time you sign in there.

## 3. Install on iPhone

Open the GitHub Pages link in **Safari** → Share → **Add to Home Screen**. It opens full-screen like an app and works offline; changes sync when you're back online.

## How the numbers work

- **BMR:** Mifflin-St Jeor.
- **TDEE:** BMR × 1.2, plus 0.0005 kcal per kg per step above 3,000 steps. At 89 kg and 10,000 steps that is about 2,470 kcal.
- **Budget:** TDEE × (1 − deficit). At 25% that's about 1,855 kcal. Switch to a fixed number in Settings if you prefer.
- **Protein:** 1.8 g per kg of adjusted body weight (ideal weight + 40% of the excess), which comes to about 130 g. Adjustable in Settings.

Carbs and fat for Nabil escalope, rice, vegetables, dates and the sauces are estimates; edit them anytime (Edit → tap the block).

## Using it

- **Add:** tap a block, or drag it into the column (on iPhone, hold for a moment, then drag).
- **Change a portion:** tap a block in the column → − / + or type an exact amount.
- **Remove:** tap it → Remove, or hold it and drag it out of the column. Every removal has an Undo.
- **Meals:** the Meals tab holds saved combinations, added in one tap.
- **One-offs:** rare meals with estimated totals. Add from “+ One-off meal” under the column.
- **Scrap day:** marks the day as off. It stays visible but is left out of the weekly averages. “Restore day” undoes it.
- **Edit / delete foods:** turn on Edit in the pantry, then tap any block.
- **Week:** Sunday to Saturday, with calories, protein, and the foods for each day.
- **Backup:** Settings → Copy backup gives you all your data as text.

## Food-estimation chat

Create a separate Claude project for estimating foods and paste the text from `food-chat-instructions.md` into its instructions. Each answer then ends with a JSON block. In the app: **+ Add → Import from the food chat** → paste → Import.

## Editing the app

`index.html` is the whole app. Keep developing it in the development chat; replace the file on GitHub with each new version.
