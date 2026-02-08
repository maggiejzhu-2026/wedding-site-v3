# GitHub Pages Deployment Guide

This guide will walk you through hosting your wedding website on GitHub Pages for free. Your site will be live at `https://yourusername.github.io/wedding-site/` (or a custom domain if you prefer).

## Prerequisites

- A GitHub account (free) - [Sign up here](https://github.com/join)
- Git installed on your computer (check by running `git --version` in Terminal)
  - If not installed, download from [git-scm.com](https://git-scm.com/downloads)

## Step 1: Create a New GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click the **+** icon in the top right → **New repository**
3. Fill in the repository details:
   - **Repository name**: `wedding-site` (or any name you prefer)
   - **Description**: "Jordan & Maggie's Wedding Website"
   - **Visibility**: Choose **Public** or **Private**
     - Note: For GitHub Pages to work with a free account, the repo must be public
     - Or upgrade to GitHub Pro for private repos with Pages
   - **Do NOT** initialize with README, .gitignore, or license
4. Click **Create repository**

## Step 2: Connect Your Local Files to GitHub

Open Terminal and navigate to your wedding site folder, then run these commands:

```bash
# Navigate to your wedding site folder
cd /Users/maggiez/code/wedding-site

# Initialize git repository (if not already done)
git init

# Add all files to git
git add .

# Create your first commit
git commit -m "Initial commit: Wedding website with custom RSVP form"

# Add your GitHub repository as the remote origin
# Replace YOUR-USERNAME with your actual GitHub username
git remote add origin https://github.com/YOUR-USERNAME/wedding-site.git

# Push your code to GitHub
git branch -M main
git push -u origin main
```

### Example:
If your GitHub username is `maggiez`, the command would be:
```bash
git remote add origin https://github.com/maggiez/wedding-site.git
```

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/YOUR-USERNAME/wedding-site`
2. Click the **Settings** tab (top right of the repository page)
3. In the left sidebar, click **Pages** (under "Code and automation")
4. Under **Source**, select:
   - Branch: **main**
   - Folder: **/ (root)**
5. Click **Save**
6. Wait 1-2 minutes for GitHub to build your site
7. Your site will be live at: `https://YOUR-USERNAME.github.io/wedding-site/`

## Step 4: Test Your Website

1. Visit `https://YOUR-USERNAME.github.io/wedding-site/`
2. Test the RSVP form:
   - Click "check my invite" and search for a guest name
   - Click "rsvp now" and fill out the form
   - Submit and check your Google Sheet to verify it's working!

## Step 5: Update Your Website (Making Changes)

Whenever you want to update your website:

```bash
# Make your changes to index.html or other files

# Stage all changes
git add .

# Commit the changes with a descriptive message
git commit -m "Update RSVP form styling"

# Push to GitHub
git push

# Wait 30-60 seconds for GitHub Pages to rebuild
# Then refresh your website to see changes
```

## Optional: Use a Custom Domain

If you want to use your own domain (like `jordanandmaggie.com`):

### 1. Buy a Domain
Purchase a domain from:
- Namecheap
- Google Domains
- GoDaddy
- Any domain registrar

### 2. Configure DNS Settings

In your domain registrar's DNS settings, add these records:

**For apex domain (jordanandmaggie.com):**
```
Type: A
Name: @
Value: 185.199.108.153

Type: A
Name: @
Value: 185.199.109.153

Type: A
Name: @
Value: 185.199.110.153

Type: A
Name: @
Value: 185.199.111.153
```

**For www subdomain (www.jordanandmaggie.com):**
```
Type: CNAME
Name: www
Value: YOUR-USERNAME.github.io
```

### 3. Configure GitHub Pages for Custom Domain

1. In your GitHub repository, go to **Settings** → **Pages**
2. Under **Custom domain**, enter your domain: `jordanandmaggie.com`
3. Click **Save**
4. Check **Enforce HTTPS** (wait a few minutes for SSL certificate to provision)
5. Create a file named `CNAME` in your repository root with just your domain:
   ```bash
   echo "jordanandmaggie.com" > CNAME
   git add CNAME
   git commit -m "Add custom domain"
   git push
   ```

### 4. Wait for DNS Propagation
- DNS changes can take 24-48 hours to propagate worldwide
- Usually works within 1-2 hours

## Troubleshooting

### "Site not found" or 404 error
- Wait a few minutes after enabling GitHub Pages
- Check that your repository is public (or you have GitHub Pro)
- Verify that `index.html` is in the root of your repository
- Make sure GitHub Pages is set to deploy from `main` branch and `/ (root)` folder

### RSVP form not working
- Check that `GOOGLE_SCRIPT_URL` is correctly set in `index.html`
- Verify your Google Apps Script is deployed with "Who has access: Anyone"
- Check your browser's Console for errors (F12 → Console tab)

### Changes not appearing
- Hard refresh your browser: Cmd+Shift+R (Mac) or Ctrl+Shift+R (Windows)
- Wait 1-2 minutes for GitHub Pages to rebuild
- Clear your browser cache

### Custom domain not working
- Verify DNS records are correct (use [DNS Checker](https://dnschecker.org))
- Wait 24-48 hours for DNS propagation
- Make sure HTTPS is enforced in GitHub Pages settings
- Check that `CNAME` file exists in your repository

## Security Notes

1. **Never commit sensitive data** to GitHub:
   - No passwords
   - No API keys (your Google Apps Script URL is fine - it's meant to be public)
   - No personal information

2. **Guest list privacy**:
   - Your guest list is embedded in the JavaScript code
   - Anyone can view it by looking at the page source
   - If you want it truly private, you'd need to move it to a backend/database
   - For most weddings, this level of privacy is fine

3. **Google Sheet access**:
   - Make sure your Google Sheet is NOT public
   - Only you (the owner) should be able to access the spreadsheet
   - The Apps Script acts as a secure intermediary

## Advanced: Protecting Your Guest List

If you want to hide your guest list from the public:

1. Create a separate Google Sheet with just the guest list
2. Create another Google Apps Script to query it
3. Have the website fetch guest data from that script
4. This requires more complex setup - let me know if you want help with this!

## Need Help?

Common commands:
```bash
# Check git status
git status

# View commit history
git log --oneline

# Undo uncommitted changes
git checkout -- index.html

# Pull latest changes (if working with others)
git pull

# View your remote URL
git remote -v
```

## Summary

You're all set! Here's what you accomplished:

✅ Created a GitHub repository for your wedding site
✅ Pushed your code to GitHub
✅ Enabled GitHub Pages
✅ Your site is now live at `https://YOUR-USERNAME.github.io/wedding-site/`
✅ RSVP form is connected to Google Sheets
✅ You can update it anytime with `git add . && git commit -m "Update" && git push`

Your wedding website is now live and ready to share with your guests! 🎉
