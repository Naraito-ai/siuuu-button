# The SIUUU Button - Landing Page ⚽🔥

This is a premium, high-converting, mobile-first single-product landing page for a physical "SIUUU Button" meme toy. It includes a virtual sound-testing button with confetti particle bursts and a Cash on Delivery (COD) order checkout form.

---

## 🚀 Host It 100% Free on GitHub Pages

Since this is a public repository, you can get it live on the internet for free in 30 seconds:
1. Go to your repository page: **[https://github.com/Naraito-ai/siuuu-button](https://github.com/Naraito-ai/siuuu-button)**
2. Click on the **Settings** tab.
3. On the left sidebar, click **Pages**.
4. Under **Build and deployment -> Branch**, select **main** (and `/root`), then click **Save**.
5. Your website will be live in ~1 minute at:
   `https://Naraito-ai.github.io/siuuu-button/`

---

## 📊 Connect the Checkout Form to Google Sheets (Free Webhook)

To collect orders directly into a Google Sheet for free:

1. Open **[Google Sheets](https://sheets.google.com)** and create a new blank spreadsheet.
2. Name the sheets headers in row 1:
   * **Col A**: `timestamp`
   * **Col B**: `name`
   * **Col C**: `phone`
   * **Col D**: `address`
   * **Col E**: `pincode`
   * **Col F**: `quantity`
3. Click **Extensions -> Apps Script**.
4. Delete all existing code and paste the following Google Apps Script:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  try {
    var data = JSON.parse(e.postData.contents);
    sheet.appendRow([
      data.timestamp,
      data.name,
      data.phone,
      data.address,
      data.pincode,
      data.quantity
    ]);
    return ContentService.createTextOutput("Success").setMimeType(ContentService.MimeType.TEXT);
  } catch(error) {
    return ContentService.createTextOutput("Error: " + error.toString()).setMimeType(ContentService.MimeType.TEXT);
  }
}
```

5. Click the **Deploy** button (top right) -> **New deployment**.
6. Select type: **Web app**.
7. Configure:
   * **Description**: `n8n/leads webhook`
   * **Execute as**: `Me` (your email)
   * **Who has access**: `Anyone` (this is critical so the website can send data to it).
8. Click **Deploy** and authorize permissions.
9. Copy the **Web App URL** provided (it will end in `/exec`).
10. Open [index.html](file:///D:/siuuu-button/index.html) in your code editor, find line 431, and replace the placeholder webhook URL:
    ```javascript
    const webhookUrl = "YOUR_GOOGLE_APPS_SCRIPT_URL_HERE";
    ```
11. Commit and push the updated `index.html` to GitHub!
