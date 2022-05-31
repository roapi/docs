# Google spreadsheet

To serve a Google spreadsheet as API, you need to gather the following config values:

* Google spreadsheet URL, usually in the form of `https://docs.google.com/spreadsheets/d/{SPREADSHEET_ID}#gid={SHEET_ID}`.
* (Optional) Google spreadsheet sheet title (bottom of the spreadsheet UI).
This is required if `SHEET_ID` is not specified in URL through `#gid`.
* Google spreadsheet service account secret key.

Here are the steps to configure the service account:

1. [Activate Google Sheets API](https://console.developers.google.com/apis/library/sheets.googleapis.com) in the Google API Console.
1. Create a service account: [https://console.developers.google.com/apis/api/sheets.googleapis.com/credentials](https://console.developers.google.com/apis/api/sheets.googleapis.com/credentials).
1. Go into service account setting, click `ADD KEY` -> `Create new key`. Then select JSON format
   and save it somewhere safe as a file. ![gsheet-add-key](../../images/gsheet-add-key.png)
1. Copy email address for your newly created service account, usually in the format of `{ACCOUNT_NAME}@{PROJECT_ID}.iam.gserviceaccount.com`. ![gsheet-service-account-email](../../images/gsheet-service-account-email.png)
1. Open the Google spreadsheet that you want to serve, then share it with the newly created service
   account using the service account email. ![gsheet-share-service-account](../../images/gsheet-share-service-account.png)


Now you can configure ROAPI to load the google spreadsheet into a table using:

```yaml
tables:
  - name: "table_name"
    uri: "https://docs.google.com/spreadsheets/d/1-lc4oij04aXzFSRMwVBLjU76s-K0-s6UPc2biOvtuuU#gid=0"
    option:
      format: "google_spreadsheet"
      application_secret_path: "path/to/service_account_key.json"
      # sheet_title is optional if `#gid` is specified in uri
      sheet_title: "sheet_name_within_google_spreadsheet"
```

ROAPI only invokes Google Sheets API during the initial data load, subsequent
query requests are served using in memory data.


## Example

Here is what it looks like to serve [this public google
spreadsheet](https://docs.google.com/spreadsheets/d/e/2PACX-1vRodiBkE77d8Y7FLe2BwwNNqy0jc3oSrtsGRrWMXXyAgdl68LxKm_LS0qfMVXa-ioPDP-5jurzKUJ0N/pubhtml)
with ROAPI.

Start server:

```
$ roapi -c local.yaml
[2022-05-31T01:07:55Z INFO  roapi::context] loading `uri(https://docs.google.com/spreadsheets/d/1-lc4oij04aXzFSRMwVBLjU76s-K0-s6UPc2biOvtuuU#gid=0)` as table `properties`
[2022-05-31T01:07:56Z INFO  roapi::context] registered `uri(https://docs.google.com/spreadsheets/d/1-lc4oij04aXzFSRMwVBLjU76s-K0-s6UPc2biOvtuuU#gid=0)` as table `properties`
[2022-05-31T01:07:56Z INFO  roapi::startup] 🚀 Listening on 127.0.0.1:5432 for Postgres traffic...
[2022-05-31T01:07:56Z INFO  roapi::startup] 🚀 Listening on 127.0.0.1:8080 for HTTP traffic...
```

Query through [Postgres wire protocol](../../postgres.html):

```
$ psql -h 127.0.0.1
psql (12.10 (Ubuntu 12.10-0ubuntu0.20.04.1), server 13)
WARNING: psql major version 12, server major version 13.
         Some psql features might not work.
Type "help" for help.

houqp=> select "Address", "Bed", "Bath", "Occupied" from properties;
     Address      | Bed | Bath | Occupied
------------------+-----+------+----------
 Bothell, WA      |   3 |    2 | f
 Lynnwood, WA     |   2 |    1 | f
 Kirkland, WA     |   4 |    2 | f
 Kent, WA         |   3 |    2 | f
 Mount Vernon, WA |   2 |    1 | f
 Seattle, WA      |   3 |    1 | f
 Seattle, WA      |   2 |    1 | f
 Shoreline, WA    |   1 |    1 | f
 Bellevue, WA     |   3 |    1 | f
 Renton, WA       |   4 |    2 | f
 Woodinville, WA  |   3 |    3 | f
 Kenmore, WA      |   4 |    3 | f
 Fremont, WA      |   5 |    3 | f
 Redmond, WA      |   2 |    2 | f
 Mill Creek, WA   |   3 |    3 | f
(15 rows)
```

Query with aggregation using [HTTP SQL frontend](../../api/query/sql.html):

```
$ curl -s -X POST localhost:8080/api/sql --data-binary @- <<EOF | jq
SELECT DISTINCT("Landlord"), COUNT("Address")
FROM properties
GROUP BY "Landlord"
EOF

[
  {
    "Landlord": "Carl",
    "COUNT(properties.Address)": 3
  },
  {
    "Landlord": "Roger",
    "COUNT(properties.Address)": 3
  },
  {
    "Landlord": "Mike",
    "COUNT(properties.Address)": 4
  },
  {
    "Landlord": "Sam",
    "COUNT(properties.Address)": 2
  },
  {
    "Landlord": "Daniel",
    "COUNT(properties.Address)": 3
  }
]
```

Query with filter using [HTTP GraphQL frontend](../../api/query/graphql.html):

```
$ curl -s -X POST localhost:8080/api/graphql --data-binary @- <<EOF | jq
query {
  properties(
    filter: {
      Bed: { gt: 3 }
      Bath: { gte: 3 }
    }
    sort: [
      { field: "Bed", order: "desc" }
    ]
  ) {
    Address
    Bed
    Bath
    Monthly_Rent
  }
}
EOF
[
  {
    "Address": "Fremont, WA",
    "Bed": 5,
    "Bath": 3,
    "Monthly_Rent": "$4,500"
  },
  {
    "Address": "Kenmore, WA",
    "Bed": 4,
    "Bath": 3,
    "Monthly_Rent": "$4,000"
  }
]
```

Note: when inferring table schema from Google spreadsheets, ROAPI automatically
replaces spaces in column names with `_`(underscore).
