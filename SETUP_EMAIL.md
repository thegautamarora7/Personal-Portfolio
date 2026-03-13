# Email Setup Guide for Contact Form

## Setup Instructions

To receive contact form submissions directly to your email (gautam07.work@gmail.com), follow these steps:

### Step 1: Create Google Sheet
1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "Portfolio Contact Form"
4. Add these column headers in Row 1:
   - A1: Name
   - B1: Email
   - C1: Subject
   - D1: Message
   - E1: Timestamp

### Step 2: Create Google Apps Script
1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete any existing code
3. Paste the following code:

```javascript
function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    const data = e.parameter;
    
    // Add data to sheet
    sheet.appendRow([
      data.Name,
      data.Email,
      data.Subject,
      data.Message,
      new Date()
    ]);
    
    // Send email notification to you
    const emailBody = `
      New Contact Form Submission
      
      Name: ${data.Name}
      Email: ${data.Email}
      Subject: ${data.Subject}
      
      Message:
      ${data.Message}
      
      ---
      Submitted on: ${new Date().toLocaleString()}
    `;
    
    MailApp.sendEmail({
      to: "gautam07.work@gmail.com",
      subject: `Portfolio Contact: ${data.Subject}`,
      body: emailBody
    });
    
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'success'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch(error) {
    return ContentService.createTextOutput(JSON.stringify({
      'result': 'error',
      'error': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

### Step 3: Deploy the Script
1. Click **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure:
   - Description: "Portfolio Contact Form"
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Click **Deploy**
6. Copy the **Web app URL** (it will look like: https://script.google.com/macros/s/...)

### Step 4: Update Your Website
1. Open `script.js` in your portfolio
2. Find this line:
   ```javascript
   const scriptURL = 'https://script.google.com/macros/s/AKfycbxHFrFaFcniDxrtxc340fLSk0DwxwoSE-AMVJunfzHAmNIg-0ARRd8Y7zc08rpL7jCe/exec';
   ```
3. Replace the URL with your new Web app URL from Step 3

### Step 5: Test
1. Go to your portfolio website
2. Fill out the contact form
3. Submit it
4. Check:
   - Your Google Sheet should have a new row
   - Your email (gautam07.work@gmail.com) should receive a notification

## Troubleshooting

**If emails aren't being sent:**
- Make sure you authorized the script to send emails on your behalf
- Check your Google Sheet for new entries (if entries appear but no email, it's a permission issue)
- Go to Apps Script → Run → Run function → doPost (authorize when prompted)

**If nothing happens:**
- Check browser console for errors (F12)
- Verify the Web app URL is correct in script.js
- Make sure the deployment is set to "Anyone" for access

## Features
- ✅ Form submissions saved to Google Sheet
- ✅ Email notifications sent to gautam07.work@gmail.com
- ✅ Includes all form fields (Name, Email, Subject, Message)
- ✅ Timestamp for each submission
- ✅ Professional email formatting

## Security Note
The current script URL in your code is a placeholder. You MUST replace it with your own deployed script URL for the form to work properly.
