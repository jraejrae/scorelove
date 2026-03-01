# Score Love — Landing Page & Email Capture

## Project Overview

**Score Love** is a golf-themed dating app. This is the pre-launch landing page with email capture via Mailchimp. The site is a single-page static HTML file hosted on Netlify with a custom domain from GoDaddy.

---

## Architecture

```
score-love/
├── index.html        ← The entire website (single file, self-contained)
├── netlify.toml      ← Netlify hosting configuration (headers, redirects)
├── README.md         ← This file
└── SETUP-GUIDE.md    ← Step-by-step setup instructions
```

**Tech Stack:**
- Pure HTML/CSS/JS (no build tools, no frameworks)
- Fonts: Google Fonts (Oswald + Source Serif 4)
- Logo: Embedded as base64 in the HTML (no external image files)
- Email capture: Mailchimp JSONP integration (no server needed)
- Hosting: Netlify (free tier)
- Domain: GoDaddy (DNS pointed to Netlify)
- Version control: GitHub

---

## Key Design Decisions

1. **Single HTML file** — Everything is inline (CSS, JS, base64 logo). This means zero external dependencies, instant loading, and easy deployment. No build step needed.

2. **Mailchimp JSONP** — Instead of a server-side form handler, we use Mailchimp's JSONP endpoint directly from the browser. This keeps the site 100% static and free to host.

3. **Mobile-first responsive** — Four breakpoints: 768px (tablets), 540px (phones), 360px (small phones). iOS zoom prevention included (16px input font size).

4. **Animations** — CSS-only entrance animations (no JS libraries). Staggered fadeUp on load.

---

## How to Make Changes

### Editing Content
Open `index.html` in any text editor. All content is in the `<body>` section:
- **Tagline**: Search for `Find Your Match Play`
- **Subhead**: Search for `Something big is teeing up`
- **Button text**: Search for `TEE ME UP`
- **Success message**: Search for `YOU'RE ON THE TEE SHEET`
- **Footer**: Search for `© 2026 Score Love`
- **Stats section**: Search for `LESS`, `MORE`, `WAY MORE`

### Editing Styles
All CSS is in the `<style>` tag in the `<head>`. Key variables are at the top:
```css
:root {
    --navy: #2B3A67;
    --cream: #f2f2e6;
    --gold: #D4A843;
    --warm-white: #FAF8F2;
    --dark: #1A2340;
    --rust: #C1553B;
}
```

### Replacing the Logo
The logo is a base64-encoded image. To replace it:
1. Convert your new logo to base64: https://base64.guru/converter/encode/image
2. Replace the `src="data:image/png;base64,..."` in the `<img>` tag
3. Update the `width` and `height` attributes

### Changing Mailchimp Settings
In the `<script>` section at the bottom, update these three values:
```javascript
const MAILCHIMP_URL = 'https://XXXXX.usXX.list-manage.com/subscribe/post-json';
const MAILCHIMP_U   = 'YOUR_U_VALUE_HERE';
const MAILCHIMP_ID  = 'YOUR_ID_VALUE_HERE';
```

---

## Deployment Workflow

1. Make changes to `index.html` locally
2. Commit and push to GitHub:
   ```bash
   cd ~/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website
   git add .
   git commit -m "describe your change"
   git push
   ```
3. Netlify auto-deploys within ~30 seconds
4. Verify at your live URL

---

## Using Claude / Claude Code for Changes

When working with Claude or Claude Code on this project, provide this context:

> "This is a single-file static landing page (index.html) for Score Love, a golf dating app. It uses inline CSS/JS, Mailchimp JSONP for email capture, and is hosted on Netlify. The local project is at ~/Dropbox (Personal)/Family Room/Julia Rae/FORE LOVE/Website/. Here's what I need to change: [your request]"

**Common requests for Claude:**
- "Update the tagline to [new text]"
- "Change the color scheme to [new colors]"
- "Add a countdown timer above the email form"
- "Add an Instagram link to the footer"
- "Replace the logo with this new image"
- "Add Google Analytics tracking"

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Email form doesn't submit | Check Mailchimp config values in the script |
| Site not updating after push | Check Netlify deploy logs at app.netlify.com |
| Fonts not loading | Check internet connection; fonts are from Google CDN |
| Logo looks blurry | Replace with a higher-resolution base64 image |
| Mobile layout broken | Check CSS media queries at bottom of `<style>` |

---

## Important URLs

- **Live site**: https://scorelove.com (after DNS setup)
- **Netlify dashboard**: https://app.netlify.com
- **GitHub repo**: https://github.com/YOUR_USERNAME/score-love
- **Mailchimp dashboard**: https://us1.admin.mailchimp.com
- **GoDaddy DNS**: https://dcc.godaddy.com/dns
