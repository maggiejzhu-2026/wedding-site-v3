# Wedding RSVP Form Integration Guide

Your wedding website is now ready to integrate with Google Forms or Typeform!

## Current Features ✓

1. **Guest Lookup** - Guests can search their name to check if they have a +1
2. **Form Integration Ready** - The "RSVP Now" tab will display your embedded form

## Option 1: Google Forms (Recommended - Free)

### Step 1: Create Your Google Form

1. Go to [forms.google.com](https://forms.google.com)
2. Click "Blank" to create a new form
3. Add these questions:

   - **Name** (Short answer, Required)
   - **Email** (Short answer, Required)
   - **Will you be attending?** (Multiple choice)
     - Options: "Yes, I'll be there!", "Still deciding", "Unable to attend"
   - **Number of guests** (Multiple choice)
     - Options: 1, 2, 3, 4
   - **Dietary requirements** (Short answer)
   - **Song request** (Short answer)

4. Customize the theme:
   - Click the palette icon (top right)
   - Choose colors that match your wedding (e.g., #e63946 for accent)
   - Upload your stick figure couple image as header if desired

### Step 2: Get the Embed Code

1. Click "Send" button (top right)
2. Click the `< >` (Embed HTML) icon
3. Copy the entire iframe code that looks like:
   ```html
   <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSe.../viewform?embedded=true" width="640" height="1234" frameborder="0">Loading…</iframe>
   ```

### Step 3: Add to Your Website

1. Open `index.html` in a text editor
2. Find this line (around line 112):
   ```javascript
   const FORM_EMBED_URL = "https://docs.google.com/forms/d/e/YOUR_FORM_ID/viewform?embedded=true";
   ```
3. Replace `YOUR_FORM_ID` with the actual URL from your Google Form embed code
4. Save the file and refresh your browser!

## Option 2: Typeform (Beautiful, Limited Free Plan)

### Step 1: Create Your Typeform

1. Go to [typeform.com](https://typeform.com) and sign up
2. Create a new form with the same questions as above
3. Typeform is more interactive and beautiful, but the free plan limits you to 100 responses/month

### Step 2: Get the Embed URL

1. Click "Share" in your Typeform
2. Go to "Embed" section
3. Copy the iframe URL (it looks like: `https://form.typeform.com/to/ABC123`)

### Step 3: Add to Your Website

1. Open `index.html`
2. Update the `FORM_EMBED_URL` with your Typeform URL:
   ```javascript
   const FORM_EMBED_URL = "https://form.typeform.com/to/YOUR_FORM_ID";
   ```

## Updating the Guest List

To update who has a +1, edit the `GUEST_LIST` array in `index.html` (lines 93-100):

```javascript
const GUEST_LIST = [
  { name: "Alex Smith", plusOne: true, plusOneName: "Sam Smith" },
  { name: "Jordan Lee", plusOne: false },
  // Add more guests...
];
```

## Tips

- **Google Forms**:
  - Free, unlimited responses
  - Responses go to a Google Sheet automatically
  - Easy to customize with your colors
  - Simple and reliable

- **Typeform**:
  - More beautiful and interactive
  - Free plan: 100 responses/month
  - Better mobile experience
  - More advanced logic and branching

## Testing

1. After adding your form URL, open `index.html` in your browser
2. Navigate to the RSVP section
3. Click "RSVP Now" tab
4. You should see your embedded form!

## Need Help?

If you run into issues:
1. Make sure the form is set to "Anyone with the link can respond"
2. Check that you copied the full URL
3. Try opening the form URL directly in a browser first
4. The iframe might take a few seconds to load

---

Enjoy your wedding! 🎉
