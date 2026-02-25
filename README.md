# BrideSide — Setup Guide

Your landing page is a single `index.html` file. No frameworks, no build tools, no installs.
Follow the steps below to get it live on GitHub Pages and collecting emails into Google Sheets.

---

## Step 1 — Set up your Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com) and create a new spreadsheet
2. Name it **BrideSide Waitlist**
3. In **Row 1**, add these exact column headers (one per cell):

   | A | B | C | D |
   |---|---|---|---|
   | email | date | time | source |

4. Keep this tab open — you'll need the spreadsheet URL in the next step

---

## Step 2 — Connect SheetDB (free API for your sheet)

SheetDB turns your Google Sheet into an API so the website can write to it without a server.

1. Go to [sheetdb.io](https://sheetdb.io) and sign up for a free account
2. Click **Create new API**
3. Paste your Google Sheet URL and follow the prompts to connect it
4. Once created, copy your **API URL** — it looks like:
   ```
   https://sheetdb.io/api/v1/XXXXXXXXXX
   ```
5. Open `index.html` in any text editor (TextEdit, Notepad, VS Code)
6. Find this line near the bottom of the file (around line 780):
   ```js
   const SHEETDB_URL = 'YOUR_SHEETDB_API_URL_HERE';
   ```
7. Replace `YOUR_SHEETDB_API_URL_HERE` with your actual URL:
   ```js
   const SHEETDB_URL = 'https://sheetdb.io/api/v1/abc123xyz';
   ```
8. Save the file

> ✅ **Test it:** Open `index.html` in your browser, submit a test email, and check your Google Sheet — the row should appear within seconds.

---

## Step 3 — Publish to GitHub Pages

### 3a. Create a GitHub account
If you don't have one, sign up free at [github.com](https://github.com)

### 3b. Create a new repository
1. Click the **+** icon → **New repository**
2. Name it: `brideside` (or `brideside-landing`)
3. Set it to **Public**
4. Leave everything else as default
5. Click **Create repository**

### 3c. Upload your file
1. On your new repo page, click **uploading an existing file**
2. Drag and drop your `index.html` file into the upload area
3. Scroll down and click **Commit changes**

### 3d. Enable GitHub Pages
1. Go to your repo → **Settings** tab
2. In the left sidebar, click **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Set branch to **main**, folder to **/ (root)**
5. Click **Save**

### 3e. Your site is live! 🎉
After ~60 seconds, GitHub will give you a URL like:
```
https://yourusername.github.io/brideside
```

---

## Step 4 — Connect a Custom Domain (optional)

If you have a domain like `brideside.co`:

1. Go to your domain registrar (GoDaddy, Namecheap, Google Domains, etc.)
2. Add these **DNS records**:

   | Type | Name | Value |
   |------|------|-------|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | yourusername.github.io |

3. In GitHub: **Settings → Pages → Custom domain** → enter your domain → Save
4. Check **Enforce HTTPS** once it propagates (can take up to 24 hrs)

---

## Updating the site

Whenever you want to make changes:
1. Edit `index.html` on your computer
2. Go to your GitHub repo
3. Click on `index.html` → click the **pencil icon** to edit
4. Paste your updated code → **Commit changes**
5. Live within ~30 seconds

Or if you're using a code editor like VS Code, you can use GitHub Desktop for a smoother workflow.

---

## File structure

```
brideside/
└── index.html      ← Your entire website (HTML + CSS + JS in one file)
```

That's it. No dependencies, no node_modules, no build step.

---

## Need help?

- SheetDB docs: [sheetdb.io/documentation](https://sheetdb.io/documentation)
- GitHub Pages docs: [docs.github.com/pages](https://docs.github.com/en/pages)
- DNS propagation checker: [dnschecker.org](https://dnschecker.org)
