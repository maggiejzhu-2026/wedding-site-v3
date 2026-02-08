# RSVP Form → Google Sheets Setup Guide

This guide will help you connect your custom RSVP form to Google Sheets so that all responses are automatically saved.

## Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new blank spreadsheet
3. Name it something like "Wedding RSVPs"
4. In the first row, add these column headers (exactly as written):
   ```
   Timestamp | Name | Email | Phone | Friday May 29th | Saturday May 30th | Open Questions | Dietary Restrictions | Wedding Requests | Anything Else
   ```

## Step 2: Create the Google Apps Script

1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete any existing code in the editor
3. Copy and paste this entire script:

```javascript
function doPost(e) {
  try {
    // Get the active spreadsheet
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

    // Parse the incoming data
    var data = JSON.parse(e.postData.contents);

    // Prepare the row data in the correct order
    var rowData = [
      data.timestamp || new Date().toISOString(),
      data.name || '',
      data.email || '',
      data.phone || '',
      data.fridayAttending || '',
      data.saturdayAttending || '',
      data.openQuestions || '',
      data.dietaryRestrictions || '',
      data.weddingRequests || '',
      data.anythingElse || ''
    ];

    // Check if this is an update (same name already exists)
    var allData = sheet.getDataRange().getValues();
    var nameColumnIndex = 1; // Column B (0-indexed, so 1 = B)
    var rowToUpdate = -1;

    // Start from row 2 (skip header)
    for (var i = 1; i < allData.length; i++) {
      if (allData[i][nameColumnIndex] === data.name) {
        rowToUpdate = i + 1; // +1 because sheet rows are 1-indexed
        break;
      }
    }

    if (rowToUpdate > 0) {
      // Update existing row
      sheet.getRange(rowToUpdate, 1, 1, rowData.length).setValues([rowData]);
    } else {
      // Append new row
      sheet.appendRow(rowData);
    }

    // Return success
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'success' }))
      .setMimeType(ContentService.MimeType.JSON);

  } catch (error) {
    // Return error
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'error', message: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService
    .createTextOutput("RSVP endpoint is working!")
    .setMimeType(ContentService.MimeType.TEXT);
}
```

4. Click the **Save** icon (💾) and name your project "Wedding RSVP Handler"

## Step 3: Deploy the Script as a Web App

1. Click the **Deploy** button → **New deployment**
2. Click the gear icon ⚙️ next to "Select type" and choose **Web app**
3. Fill in the deployment settings:
   - **Description**: "Wedding RSVP Form Handler"
   - **Execute as**: Me (your email)
   - **Who has access**: Anyone
4. Click **Deploy**
5. You may need to authorize the app:
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced** → **Go to [project name] (unsafe)**
   - Click **Allow**
6. **IMPORTANT**: Copy the **Web app URL** that appears (it looks like: `https://script.google.com/macros/s/...`)

## Step 4: Update Your Website

1. Open `index.html` in a code editor
2. Find this line (around line 242):
   ```javascript
   const GOOGLE_SCRIPT_URL = "YOUR_GOOGLE_APPS_SCRIPT_URL_HERE";
   ```
3. Replace `"YOUR_GOOGLE_APPS_SCRIPT_URL_HERE"` with your actual Web app URL in quotes:
   ```javascript
   const GOOGLE_SCRIPT_URL = "https://script.google.com/macros/s/AKfycby.../exec";
   ```
4. Save the file

## Step 5: Test the Form

1. Open your website
2. Navigate to the RSVP section
3. Fill out and submit the form
4. Check your Google Sheet - you should see a new row with the submission!

## Features

✅ **Automatic updates**: If someone submits the form twice with the same name, it updates their existing response instead of creating a duplicate

✅ **Timestamp tracking**: Every submission is automatically timestamped

✅ **No backend needed**: Everything runs through Google's infrastructure

## Troubleshooting

**Form shows "Please configure your Google Apps Script URL first"**
- You need to update the `GOOGLE_SCRIPT_URL` in index.html with your actual script URL

**Nothing appears in the spreadsheet**
- Make sure the Web app deployment has "Who has access" set to **Anyone**
- Check that your column headers match exactly (including capitalization and spaces)
- Try redeploying the script (Deploy → New deployment)

**"Authorization required" errors**
- Re-authorize the script in Google Apps Script
- Make sure you deployed it with "Execute as: Me"

## Viewing Your Responses

Just open your Google Sheet anytime to see all RSVP responses. You can:
- Sort and filter responses
- Export to Excel or PDF
- Share with others (be careful with permissions!)
- Create charts and pivot tables to analyze your guest list

## Optional: Email Notifications

If you want to receive an email every time someone RSVPs, add this to your Apps Script (after the `sheet.appendRow(rowData);` line):

```javascript
MailApp.sendEmail({
  to: "your-email@example.com",
  subject: "New RSVP: " + data.name,
  body: "New RSVP received!\n\n" +
        "Name: " + data.name + "\n" +
        "Saturday: " + data.saturdayAttending + "\n" +
        "View all responses: " + SpreadsheetApp.getActiveSpreadsheet().getUrl()
});
```

Don't forget to redeploy after making changes!
