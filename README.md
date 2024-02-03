# Excel-as-Database

[![npm version](https://badge.fury.io/js/excel-as-database.svg)](https://badge.fury.io/js/excel-as-database)

Excel-as-Database is a powerful Node.js package designed to leverage Microsoft Excel sheets as a lightweight and easy-to-use database solution. This package simplifies CRUD operations and enables developers to seamlessly interact with Excel files as if they were conventional databases.

## Features

- **Simple Integration:** Easily connect your Node.js application with Excel files, treating them as databases for data storage and retrieval.

- **SQL-like Operations:** Utilize SQL-like syntax to perform CRUD operations (SELECT, INSERT, UPDATE, DELETE) on your Excel data.

- **Error Handling:** Comprehensive error handling ensures robust performance even in challenging scenarios.

- **User-Friendly API:** The package provides a straightforward API for developers to interact with Excel files programmatically.

- **Multiple Tables:** Each sheet in the Excel file is treated as an individual table, allowing you to work with multiple tables within a single Excel document.

- **Extensive Data Checks:** The package includes extensive checks on manually entered data in the Excel sheet, ensuring data integrity and preventing common errors.

## Installation

```bash
npm install excel-as-database
```

## How to use

1. **Connect to the excel file**

```js
const excelAsDatabase = require('excel-as-database');
const localExcelDb = new excelAsDatabase(`/your/absolute/folder/path/`);

await localExcelDb.createExcel(); // this will create a new Excel file at the provided folder path
```

2. **Create tables**

   - Open your terminal or file explorer and go to `/your/absolute/folder/path/`
   - Make sure you have an Excel file named `ExcelDB.xlsx` in the specified folder. This file will serve as your database.
   - Open `ExcelDB.xlsx` and refer to the 1st sheet, which acts as a template for creating other tables.
   - The 1st sheet is reserved for template use only; please avoid modifying this sheet.
   - Explore and use sheets starting from the 2nd sheet onwards for creating new tables.
   - Utilize the structure and layout of the 1st sheet as a guide for designing your new tables.
   - Treat each sheet in `ExcelDB.xlsx` as a separate table.
   - Configure the table schema according to the image provided below:

   ![Table Schema](https://github.com/svfodekar/Notes/assets/121047125/7d3ab6b0-c1c4-4dca-85e3-44b3db4aa346)

Ensure that you follow the specified folder path, use the correct Excel file (`ExcelDB.xlsx`), and refer to the provided image for setting up the table schema.

## CRUD operations

1. **SELECT**
```js
const selectSql = {
    from: "users",
}

const selectSql = {
    select: ["*"],
    from: "users",
}

const selectSql = {
    select: ["rollNo", "name"],
    from: "users",
    offset: 10,
}


const selectSql= {
    select: ["rollNo", "name", "surname"],
    from: "users",
    where: " name != 'john' ",
    orderBy: ["name desc"],
}

const selectSql = {
    select: ["rollNo", "name", "surname", "SUM(marks)", "AVG(marks)", "MAX(marks)", "MIN(marks)", "COUNT(marks)"],
    from: "users",
    where: "isActive != false and ( rollNo < 100 or name = 'john' ) and dob = 11/11/1995 and (marks + 10 > 50 )",
    groupBy: ["rollNo", "name", "surname"],
    having: "SUM(marks) + 5 <  150 ",
    orderBy: ["rollNo", "name desc", "surname asc"],
    limit: 4,
    offset: 2
}


const data = await localExcelDb.select(selectSql);

```

2. **INSERT**

```js
const insertSql = {
    table: "users",
    insert: [
        {
            name: "lee",
            isActive: true,
            surname: "Yu",
            dob: "13/06/1999",
            marks: 45
        }, {
            name: "mock",
            isActive: false,
            surname: "rid",
            dob: "13/06/1994",
            marks: 41
        }
    ]
}

await localExcelDb.insert(insertSql);

```

3. **UPDATE**

```js
const updateSql = {
    table: "users",
    set: {
        isActive: false,
        marks: 0
    },
    where: "dob = 11/07/1980 and marks <= 20"
}

await localExcelDb.update(updateSql);
```

4. **DELETE**

```js
const deleteSql = {
    from : "users",
    where : "isActive = false and marks <= 0"
}

await localExcelDb.delete(deleteSql);

```

## Contributing
Feel free to contribute by opening issues, submitting pull requests, or suggesting improvements. Your feedback is valuable!
Git repository - https://github.com/svfodekar/excelAsDatabase

## Author
**Saurabh Foddekar**
- Email: svfodekar@gmail.com
- LinkedIn: [Saurabh Fodekar](https://www.linkedin.com/in/saurabh-fodekar-b094591b4)
