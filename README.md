# 03 — Receipt to Spreadsheet Bookkeeping

The business owner forwards a photo of a receipt to a dedicated email/label → AI reads the data and adds it to the expense sheet → if the amount is unusually large, an alert is sent too. No phone call needed.

## Demo Video

Contact me on linkedin: http://linkedin.com/in/solutionbylaiba for demo video request.

## Screenshots

**Receipt Forwarded by Email**

<img width="1920" height="799" alt="invoice attach" src="https://github.com/user-attachments/assets/ec3144d7-2b76-4110-abe6-c4d8287a6d06" />

**n8n Workflow Canvas**

<img width="1920" height="796" alt="workflow" src="https://github.com/user-attachments/assets/d4046152-a4a8-4a21-9573-77e300fab2fc" />


**Expenses — Google Sheet**

<img width="1920" height="766" alt="excel log" src="https://github.com/user-attachments/assets/67847d0f-bfdd-4f5e-9683-dc85ca9851c6" />


**High-Value Alert Email**

<img width="1909" height="789" alt="high amount alert email" src="https://github.com/user-attachments/assets/262ffd2c-2206-4d26-bc92-7f5aab60db0c" />


## What You'll Need

1. **Gmail account** — create a label named "Receipts" in it (Gmail settings → Labels → Create new).
2. **Google Sheet** named "Expenses", with headers: `vendor, date, amount, currency, category, sourceEmail, addedAt`.
3. **OpenAI API key** (this uses gpt-4o-mini vision to read receipts).

## Import Steps

1. Open n8n → **Import from File** → select `workflow.json`.
2. Open the **Watch Receipts Label** node → attach a Gmail OAuth2 credential → replace `YOUR_RECEIPTS_LABEL_ID` with your "Receipts" label's ID (you can select it from the dropdown inside the node and the ID will fill in automatically).
3. **Extract Data (OpenAI Vision)** node → attach an HTTP Header Auth credential (`Authorization: Bearer YOUR_OPENAI_KEY`) — you can reuse the same credential created for automation 01, if you built that one first.
4. **Append Expense Row** node → attach a Google Sheets credential and replace `YOUR_GOOGLE_SHEET_ID`.
5. **Alert Owner** node → attach a Gmail credential and replace `YOUR_EMAIL@example.com` with your own address. The alert threshold (currently 20,000) can be changed in the **High Value?** node.

## What the Business Owner Needs to Do (client-facing instruction)

"Take a photo of every receipt and forward/send it to `receipts@yourbusiness.com` (or whichever email you've set up) — that's all you need to do, everything else happens automatically."

## How to Test

- Email yourself a receipt photo to that label.
- Within about a minute, check that the data was extracted and a row appeared in the sheet.
- Send a receipt with a deliberately large amount to test the alert email.

## Note

Attachment images need to be clear and readable — a very blurry photo can cause the AI to misread the amount. Tell the client to take receipt photos in good, direct lighting.

## For a New Client

Just update the label ID, sheet ID, and alert email — about 10 minutes of work.
