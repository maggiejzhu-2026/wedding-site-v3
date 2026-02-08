# Netlify + GitHub Connected Setup

This guide will help you connect your GitHub repository to Netlify for automatic deployments.

## Benefits of This Setup

✅ **Automatic Deployments**: Push to GitHub → Netlify deploys automatically
✅ **Version Control**: Full Git history of all changes
✅ **Collaboration**: Easy for others to contribute
✅ **Deploy Previews**: Test changes before going live
✅ **Rollbacks**: Revert to any previous version instantly

## Part 1: Fix GitHub Push Issues

Let's resolve the Git error you had and get your code into GitHub.

### Step 1: Pull with Unrelated Histories

```bash
cd /Users/maggiez/code/wedding-site
git pull origin main --allow-unrelated-histories --no-rebase
```

If this shows a merge conflict or asks you to resolve differences:

```bash
# Accept your local version for any conflicts
git checkout --ours .
git add .
git commit -m "Merge remote changes"
```

### Step 2: Push Your Code

```bash
git push -u origin main
```

If you still get an error, we can force push (this will overwrite what's on GitHub):

```bash
git push -u origin main --force
```

⚠️ **Note**: `--force` will replace everything on GitHub with your local files. Only use this if you don't have important files on GitHub that aren't on your computer.

### Step 3: Verify on GitHub

1. Go to: https://github.com/maggiejzhu-2026/wedding-site-v2
2. You should see your files: `index.html`, `RSVP-SETUP-INSTRUCTIONS.md`, etc.
3. ✅ If you see your files, you're ready for Part 2!

## Part 2: Connect GitHub to Netlify

Now let's connect your GitHub repository to Netlify for automatic deployments.

### Step 1: Create Netlify Account (if you haven't)

1. Go to [netlify.com](https://netlify.com)
2. Click **Sign up**
3. Choose **GitHub** as your sign-up method (this makes connecting easier)
4. Authorize Netlify to access your GitHub account

### Step 2: Import Your GitHub Repository

1. Log in to [Netlify](https://app.netlify.com)
2. Click **Add new site** button (top right)
3. Choose **Import an existing project**
4. Click **Deploy with GitHub**
5. If prompted, authorize Netlify to access your repositories
6. Find and click on **wedding-site-v2** from the list

### Step 3: Configure Build Settings

Netlify will show you deployment settings:

```
Branch to deploy: main
Base directory: (leave blank)
Build command: (leave blank - we don't need a build step)
Publish directory: (leave blank or put a single period: .)
```

**Important**: Since your site is a simple HTML file with no build process:
- Leave **Build command** blank
- Leave **Publish directory** blank (or enter just a period: `.`)

### Step 4: Deploy!

1. Click **Deploy [your-site-name]**
2. Netlify will:
   - Clone your GitHub repo
   - Deploy your site
   - Give you a live URL
3. Wait 30-60 seconds for the first deploy
4. You'll see: **Site is live** ✅

### Step 5: Get Your Live URL

Your site will be live at: `https://[random-name].netlify.app`

Let's customize this:
1. Go to **Site configuration** → **Site details**
2. Click **Change site name**
3. Enter something like: `jordan-maggie-wedding`
4. Your new URL: `https://jordan-maggie-wedding.netlify.app`

## Part 3: Making Updates (Automatic Deployments)

Now whenever you make changes, just push to GitHub and Netlify deploys automatically!

### Update Workflow

```bash
# 1. Make changes to index.html or other files
# 2. Save your changes

# 3. Commit your changes
cd /Users/maggiez/code/wedding-site
git add .
git commit -m "Update RSVP form styling"

# 4. Push to GitHub
git push

# 5. That's it! Netlify automatically deploys your changes
```

### Monitor Your Deployment

1. Go to your Netlify dashboard
2. Click on the **Deploys** tab
3. You'll see:
   - ✅ **Published** - Live on your site
   - 🔄 **Building** - Deploying now
   - ❌ **Failed** - Something went wrong

### Deployment Time

- Typical deployment: 30-60 seconds
- You'll get an email when deployment completes
- Check your live site to see the changes!

## Part 4: Advanced Features

### Deploy Previews (Test Before Going Live)

If you want to test changes before they go live:

**Option A: Using Branches**
```bash
# Create a new branch for testing
git checkout -b test-changes

# Make your changes and commit
git add .
git commit -m "Testing new feature"

# Push the branch
git push origin test-changes
```

Netlify will create a **preview URL** for this branch. You can test it without affecting your live site. When ready, merge to main:

```bash
git checkout main
git merge test-changes
git push
```

**Option B: Using Pull Requests**
1. Create a branch and push it (as above)
2. Go to GitHub and create a Pull Request
3. Netlify will comment with a preview URL
4. Test the preview
5. Merge the PR when ready

### Instant Rollbacks

If you deploy something broken:

1. Go to Netlify → **Deploys** tab
2. Find the last working version
3. Click **•••** (three dots) next to it
4. Click **Publish deploy**
5. Your site instantly reverts to that version!

### Build Notifications

Get notified when deploys finish:

1. Netlify dashboard → **Site configuration** → **Build & deploy**
2. Scroll to **Deploy notifications**
3. Add your email, Slack, or webhook

### Environment Variables (If Needed Later)

If you need to add secrets (API keys, etc.):

1. Go to **Site configuration** → **Environment variables**
2. Click **Add a variable**
3. Enter key/value pairs
4. Redeploy to use them

## Common Issues & Solutions

### "Repository not found" on Netlify

**Solution**:
1. Go to Netlify → **User settings** → **Applications**
2. Find **GitHub**
3. Click **Configure**
4. Grant access to your repository

### Changes not deploying

**Solution**:
```bash
# Make sure you pushed to the right branch
git branch  # Should show: * main

# Check your last push succeeded
git status  # Should show: "Your branch is up to date with 'origin/main'"

# Force trigger a deploy in Netlify
# Go to Deploys → Click "Trigger deploy" → "Deploy site"
```

### "Build failed" error in Netlify

**Solution**: Since you don't have a build process, make sure:
1. Build command is blank
2. Publish directory is blank or `.`
3. Your `index.html` is in the root of the repository

### RSVP form not working after deploy

**Solution**:
1. Check that `GOOGLE_SCRIPT_URL` is correct in `index.html`
2. Verify Google Apps Script is deployed with "Who has access: Anyone"
3. Open browser Console (F12) and check for CORS errors

### Want to disconnect GitHub?

If you want to switch back to manual drag-and-drop:

1. Netlify dashboard → **Site configuration** → **Build & deploy**
2. Scroll to **Build settings**
3. Click **Link to a different repository** or **Stop builds**

You can still deploy manually by dragging your folder to the Deploys section.

## Your Complete Workflow

```bash
# Daily workflow for updating your wedding site:

# 1. Make changes
# Edit index.html or other files

# 2. Test locally (optional)
# Open index.html in your browser

# 3. Commit and push
git add .
git commit -m "Update guest list"
git push

# 4. Wait 30 seconds
# Netlify automatically deploys

# 5. Verify
# Visit your live site: https://jordan-maggie-wedding.netlify.app
```

## Summary

✅ Your GitHub repository is now connected to Netlify
✅ Every `git push` automatically deploys your site
✅ You have full version control with Git
✅ You can instantly rollback to any previous version
✅ You get deploy previews for testing

## Next Steps

1. ✅ Finish Part 1 (get code into GitHub)
2. ✅ Complete Part 2 (connect to Netlify)
3. ✅ Test the workflow (make a small change and push)
4. 🎨 Optionally add a custom domain
5. 🎉 Share your wedding website with guests!

**Your Live Site**: Check your Netlify dashboard for your URL!
