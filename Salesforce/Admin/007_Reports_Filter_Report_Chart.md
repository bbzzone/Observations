# Reports

This is used to dispaly records based on certain criteria just like listview but with additional functionality which list view doesn't provide.

- We can apply filter, groups and Mathematic calculation while showing records.
- We can also display reports in graphical format.
- Every report is stored in a folder which decides how one can access reports to View, Edit or Manage those.
- Reports folder can be public, hidden or shared.



## Report Builder

- This is used to create a report.
- We need to select a report type
- Select fields to display in our report
- Apply filters
- Group report based on rows and columns
- Run reports and save reports



## Filters

There are filters which one uses to filter the records to add in report builder. There are 4 types of filters

1. *Standard Filter* => Show me & Created Date (These are fields in Filters of Reports)
   - In the Filter section of Reports page there are 2 fields *show me* and *Created Date*
   - From *Show me* select => type of objects you want to see
   - From *Created Date* => Select objects from a certain time period
2. Field Filter => Specific to fields.
   - In Filter section press on search bar and select the field you want to add filter on and press enter.
   - Now select the value you want to filter on and select the logic (equals, not equals, greater etc.).
3. Filter Logic => Boolean condition to control Field Filters. (Multiple fields filters with AND OR logic)
   - If you have applied multiple filters, Go to Filter section and Press drop down arrow.
   - From drop down menu select **Add Filter Logic**. Select if you want filter to be like (1 OR 2 AND 3) or in any other configuration.
4. Cross Filter => Filter a report by child object using With or without condition. (When we create filters using multiple objects)
   - Cross filters are used to filter objects based on whether that object has links to another object or not.
   - Go to Filter section than press *Add cross filter*. 
   - Select Object 1 and relationship (**with** if object 1 needs to have a relationship with object 2, **without** otherwise). Now select Object 2.



## Report Formats

- Tabular
  - Make a List
- Summary
  - Group & Summarize by Rows only
- Matrix
  - Group & Summarize by Row and Column
- Joined
  - Report on multiple Report Types.



## Report Folder

Reports are stored in folder which can be **public, hidden or shared**. By using these properties we can control the access of content of the folder based on **Roles, Permissions, Public Groups, Territories and license types.** We will not be sharing reports individually but instead we will be sharing report folders. We can give 3 types of access **View, Edit and Manage(View, Edit and Share with other users)**. 

1. To add a Report Folder. We need to go to Report Tab of the object. 
2. On the top right corner we need to select **New Folder**
3. Then Enter Name for the folder and save.



## Tabular Report

Before adding Reports we need to add **Reports Tab and Dashboard Tab** to our application.

1. Navigate to **Reports** Tab.
2. On the top right corner Click **New Report**.
3. Select **Report Type** and a right pane will appear press **Start Report** there.
4. It will open a new page with 2 Tabs in left pane **(Outline, Filters)**.
5. In **Outline** there are 2 sections one is **Groups** which will be used to created summarised or matrix Report.
6. 2nd section is of **Columns** where we select which fields to display in the report page.
7. We can select multiple fields and order them by dragging them around.
8. In the **Filter** tab we can add [Filters](#Filters) like Standard, Field, Filter logic and Cross Filter.



## Summary Report

Summary reports are very similar to [Tabular Reports](#Tabular-Report) infact the first step to create Summary Report is to create a [Tabular Report](#Tabular-Report). The only thing different in Summary Report is that we can group Records with similar field value. If we have 5 persons with similar phone number, we can group all those records. This is the additional functionality we get on summary reports.

**We can also create charts in Summary Reports**.

1. Create a Tabular Report.
2. To Group it by a particular field click on **Add group** searchbox inside **Groups** section.
3. On clicking Groups it will automatically filter the items by group name and show data accordingly.
4. We can add total for a number field by clicking on it in **Columns** section. It will show a summarize field where we can check **Average, sum, max, min or median**.
5. We can also add charts by using **Add chart** button, we can change the chart properties by clicking gear icon of chart.



## Matrix Report

These are again similar to [Summary Report](#Summary-Report), we just need to add a group based on column too to make a Matrix Report from Summary Report.



## Report Type

- It is like template for reports
- These determines which records and fields are available for use.
- This is based on relationshipts between a primary obhect  and its related object.
- These can also be set to show only records **with** links to related object or **with or without** related object.



### Create Report Type

Before creating **Report type** we need to check **Allow Reports** on object Details page.

1. In the Setup page search for **Report Types**
2. Click **New Custom Report Type**.
3. Select the Primay Object.
4. Select the Category to add current Report Type to.
5. On clicking **Next** you will move to a page where we need to select the related Objects.
6. Here add the child object related to **Primary Object** and select the relationship you want between them.
7. Selecting **Each "A"** will only add records which have both objects presents and selecting **"A"** will select all the records in Primary Object.
8. To add or remove fields for the Primary Object click on **Edit Layout** after saving the Report Type.
9. From there you can select fields to add in Report Type and then click Save.



## Filter By Scope

1. Go to Object manager.
2. Select the Object on which we need filter on.
3. Select Scoping Rules from left pane.
4. Click on **New Scoping Rule**.
5. Set **Rule Name** and set **Rule Criteria** where field equals True.
6. After setting **Rule Criteria** we need to set **Record Criteria** by using which we can filter records based on Record data.

**Filter by Scope** will work in ListView and in Reports.



## Joined Report

These are the reports which can be created by joining more than one record type. By using this we can create a single report on different objects.

1. Create a new Report
2. On the top left corner from the drop down, select **Joined Report** by clicking on **Report**.
3. It uses **blocks** to add multiple Report Types.
4. We can add another **Record Type** by clicking on **Add Block** button.
5. This will add another section to the reports page with another report type.
6. We will have different section for columns and filters for different blocks but single grouping will work on both.



## Bucket Fields

Bucket fields are used to group different values. Suppose we have a field stream. Here we want to merge students from Medical and Non-medical to be treated similarly than we can create a bucket for this.

Open a report and on a field name click on drop down and select **Bucket this Column**. 

1. For Text values we need to **Add a Bucket** and Select values to add in bucket.
2. Click on **Move To** button to move those values to a particular bucket.
3. For remaning values you can create another bucket or check **Bucket remaining values as Others** which will create another bucket with the name of others.
4. Doing this will create a new column where values for each record will depend on bucket name. 
5. We can **Group** based on this column by going to **Groups** and selecting the **Bucket** we created.



## Row Level Formula

This is similar to **Formula Field** in an object, the only difference is that Bucket fields and Row level formula is **only available in Reports**.

To add a row level formula

1. In the reports page click on drop down on **column** (present in left pane).
2. Click on **Add Row level formula**.
3. Provide column name and your formula for the field to output something.
4. Click save and New column will be there in the report sheet.



## Reports on Duplicate Records

To check for Duplicate Records one need to create a Report Type for that. Report Type will not pe created on any specific Object. We will create it on Standard **Duplicate Record Sets** type.

1. Go to **Report Types** from quick search Box.
2. Select **Duplicate Record Set** as primary object.
3. Fill other details as well
4. On next page select **Duplicate Record Items** as secondary object.
5. Now **Create new record** in the object you want to check duplicacy in.
6. You will see 2 columns in report of object.
   1. **Duplicate Record Set Name**
   2. **Duplicate Record Item Name**
7. We can group by **Duplicate Record Set Name** as it will be similar for all duplicate records of one type.
8. This **Report** will return every object which is duplicate in the org.



# Dashboards

To create Dashboard we need to create [Reports](#Reports) as **dashboard is a visal display of key metrics and trends for records in an org**.

- Reports are the source for dashboard.
- A single report can be added in multiple *dashboard components* on a single dashboard.
- Having multiple reports on a single dashboard page makes it a powerful visual display tool.
- Like *Reports* dashboard are saved in **Dashboard Folders**.
- To view dashboard one need to have access to dashboard folders.
- To view reports in dashboard components one also need to have access to reports which are present in *dashboard components*.



- Each Dashboard has a running user.
- Running user's security settings determine which data to display in dashboard.
- If the running user is a specific user, then all dashboard veiwers sees data based on the security settings of that user, regardless of their own security settings.
- **Dynamic Dashboards** are those for which running user is always logged in user. Here, each user views the dashboard as per their own security settings.



## Create a Dashboard

This process is very similar to reports.

1. Add dashboard to the App.
2. Go to dashboard Tab in the app.
3. Click on **New Dashboard**. Create the new dashboard by following the menus.
4. Now on Dashboard page click on **Component** to add a report.
5. From here we can select Reports we want to show on our dashboard.
6. We can edit the report like change chart type or add columns or add groups in our dashboard reports *(Changes in dashboard reports won't reflect on actual Report)*.



# Adding Report and Dashboards on Lightning Page

## Adding Report on Record Page

1. Open **Lighting App Builder** or open the record page and click on gear icon and press **Edit**.
2. Add **Report Chart** chart component from left pane to the record page layout.
3. **Remember recrods which have charts enabled will be the only ones which will be eligible for visualisation in  Record page**. So you can not place *tabular reports* on record page.



## Adding Reports and Dashboard on Home Page

1. Open **Home Page** (any lightning page you want to edit) by going to **Lighting App Builder** or by clicking **Edit Page** by clicking on gear icon on Home Page.
2. Add **Report Chart** or **Dashboard Component** on Page Layout.
3. Select the reports or dashboards you want to select from the list of available dashboards for the user.
4. Click save when components are aligned properly and it will reflect on your lightning page.



## Share Report and Dashboard

We can't share Reports or Dashboard individually but instead we can share containing folder to other users. 

1. For that we need to navigate to the Reports/Dashboards Tab in our app.
2. Click on **All Folders**
3. Click on the down arrow buttong near Folder name
4. Select Share from there.
5. Now we can add users we want to share our folder with. (Sharing rules can also be set using **Roles, Public Groups, Role and Subordinates**).
6. Anyone with whom that folder is shared will be able to access all the reports or dashboards within that folder.



**To allow other users to edit your dashboard** you need to go to user's profile and on the profile page and go to System Permissions and check the ***Edit my dashboard*** button.

