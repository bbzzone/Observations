# Text Fields

There are many fields for text values like

- Text (Simple single line text input)
- Text Area
- Text Area Long
  - Here we can select number of visible lines vertically
- Text Area Rich
  - This Text Area will allow text styling adding images and many other things that a rich text editor supports.
  - Here again we can select number of visible lines vertically.
- Text Encrypted



# Checkbox

There are only 2 states of a checkbox, Selected or Not selected. We can set it's default state while creating it in object. This can be used to show values which have only 2 states.



# Picklists

Picklists are like drop down menu's where we have to select single or multiple values from a given set of values.

- Picklist
  - Here we can choose to select picklist items from our custom items or from global picklist values.
  - There is options to show items in alphabetical order and to set first value as default value.
  - In case we are getting our options from external source like an Excel sheet, then we can restrict the values to be shown by checking the next checkbox *(Restrict picklist to the values defined in the value set)*. If we have 5 values in our Excel sheet and we only want 4 then we can add those 4 values to the Value set and check this box to insure that only items in Value Set will be available for selection.
  - It is considered **best practice to check restriction checkbox**.
- Multi-Select Picklist
  - Similar to Picklist but we can select multiple values rather than a single one
  - Like Text Area large we can set number of visible lines in this too.

We can add/delete/deactive a picklist value by navigating to Fields and Properties of the Object and then by going to Picklist. There we have the option to modify the items in the picklist.



## Global Picklist Value Set

There will be cases where we need same picklist for different object, creating multiple picklists for every object is possible but is very time consuming and repeating. To avoid such scenarios we create global picklists which are defined only once and can be used multiple times.

To create a global value set

1. Navigate to Home
   1. Search for Picklist Value Sets in Quick Search menu on left.
   2. Click on **Picklist Value Sets** and click new button to create new Value set
   3. Add Label, Name and Values in the picklist.
   4. There will be options to Show them alphabetically or Setting first as default in Value set
   5. We can't set these values while creating picklist with Global Value Set.
   6. **More values can be added in Picklist Value Set** by Navigating to Picklist Value Set and adding new Values from there.
   7. If there is a value you dont want to use and also don't want to delete you can deactivate it instead of deleting it. That way it will not be visible while creating records.



# Field Dependency

It Create a dependent relationship that causes the values in a picklist or multi-select picklist to be dynamically filtered based on the value selected by the user in another field.

To create Field Depenecny between a field and a picklist, we need to navigate to object's Fields and relationship section and from there we need to create a relationship between both fields.

This is like creating different picklists for different type of users depending on a particular value. That can be age, country, color anything.



# Schema Builder

One can access Schema Builder by Going to home and in quick search *Schema Builder*.