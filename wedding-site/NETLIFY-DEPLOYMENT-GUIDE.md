# Netlify Deployment Guide (Easy Method!)

This guide shows you how to deploy your wedding website to Netlify using drag-and-drop - **no Git commands required!**

## Why Netlify?

✅ Drag-and-drop deployment (easiest method)
✅ Free hosting with HTTPS
✅ Custom domain support
✅ Automatic updates when you drag new files
✅ No Git knowledge needed

## Step 1: Create a Netlify Account

1. Go to [netlify.com](https://netlify.com)
2. Click **Sign up** in the top right
3. You can sign up with:
   - GitHub account (recommended if you have one)
   - Email address
4. Complete the sign-up process

## Step 2: Deploy Your Site (Drag & Drop Method)

This is the easiest way - no command line needed!

1. Log in to [Netlify](https://app.netlify.com)
2. You'll see the main dashboard
3. Look for the section that says **"Want to deploy a new site without connecting to Git? Drag and drop your site output folder here"**
4. Open Finder and navigate to your wedding site folder:
   ```
   /Users/maggiez/code/wedding-site
   ```
5. **Important**: Drag the **entire folder** (wedding-site) into the Netlify drag-and-drop area
6. Netlify will upload and deploy your site automatically (takes about 30 seconds)
7. Once complete, you'll see a randomly generated URL like: `https://random-name-12345.netlify.app`
8. Click the URL to view your live site!

## Step 3: Test Your Site

1. Visit your Netlify URL (e.g., `https://random-name-12345.netlify.app`)
2. Test the RSVP form:
   - Search for a guest name
   - Fill out and submit the form
   - Check your Google Sheet to verify the data arrived!

## Step 4: Customize Your Site URL

The random URL isn't very pretty. Let's change it:

1. On your site's Netlify dashboard, click **Site settings**
2. Click **Change site name** (under "Site information")
3. Enter a custom name like: `jordan-maggie-wedding`
4. Your new URL will be: `https://jordan-maggie-wedding.netlify.app`
5. Click **Save**

## Step 5: Update Your Site (Making Changes)

When you want to update your website:

### Method A: Manual Drag & Drop (Easiest)

1. Make your changes to `index.html` or other files on your computer
2. Save the files
3. Go to your site's Netlify dashboard
4. Click the **Deploys** tab at the top
5. Scroll down to the drag-and-drop area
6. Drag your **entire wedding-site folder** into the area again
7. Netlify will upload the new version (takes about 30 seconds)
8. Your site will automatically update!

### Method B: Using Netlify CLI (Optional - If You Like Command Line)

If you prefer the command line, you can use Netlify CLI:

```bash
# Install Netlify CLI (one-time setup)
npm install -g netlify-cli

# Navigate to your site folder
cd /Users/maggiez/code/wedding-site

# Login to Netlify
netlify login

# Deploy your site
netlify deploy --prod

# Follow the prompts to link to your existing site
```

## Optional: Use a Custom Domain

If you want to use your own domain (like `jordanandmaggie.com`):

### 1. Buy a Domain

Purchase from any domain registrar:
- Namecheap (recommended, usually cheapest)
- Google Domains
- GoDaddy

### 2. Configure Domain in Netlify

1. In your site's Netlify dashboard, go to **Domain settings**
2. Click **Add custom domain**
3. Enter your domain: `jordanandmaggie.com`
4. Click **Verify**
5. Netlify will show you DNS records to add

### 3. Update DNS Settings

Go to your domain registrar's DNS settings and add the records Netlify shows you. Typically:

```
Type: A
Name: @
Value: 75.2.60.5

Type: CNAME
Name: www
Value: [your-site-name].netlify.app
```

### 4. Wait for DNS Propagation

- DNS changes take 1-24 hours to propagate
- Usually works within 1-2 hours
- Netlify will automatically provision an SSL certificate (HTTPS)

## Troubleshooting

### "Site not loading" or shows Netlify 404 page

- Make sure you dragged the **entire folder**, not just `index.html`
- Verify that `index.html` is in the root of the folder you're uploading
- Check that the file is named exactly `index.html` (not `Index.html` or `index.HTML`)

### RSVP form not working

- Verify the `GOOGLE_SCRIPT_URL` is correctly set in `index.html`
- Check that your Google Apps Script is deployed with "Who has access: Anyone"
- Open browser Console (F12 → Console) and look for errors
- Make sure your Google Sheet has the correct column headers

### Custom domain not working

- Wait 1-24 hours for DNS propagation
- Use [DNS Checker](https://dnschecker.org) to verify your DNS records
- Make sure you added the records to your domain registrar, not Netlify
- Check that HTTPS is enabled in Netlify (it should be automatic)

### Need to revert to a previous version

1. Go to your site's Netlify dashboard
2. Click the **Deploys** tab
3. Find the previous deploy you want to restore
4. Click the three dots (•••) next to it
5. Click **Publish deploy**

## Comparing Deployment Options

| Feature | Netlify Drag & Drop | GitHub Pages |
|---------|-------------------|--------------|
| Difficulty | ⭐ Very Easy | ⭐⭐⭐ Requires Git |
| Speed to deploy | 30 seconds | 2-3 minutes |
| Updates | Drag new folder | Git commands |
| Custom domain | ✅ Easy | ✅ Easy |
| HTTPS | ✅ Automatic | ✅ Automatic |
| Version history | ✅ Yes | ✅ Yes (with Git) |
| Cost | ✅ Free | ✅ Free |

## Advantages of Netlify

1. **No Git Required**: Just drag and drop your folder
2. **Deploy Previews**: Every update creates a preview URL before going live
3. **Instant Rollbacks**: Revert to any previous version with one click
4. **Form Handling**: Built-in form processing (though you're using Google Sheets)
5. **Better Error Messages**: Clear feedback if something goes wrong

## If You Want Git Integration Later

Once you're comfortable, you can connect your GitHub repository to Netlify for automatic deployments:

1. Resolve your Git issues (or start fresh)
2. Push your code to GitHub
3. In Netlify, click **Add new site** → **Import an existing project**
4. Choose GitHub and select your repository
5. Netlify will automatically deploy whenever you push to GitHub

But you don't need to do this now - drag & drop works perfectly!

## Summary

✅ Created a Netlify account
✅ Deployed your site with drag & drop
✅ Your site is live at `https://[your-site-name].netlify.app`
✅ RSVP form connected to Google Sheets
✅ To update: Just drag the folder again!

Your wedding website is now live! 🎉

**Your Netlify URL**: Check your Netlify dashboard for your unique URL

**Need to update?** Just drag your wedding-site folder into the Deploys section again - that's it!
