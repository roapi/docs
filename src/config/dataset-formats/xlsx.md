# Xlsx(Microsoft Excel)

To load the `.xlsx`, `sheet_name` needs to be specified in a config.

By default, most `.xlsx` files initially use Sheet1 as the `sheet_name`. Be sure to change this sheet_name as needed if your spreadsheet uses a different sheet_name.

Ex) Sheet1

![xlsx_sheet_name](../../images/xlsx_sheet_name.png)


```yaml
tables:
    - name: "excel_table"
      uri: "path/to/file.xlsx"
      option:
        format: "xlsx"
        sheet_name: "Sheet1"
```



If no `sheet_name` is specified, ROAPI will throw the error.