# Data Import Wizard

This is used to import data into salesforce. It has following features

- It helps to import data from excel/csv format into Salesforce.
- One can find this in setup.
- This can import upto 50,000 records at a time.
- One can perform insert, update & upsert **(insert and update together)** operations.



To import data we need to follow below steps:

1. Search **Data Import Wizard** in quick search box.
2. Click on **Launch Wizard**.
3. On the Selection page, Select the object you want to import data for
4. Select whether you want to:- 
   - **Add New Records**
   - **Update existing Records**
   - **Add New and update existing Records**
5. Select appropriate options in this section
   - **Match By** => Is used to match the record by some Id in excel (This is used when we want to update or upsert records)
   - **Record Owner** => Is used to give records automatically an owner. *Remeber ownder field in excel should have values of owner as **User Id** user have in Salesforce org*.
6. In the **Maping** section map the fields to their respective headers.



# Data Loader

- It helps to import data from excel/csv format into Salesforce.
- It can import 5 million records at a time.
- Available operations are
  - Insert
  - Update
  - Upsert
  - Delete
  - Export
  - Export All (inluding deleted records)



We need to download Data Loader on our system to use it.
