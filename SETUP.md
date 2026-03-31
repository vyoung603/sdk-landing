# SDK Landing Page -- Setup

## Google Sheet for Leads
- Sheet: [SDK Early Access Leads](https://docs.google.com/spreadsheets/d/1WJaNWAu8PigGuA_KVI-abod--LnycycEM8SSFgJ_8Fs/edit)
- Location: Project Juno Admin folder

## Wiring the Form (2-minute setup)

The landing page form submits to a Google Apps Script web app. One-time setup:

1. Open the Google Sheet above
2. Click **Extensions > Apps Script**
3. Delete any existing code and paste the following:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Sheet1");
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow(["", data.email, new Date().toISOString(), data.source || "landing-page", "New", ""]);
  return ContentService
    .createTextOutput(JSON.stringify({ status: "ok" }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Click **Deploy > New deployment**
5. Type = **Web app**
6. Execute as = **Me (vyoung@sondermind.com)**
7. Who has access = **Anyone**
8. Click **Deploy** and copy the URL
9. Paste the URL into `index.html` where it says `APPS_SCRIPT_URL_HERE`

## Calendly
Replace `CALENDLY_URL_HERE` in `index.html` with Val's Calendly link for SDK discovery calls.

## Deploy to GitHub Pages
```bash
cd /Users/vyoung/Desktop/Clawdex/scratch/sdk-landing
git init && git add . && git commit -m "SDK landing page"
gh repo create vyoung603/sdk-landing --public --source=. --push
# Enable Pages: Settings > Pages > Deploy from branch > main
```
