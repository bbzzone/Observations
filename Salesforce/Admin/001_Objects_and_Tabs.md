# Objects

Objects are like tables in database(like sql tables). It has rows, columns and data cells.

<table>
    <tr>
        <th>Salesforce Term</th>
        <th>In Excel Terms</th>
    </tr>
    <tr>
    	<td>Object</td>
        <td>Table</td>
    </tr>
    <tr>
    	<td>Record</td>
        <td>Row</td>
    </tr>
    <tr>
    	<td>Field</td>
        <td>Column</td>
    </tr>
    <tr>
    	<td>Data Value</td>
        <td>Data Value</td>
    </tr>
</table>



There are 2 types of Objects in Salesforce. **Standard Objects** and **Custom Objects**.

## Standard Objects and Custom Objects

These are objects which are already created by salesforce and one can look at them by opening Object Manager tab where there will be a type column to tell weither object is custom or Standard Objects. There are various standard objects like **Account, Contact, Case, Lead, Opportunity etc.**

Custom Objects are one which are created by developer or admin as per requirement. One need to create a **[Tabs](#Tabs)** to view custom objects in an app. One can look at various apps by clicking on launcher button and then by clicking prebuilt apps like sales cloud, service cloud etc.



### Standard vs Custom Objects

We need to create **Label, Plural label and API Name** for Standard and Custom Objects. These are all different for both types of objects. One can use any type of Plural name but their is a standard which most of the people follow.

**Label is the name of the object. Plural Label is used for Tabs for that particular object and API Name is used in features like flow, apex etc.**

<table>
    <tr>
        <th></th>
        <th>Standard</th>
        <th>Custom</th>
    </tr>
    <tr>
    	<th>Label</th>
        <td>Account</td>
        <td>Student</td>
    </tr>
    <tr>
    	<th>Plural Label</th>
        <td>Accounts</td>
        <td>Students</td>
    </tr>
    <tr>
    	<th>API Name</th>
        <td>Account</td>
        <td>Student_c</td>
    </tr>
</table>



## Tabs

Tabs can be used to navigate around in the app. There are 2 types of navigations in salesforce **Standard Navigation and Console Navigation**. To see object on UI we need to create a Tab for that object which will be internally connected with Object it is navigating user to. Without being able to navigate to the object we will fail to view, edit or enter information in a particular tab.

On clicking the tab it will open the homepage for that particular object from where we can view, update or delete the records in that object.



## Creating Objects

We need to navigate to Object manager from there we will click on create new Object. 

1. Open Salesforce Home.
2. Click on Object Manager
3. Click on Create Object.

After clicking Create Object a form will open with many different fields also containing **Label, Plural label and Object Name(For API Reference)**. 

While creating an object it is neccessary to create at least one field (column). So there is also an option for a Record Name and it's data type.

Record Name will be the label for your field and data type can be **text or autonumber**. 

Auto Number is a number which will be incremented automatically we only need to define the **display format** and starting value of the field.



### Optional Features

**After setting Record Name one will navigate to optional Features**

?????



Now after going through all the options we need to check Launch new Custom Tab Wizard. This makes it easy to create tab for the particular object but if we forgets to create a tab using this check, we can create tab later for the object.

### Tab creation

1. After clicking save the object with *Launch new custom tab wizard checked*, a new page for tab creation will open which will have option to select object, there we will select the **object** which we need to navigate throught that tab. Now we need to select **Tab Style** from already created tab styles by salesforce.
2. After clicking next, we will be navigated to a page for selecting Tab visibility for different types of profiles. Like if we want tab to be invisible for `Custom community user` profile then we can do that in this page.
3. Now it will ask for which apps we need to add the custom tab. It will list all the apps and we need to select the ones which we want our new custom tab in.

- **If we forgot to create the tab for the object while creating the object**. We can create it by going to Home and navigating or searching tabs and then the same menu as before will appear and we can create the tab for that object.



## Fields in Salesforce

Fields are like columns in an excel sheet. But like other databases we need to define data type with fields. 

**To add a field we need to navigate to the Object in Object manager**

1. Navigate to Object we want to add field to.
2. Click **Fields and Relationships**
3. Click new to create new field.
4. Then choose the **Data Type** of the Object
5. Then set the **label for the Field** (column name), Length of the field and **Field Name** (API Name)
6. One can also add help text(will add a exclamation button which on hover will give help text) and description text. Values like **Required, unique and Default Value** can be set in this page itself.
7. In the next step set the profile visibility for that particular Field.
8. In the next step we need to set if the field is visible for page layout(Inside Record -> Details section).



There are various datatypes for salesforce fields. **Auto Number, Formula, Roll-up Summary, Lookup Relationship, Master-Detail Relationship, External Lookup Relationship, Checkbox, Currency, Date, Date/Time, Email, Geolocation, Number, Percent, Phone, Picklist, Picklist(Multi-Select), Text, Text Area, Text Area (long), Text Area (Rich), Text (Encrypted), Time, URL**



## Creating Records

In the app we need to navigate to the Object using tab and from there we can add new records by clicking on new button.

While creating record if we **forgot to add it to app layout** we can later go to object manager than to object itself and in it's layout settings, where we can drag and drop our record to be visible in layout.

## Creating Apps

App is a container for all the objects, tabs and other functionality. A salesforce app only consists of a name, logo and an ordered set of tabs.

**To create app we need to navigate to App Manager**, There we need to select **New lightning app**. It will open a menu where we need to fill all the details of the app like app name, it's details and developer name which again will be used by api. We can also add logo for the app.

On the next page we need to select Navigation Style (Standard or Console Navigation), Supported Form Factor(Desktop, Phone or both), Setup Experience  and some Personalised Settings.

By clicking next we will be navigated to add utility items. Utility items are visible at app's bottom similar to bottom navbar in mobile(Android) apps.

After adding Utility Items we need to add Navigation Items like the custom tabs we created for different object we needed in our app.

After that we need to add Profiles to the app. **It is very important to add System Administration profile to the app for full access of the app otherwise it can create problems in near future**.

To ***EDIT THE APP*** we need to navigate to App Manager and select the app and click edit. From there we can edit the settings of the app.



## Best Practices

There is some order which is consider better to create salesforce apps than other orders.

1. Create an Object
2. Create a Tab
3. Create Fields in Object
4. Create App
5. Create Records
