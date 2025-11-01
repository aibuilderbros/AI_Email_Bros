Perfect 🎉 — glad it’s working now!
Here’s a **README.md–style guide** you can drop directly into your project for future reference 👇

---

# 🚀 Deploying Expo React Native Web App to Netlify

This guide explains how to build, deploy, and update an **Expo React Native Web** app on **Netlify** — including how to fix routing issues (`Page not found`).

---

## 🧰 Prerequisites

* Node.js 18+ (recommended: latest LTS)
* Expo CLI installed:

  ```bash
  npm install -g expo-cli
  ```
* A [Netlify](https://www.netlify.com/) account connected to your GitHub repo

---

## ⚙️ Project Setup

### 1. Enable Web Support

If your project was created with Expo:

```bash
npx expo start --web
```

This verifies your app runs in the browser.

---

### 2. Create `_redirects` File

Netlify needs this file to handle client-side routing correctly.

Create a file at:

```
public/_redirects
```

Add this line inside:

```
/* /index.html 200
```

This ensures that all unknown routes are redirected to your app’s main `index.html`.

---

### 3. Update `package.json` Build Script

Add this script to your `package.json`:

```json
{
  "scripts": {
    "build:web": "expo export --platform web && cp public/_redirects dist/_redirects"
  }
}
```

This tells Expo to export the web build and copy the `_redirects` file into the output folder.

---

## 🚀 Deploying to Netlify

### 1. In Netlify, set these build settings:

* **Build command:**

  ```bash
  npm install && npm run build:web
  ```
* **Publish directory:**

  ```
  dist
  ```

### 2. Commit and push your code to GitHub

Netlify will automatically:

* Install dependencies
* Build the web app
* Copy `_redirects`
* Deploy the site from the `dist/` folder

---

## 🔄 Updating / Redeploying After Edits

When you edit your code:

1. Save changes locally
2. Commit and push:

   ```bash
   git add .
   git commit -m "Update app"
   git push
   ```
3. Netlify automatically rebuilds and redeploys your site 🎯

> 🧠 Tip: You **don’t need to manually run `expo export` or redeploy manually** unless you’re using drag-and-drop uploads.

---

## 🧹 Manual Redeploy (Optional)

If you want to rebuild manually (without Git):

```bash
npm run build:web
```

Then drag and drop the **`dist/`** folder into [https://app.netlify.com/drop](https://app.netlify.com/drop).

---

## 🧩 Common Issues

| Problem                          | Cause                     | Fix                                     |
| -------------------------------- | ------------------------- | --------------------------------------- |
| 404 “Page not found” on subpages | Missing `_redirects` file | Add `/* /index.html 200` and redeploy   |
| Site not updating after edit     | Cache or old build        | Clear Netlify cache and redeploy        |
| Assets missing                   | Wrong publish folder      | Ensure `dist` is your publish directory |

---

## ✅ Example Directory Structure

```
my-app/
├─ app/                     # Expo app routes & screens
├─ public/
│  └─ _redirects
├─ dist/                    # Generated after build
├─ package.json
└─ README.md
```

---

## 🎉 Done!

Each time you push to `main`, Netlify rebuilds and redeploys automatically — including all your recent edits.

---

Would you like me to add a **“local preview”** section (how to test your Netlify build locally using `netlify-cli`)?
