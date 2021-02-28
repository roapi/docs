# Google spreadsheet

To serve a Google spreadsheet as API, you need to gather the following config values:

* Google spreadsheet URL
* Google spreadsheet sheet title (bottom of the spreadsheet UI)
* Service account secret key

Here are the steps to configure the service account:

1. Activate the Google Sheets API in the Google API Console.
1. Create service account: https://console.developers.google.com/apis/api/sheets.googleapis.com/credentials.
1. Go into service account setting and click `ADD KEY`. Then select JSON format
   and save it somewhere safe.
1. Go back to Google spreadsheet and share it with the newly created service
   account through service account email).

ROAPI config to load the google spreadsheet as data source:

```yaml
tables:
  - name: "table_name"
    uri: "https://docs.google.com/spreadsheets/d/1-lc4oij04aXzFSRMwVBLjU76s-K0-s6UPc2biOvtuuU#gid=0"
    option:
      format: "google_spreadsheet"
      application_secret_path: "path/to/service_account_key.json"
      sheet_title: "sheet_name_within_google_spreadsheet"
```
