# Xlsx2Sqlite

Map xlsx files to database table convert

## How to use?

- First make sure that python is installed on your machine

in terminal write

```sh
python --version
```

- Ensure you have the necessary Python packages installed. You can install them using the `requirements.txt` file.

```sh
pip install -r requirements.txt
```

- Write your own `config.json`

```json
{
  "info": {
    "csvFilePath": "data.xlsx",
    "dbFilePath": "database.db"
  },
  "mapping": [
    {...}
    {
      "csvSheet": "Sheet1",
      "dbTable": "Table1",
      "dbConstraints": ["FOREIGN KEY(titleId) REFERENCES titles(id)"],
      "columns": [
        {
          "csvColName": "id",
          "dbType": "INTEGER NOT NULL PRIMARY KEY"
        },
        {
          "csvColHeader": "B",
          "dbColName": "age",
          "dbType": "INTEGER"
        },
        {
          "csvColName": "student_name",
          "csvColHeader": "C",
          "dbColName": "name",
          "dbType": "TEXT NOT NULL"
        }
      ]
    }
  ]
}
```

- Run

```sh
python main.py
```

## Understand `config.json`

`config.json` has two main property

- info
- mapping

### info

```json
"info": {
  "csvFilePath": "data.xlsx",
  "dbFilePath": "database.db"
},
```

Use to identify the path of input and output files

- "`csvFilePath`":

  - for the excel fiel path
  - if the file exist in the same dir of main.py jsut type the file name

- "`dbFilePath`"

  - for database file output dir

make sure to type file extensions

### mapping

```json
{
  "csvSheet": "Sheet1",
  "dbTable": "Table1",
  "dbConstraints": ["FOREIGN KEY(titleId) REFERENCES titles(id)"],
  "columns": [
    ...
  ]
}
```

is a list of json objects to identify the relation between xsls sheets and db tables and there columns

- "`csvSheet`":

  - for excel sheet name

- "`dbTable`":

  - for database table name
  - not required
  - if not given it will equal `csvSheet`

- "`dbConstraints`":

  - for others constriants

- "`columns`":

  - the relation between sheet column and db table columns

#### column object

```json
{
  "csvColName": "student_name",
  "csvColHeader": "B",
  "dbColName": "name",
  "dbType": "TEXT NOT NULL"
}
```

- "`csvColName`":

  - column name in xlsx

- "`csvColHeader`":

  - column header in xlsx `A B C ...Z`
  - not required

- "`dbColName`":

  - column name in database table
  - not required
  - if not given it will equal `csvColName`

- "`dbType`":

  - column type in database table
