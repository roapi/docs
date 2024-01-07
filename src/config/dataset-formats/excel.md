# MS Excel compatible formats.

ROAPI supports loading a few Microsoft Excel compatible formats like xls, xlsx, xlsb, ods.

## Configuration
To load MS Excel compatible files the config should be specified like:
```yaml
tables:
    - name: "<table name>"
      uri: "<files path>"
      option:
        format: "<file format>"
        sheet_name: "Sheet1"
        rows_range_start: 2
        rows_range_end: 5
        columns_range_start: 1
        columns_range_end: 6
        schema_inference_lines: 3
```
* **format** - name of file format. Currently supported files format:
    * xls (Microsoft Excel 5.0/95 Workbook)
    * xlsx (Excel Workbook)
    * xlsb (Excel Binary Workbook)
    * ods (OpenDocument Spreadsheet)
* **sheet_name** - the name of the spread sheet with table data. By default, most files initially use Sheet1 as the `sheet_name`. Be sure to change this `sheet_name` as needed if your spreadsheet uses a different name.
![xlsx_sheet_name](../../images/xlsx_sheet_name.png)
If no `sheet_name` is specified, ROAPI will use first spreadsheet.
* **Table range options**
    * **rows_range_start** - the first row of the table. It contains column names. By default, `rows_range_start` is 0 (the first raw in spreadsheet)
    * **rows_range_end** - the last row of the table. By default, ROAPI reads all data.
    * **columns_range_start** - the column of the table. By default, `columns_range_start` is 0 (first column in spreadsheet)
    * **columns_range_end** - the last column of the table. By default, ROAPI reads all columns.  
For example, to take only selected data:
  ![spread_sheet_range](../../images/spread_sheet_range.png)
  the config file looks like:
```yaml
tables:
    - name: "<table name>"
      uri: "<files path>"
      option:
        format: "<file format>"
        sheet_name: "Sheet1"
        rows_range_start: 1
        rows_range_end: 4
        columns_range_start: 1
        columns_range_end: 3
```
* **schema_inference_lines** - the number of rows (inside table range) to use in schema inference. This number includes the row with column names, so, for example, `schema_inference_lines: 3` means ROAPI will use first row for column names inference and 2 rows for column types inference. If this option is not specified then ROAPI reads all rows for column data types inference.

## Schema inference. 
ROAPI can infer schema of data automatically. The first row of data range is a row with column names. After column names inference ROAPI will infer data types by scanning all remaining rows or limited number of rows specified in `schema_inference_lines` option.
If column contains more than one data type (for exaple, float and int) then ROAPI use Utf8 datatype.

Also, it is possible to specify schema in configuration file. This allows to avoid schema inference from data and loading of table will be faster.

```yaml
tables:
    - name: "excel_table"
      uri: "path/to/file.xlsx"
      option:
        format: "xlsx"
      schema:
        columns:
        - name: "int_column"
          data_type: "Int64"
          nullable: true
        - name: "string_column"
          data_type: "Utf8"
          nullable: true
        - name: "float_column"
          data_type: "Float64"
          nullable: true
        - name: "datetime_column"
          data_type: !Timestamp [Seconds, null]
          nullable: true
        - name: "duration_column"
          data_type: !Duration Second
          nullable: true
        - name: "date32_column"
          data_type: Date32
          nullable: true
        - name: "date64_column"
          data_type: Date64
          nullable: true
        - name: "null_column"
          data_type: Null
          nullable: true
```
