# Formula Field

These are read only field which are populated based on expression or formula automatically.

There are 2 different kind of formulas field in salesforce, **Simple formula and Advanced Formula**. Simple Formula will only have simple mathematically expression while Advanced Formula will have many features like If condition, abs functions, ceil, floor, Right, Left and many more. Using this field one can add many different conditions and Mathematical expressions so that it becomes easier to calculate the value of the current field. 

A Formula field can depend on **multiple other fields**. 



# Validation Rule

Restrict record's creation and updation based on certain rules. We will define those conditions using validation rules.

To create validation record on an object, we need to navigate to object using object manager and then to validation rules in it's settings. From there we can create validation rules. We can ***activate or deactivate validation records from a checkbox in there***. 

One can set error location too using these rules. If validation rule is using only 1 field then we can show the error message near to that field otherwise if it is running on multiple fields then we can set validation error to be visible on top of the page.

There are various ways to set a validation rule in Salesforce. Take an example of writing a simple **OR** condtion, these are few ways one can set that condition.

- `age > 12 || age < 18`
- `age > 12 OR age < 18`
- `OR( age > 12 || age < 18 )`

There are various other functions as well e.g. `ISBLANK(field_name)` to check if a field is blank or not.



# Page Layout

Page Layout are layout of a record. This is the layout of the input page while we will be adding records in the object. There are other usage of Page Layout like creating 2 different page layouts on different selections.

- By using **Page Layouts** one can create sections in Input Page Layout.
- By using **Record Type with Page Layout** we can achieve so many creative things. 

We can create different Page Layouts for different cases and we can control which to show with the help of Record Type.



# Record Type

With the help of record type one can control values of picklist and Page Layouts depending on different scenarios or cases.

**To create Record Type** we need to navigate to Object through Object Manager and from there we need to go to **Record Types** to create new Record type.

- Go to Record Types
- Click on New to create new Record type
- Enter Record Label and Record Type Name(For API Usage)
- Set it to **active**.
- Check Make Available for profiles you want that record to be.
- Then click next
- On the next page you will be welcomed with a screen for selecting page layout you want to bound the record type to.
- On pressing save your record type will be created with a new page to **Edit Picklists for various Record Types**.

As Record type is created now, while creating a new record user will be asked to choose the Record Type and as per user selection next Layout will be shown to the User.

To **change layouts for different Record Types** one can navigate to Record Type section and from there *Page Layout Assignment* and there one can select different page layouts for a particular record on a particular profile.

- **To DELETE a record type we need to deactivate it first.**
- **RECORD TYPE field can also be added in Record by going to page layout and dragging the RECORD TYPE field which is created automatically**.
- **If we have a validation check for a field which is not available in particular layout we need to modify that check and need to add Record Type in that check**.

Use Something like this

`RecordType.Name = "Fresher"` => If Record Label is Fresher then it will work

`RecordType.DeveloperName = "Fresher"` => If Record Name is Fresher then it will work.

**It is a better practice to use DeveloperName instead of Name because DeverloperName/API Name will be unique but label can be used multiple times.**



# Compact Layout

Compact layout is the header when we open a particular record. By default only Record Id (Primary key) of the Record is available there but we can add multiple values there.

We need to navigate to *Compact Layout* section in Object Settings. There we need to create new Compact layout. Then we can add or remove fields we want to see in header of the record information.



To assign this layout we need to go to the top right corner `Compact Layout Assignment`. From there we can link the layout with Record type.

