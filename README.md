# SISORA — 100% Native Android Application (Kotlin + Jetpack Compose)

A **100% native Android APK** (`app.sisora.shop`) built with **Kotlin & Jetpack Compose** (no HTML, no WebView, no Capacitor).

Anyone can install `SISORA.apk` on their Android phone, but **a username and password are required to unlock and access boutique data**, with live multi-phone synchronization powered by **Firebase**, **Supabase**, or **Netlify**.

---

## Features Built Natively in Kotlin & Jetpack Compose

- **Username & Password Gate (`AuthScreen.kt`)**:
  - Data is locked behind **Sign in**, **Create shop**, and **Join shop**.
  - Usernames (e.g., `anna`) are automatically converted to private auth identifiers (`anna@sisora.app`) so no personal email or verification link is needed.
- **Multi-Cloud Live Sync (`CloudSyncClient.kt`)**:
  - Works out of the box with **Firebase** (Auth + Realtime Database), **Supabase** (Auth + Postgres), or **Netlify** (Netlify Functions + Blobs).
  - You can paste your cloud config directly inside the app's **☁️ Cloud** tab on first launch (no rebuild required!) OR pre-configure it in `app/src/main/java/app/sisora/shop/data/CloudConfig.kt`.
  - **1-Paste Full Invite Code**: When the shop owner copies the **Full Invite Code** from **Settings → Account & live cloud sync**, it bundles both the Cloud Config and the Shop Join Code (`SISORA1:...`). Any sister who installs `SISORA.apk` can simply paste that one code in **Join shop**, pick her username and password, and sign in immediately!
- **Complete Boutique Management**:
  - **Home**: Net profit banner, today's sales, stock count, total revenue, expenses, due payments, open orders, quick actions, and low-stock alerts.
  - **Stock & Outfits**: Native photo picker & compression, SKU codes, categories, sizes/variants, colors, cost & selling price, low-stock alerts, and sister ownership (`Jointly owned` or individual sister).
  - **Sales, Payments & Returns**: Record sales, partial/full payments, returns & exchanges (with automatic store credit transfer), and order delivery tracking (`Ordered` → `Packed` → `Shipped` → `Delivered`).
  - **Customers & WhatsApp Integration**: Customer book with spending history, due balances, 1-tap phone call (`ACTION_DIAL`), and 1-tap WhatsApp payment reminders & shipping notifications.
  - **Native Canvas Catalogue Generator (`CatalogueRenderer.kt`)**: Generates high-resolution (`1080px`) photo catalogue pages using Android's native `Canvas` & `Bitmap` and shares them directly to WhatsApp or Instagram via Android's native `FileProvider`.
  - **Profit Split & Settle-Up**: Equal or custom percentage profit sharing, sister-by-sister balance calculation, suggested transfers, and settlement history.
  - **Backup & CSV Exports**: Native JSON full backup & restore (including product photos) and CSV exports for Sales, Stock, Expenses, and Customers.

---

## Option A: Connect Firebase (Free)

1. Go to <https://console.firebase.google.com> and **Create a project**.
2. **Build → Authentication → Get started → Email/Password → Enable → Save.**
3. **Build → Realtime Database → Create database.**
4. Open the **Rules** tab, paste the contents of `database.rules.json`, and click **Publish**.
5. In **Project settings (gear icon) → General → Your apps → Web (`</>`)**, copy the `firebaseConfig` block and paste it into the app's **☁️ Cloud** tab (or into `CloudConfig.kt`).

## Option B: Connect Supabase (Free)

1. Create a project at <https://supabase.com>.
2. Go to **Authentication → Providers → Email** and turn **OFF** *Confirm email*.
3. Open **SQL Editor**, paste the contents of `supabase-schema.sql`, and click **Run**.
4. Copy your **Project URL** and **anon public key** from **Project Settings → API** and paste them into the app's **☁️ Cloud** tab (under `Supabase`).

## Option C: Connect Netlify (Free)

1. Deploy this repository to <https://app.netlify.com> (it includes `netlify.toml` and `netlify/functions/sisora.mjs` using Netlify Blobs).
2. Paste your Netlify site URL (`https://your-site.netlify.app`) into the app's **☁️ Cloud** tab (under `Netlify`).

---

## Building `SISORA.apk`

- **Pre-built APK**: `SISORA.apk` in the project root is already compiled, aligned, and signed with `signing/sisora.keystore`.
- **Local Gradle Build**:
  ```bash
  ./gradlew assembleRelease
  ```
- **GitHub Actions Cloud Build**:
  Push to GitHub — `.github/workflows/build-apk.yml` automatically builds and publishes the signed native `SISORA.apk` to **Releases** and **Artifacts**.
