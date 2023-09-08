# Relationships
By using relationships we will be connecting 2 Objects or 2 Records with each other.

## One to Many Relationship
In this type of relationship a single field is related to different other fields.

### Lookup Relationship
This is the type of relationship where one object is linked with another object. Relationship field allow user to click on lookup icon to select a value from a popup list. This is a loosely coupled relationship (If parent is delete no effect will be reflected on children).

We create lookup field in child elements.
1. First we will create a parent object, on which our children will depend.
2. When parent is ready we will create a new lookout field in child by going to field and relationships of the child object.
3. There we will select data type of the new field to be **lookout field** and will click next.
4. On the next screen we will select the parent element on which field is dependent from a drop down list.
5. Now we will select the label and name of the field. Here we will set **Child Relationship Name** which we will be using in development.
6. There will be option of what to do when lookup field is deleted. If value of lookup field is required then you won't be able to delete the parent of lookup field.
7. We can also choose label of related field on the very next page.

### Master-Detail Relationship
Creates a special type of parent-child relationship between two objects. Unlike *Lookup Field*, if parent is deleted all the child records will be removed (**Tightly coupled Relationship**).  **Rollup Summary** can be created on master record so that detail records can be summarized. Ownership and sharing of detail record will be decided by the master record like if a user is owner of the parent record, he will also be the owner of the child record. 
- **A field in master-detail relationship is a required field**.
- **If we have records added already in the object without master-detail field then we won't be able to create a master-detail field**. For that we need to create a lookup relationship first then populate all records with that relationship then change the relationship type to Master-Detail.

1. First we need to create parent Object.
2. Now we need to create a field in child with data type of **Master-Detail Relationship** 
3. Now we need to define Field Label, Field Name.
4. On the same page we need to set Sharing Settings. We need to select whether record is editable by a person with only read access or read/write access.
5. There is another checkbox for **Reparenting**. If this is checked then Parent of the field can be changed. 
6. Standard Objects can't be on the detail section of a custom object in Master-detail Relationship.

### Rollup Summary
This is a read-only field which can be used to calculate the **sum, count, min, max** for a parent record relationship. If parent have relationship with 10 children then count Rollup Field will give it's value as 10.
*One can also select fields for Rollup Summary by filtering them*. ***Remember to create it on Parent field instead of child***.

### Convert Master-detail to Lookup
To convert master-detail to lookup, we need to **remove all the Rollup Summary** fields from parent and then we can simply change the data type.

## Many to Many Relationship 
To create many to many relationship, we need to create a junction object. A junction object is the one which contains relationship with different children.
**We can only create 2 Master-detail Relationships on a single object**
