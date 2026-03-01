# Score Love — Setup Guide

Complete setup instructions for getting the landing page live. Follow these steps in order.

---

## Step 1: Local Project Setup (Mac + Dropbox)

### 1a. Create the Dropbox folder
```bash
# Folder already exists at:
# ~/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website/
# No need to create it — just copy the project files there.
```

### 1b. Copy project files into it
Copy `index.html`, `netlify.toml`, `README.md`, and this file (`SETUP-GUIDE.md`) into `~/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website/`.

### 1c. Initialize Git
```bash
cd "$HOME/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website"
git init
git add .
git commit -m "Initial commit: Score Love landing page"
```

---

## Step 2: GitHub Setup (Free Account)

### 2a. Create a GitHub account
Go to https://github.com/signup and create a free account.

### 2b. Create a new repository
1. Click the **+** icon → **New repository**
2. Name: `score-love`
3. Set to **Private** (recommended for pre-launch)
4. Do NOT initialize with README (we already have one)
5. Click **Create repository**

### 2c. Push your local code to GitHub
GitHub will show you the commands. Run these in your terminal:
```bash
cd "$HOME/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website"
git remote add origin https://github.com/YOUR_USERNAME/score-love.git
git branch -M main
git push -u origin main
```

You'll be prompted for your GitHub credentials. If using 2FA, you'll need a personal access token instead of your password:
- Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
- Generate new token with `repo` scope
- Use this token as your password when pushing

---

## Step 3: Mailchimp Setup (Free Account)

### 3a. Create account
Go to https://mailchimp.com and sign up for the free plan (up to 500 contacts).

### 3b. Create an Audience
1. Go to **Audience** → **All contacts**
2. If prompted, create your first audience
3. Name it something like "Score Love Early Access"

### 3c. Get your form integration values
1. Go to **Audience** → **Signup forms** → **Embedded forms**
2. Look at the generated form HTML. Find the `<form action="..."` URL. It will look like:
   ```
   https://scorelove.us21.list-manage.com/subscribe/post?u=abc123def456&id=xyz789
   ```
3. Extract these three values:
   - **MAILCHIMP_URL**: `https://scorelove.us21.list-manage.com/subscribe/post-json` (change `post` to `post-json`)
   - **MAILCHIMP_U**: The `u` parameter value (e.g., `abc123def456`)
   - **MAILCHIMP_ID**: The `id` parameter value (e.g., `xyz789`)

### 3d. Update index.html
Open `index.html` and find the Mailchimp configuration section near the bottom:
```javascript
const MAILCHIMP_URL = 'https://XXXXX.usXX.list-manage.com/subscribe/post-json';
const MAILCHIMP_U   = 'YOUR_U_VALUE_HERE';
const MAILCHIMP_ID  = 'YOUR_ID_VALUE_HERE';
```
Replace with your actual values.

### 3e. Set up a Welcome Email (Optional but Recommended)
1. Go to **Automations** → **Create** → **Email**
2. Choose **Welcome new subscribers**
3. Design your welcome email with the Score Love branding
4. Set it to send immediately when someone subscribes
5. Activate the automation

### 3f. Commit and push the Mailchimp update
```bash
cd "$HOME/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website"
git add .
git commit -m "Add Mailchimp integration credentials"
git push
```

---

## Step 4: Netlify Setup (Free Account)

### 4a. Create account
Go to https://app.netlify.com/signup and sign up with your GitHub account (easiest).

### 4b. Deploy from GitHub
1. Click **Add new site** → **Import an existing project**
2. Choose **GitHub**
3. Authorize Netlify to access your GitHub
4. Select the `score-love` repository
5. Build settings should auto-detect (publish directory: `.`)
6. Click **Deploy site**

Your site is now live at a random Netlify URL like `https://amazing-tesla-abc123.netlify.app`

### 4c. Set up custom domain
1. In Netlify: Go to **Domain management** → **Add a custom domain**
2. Enter `scorelove.com` (or your domain)
3. Netlify will tell you to update your DNS

---

## Step 5: Point GoDaddy Domain to Netlify

### 5a. Update DNS records
1. Log into GoDaddy → **My Products** → **DNS** for your domain
2. **Delete** any existing A records or CNAME records for `@` and `www`
3. Add these records:

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 75.2.60.5 | 600 |
| CNAME | www | YOUR-SITE.netlify.app | 600 |

Note: The A record IP (`75.2.60.5`) is Netlify's load balancer. Confirm the current IP in Netlify's domain settings.

### 5b. Enable HTTPS
1. Back in Netlify: **Domain management** → **HTTPS**
2. Click **Verify DNS configuration**
3. Once verified, click **Provision certificate**
4. SSL will be active within a few minutes

### 5c. Wait for propagation
DNS changes can take up to 48 hours, but usually work within 15-30 minutes. Test at https://scorelove.com.

---

## Step 6: Test Everything

### Checklist
- [ ] Site loads at https://scorelove.com
- [ ] Site loads at https://www.scorelove.com (redirects to non-www)
- [ ] HTTP redirects to HTTPS
- [ ] Logo displays correctly
- [ ] Animations play on load
- [ ] Email form validates bad emails (shows red outline + error)
- [ ] Email form submits to Mailchimp (check your Mailchimp audience)
- [ ] Success message appears after signup
- [ ] Welcome email arrives (if configured)
- [ ] Mobile: form stacks vertically on phone
- [ ] Mobile: no horizontal scrolling
- [ ] Mobile: text is readable without zooming

---

## Ongoing Maintenance

### Making changes
1. Edit files in `~/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website/`
2. Test locally by opening `index.html` in your browser
3. Push to deploy:
   ```bash
   cd "$HOME/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website"
   git add .
   git commit -m "Your change description"
   git push
   ```
4. Netlify deploys automatically in ~30 seconds

### Monitoring signups
- Log into Mailchimp → **Audience** → **All contacts**
- You can export your subscriber list at any time
- Set up email notifications in Mailchimp to get alerts for new signups

### Costs
- **Netlify**: Free (100GB bandwidth/month, plenty for a landing page)
- **GitHub**: Free (private repos included)
- **Mailchimp**: Free (up to 500 contacts, 1,000 emails/month)
- **GoDaddy**: Your existing domain renewal cost only
