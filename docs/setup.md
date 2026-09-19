# Setup

## Prerequisites

- An n8n instance with the LangChain nodes available
- An OpenAI API credential
- A Google account with access to Google Sheets and Gmail
- A Google Sheet containing the sample CSV or data with a compatible header row

## Import the workflow

1. Open n8n and create a new workflow.
2. Choose **Import from File**.
3. Select `workflows/ai-data-analyst-agent.json`.
4. Save the imported workflow.

## Connect credentials

Open each integration node and connect the corresponding n8n credential:

- **OpenAI Chat Model:** OpenAI API credential
- **Get row(s) in sheet in Google Sheets:** Google Sheets OAuth2 credential
- **Send a message in Gmail:** Gmail OAuth2 credential

Credentials are deliberately excluded from this repository.

## Configure the data source

1. Upload `sample-data/sales-data-sample.csv` to Google Sheets, or open it as a new spreadsheet.
2. In the Google Sheets node, replace `YOUR_GOOGLE_SHEET_ID` with the ID from your sheet URL.
3. Replace `Sheet1` if your worksheet has a different name.
4. Confirm that the operation reads rows from the selected sheet.

## Configure email delivery

In the Gmail node, replace `you@example.com` with the intended report recipient. For production use, consider collecting and validating the recipient at runtime or adding an approval step.

## Test

Run the workflow manually and try:

```text
Summarize total sales, average sales per order, and disputed orders.
```

Then try:

```text
How many unique customers are there in each city? Email me the result.
```

Review the computed values and the email recipient before activating the workflow.

## Optional self-hosted environment

`.env.example` documents useful variables for a self-hosted setup. The included public workflow uses visible placeholders so it can be safely imported across n8n environments; configure values in the n8n UI or replace them with environment expressions supported by your deployment.

## Troubleshooting

- **The agent does not read data:** verify the selected spreadsheet, worksheet, and Google credential.
- **The Gmail tool fails:** reconnect the Gmail credential and confirm the recipient.
- **The model node fails:** verify the OpenAI credential and that the configured model is available to your account.
- **The imported workflow shows missing credentials:** this is expected; select credentials created in your own n8n instance.
