# Data Security

Date security is important as we need to provide which user have access to which part of the application. Salesforce has layered Sharing Model.

There are 4 layers of Data Access in Salesforce=>

1. [Organization level Security](#Control-Access-to-the-Org)
2. [Object level Security](#Control-Access-to-Objects)
3. [Field level Security](#Control-Access-to-Fields)
4. [Record level Security](#Record-level-Security)

## Control Access to the Org

With this type of access we can create users, deactivate user accounts, create password policies, specify trusted IP Ranges or set *login access by time*.

### Manage Users

Every Salesforce user is identified by a username, a password, and a single profile. Together with other settings, the profile determines what tasks users can perform, what data they see, and what they can do with the data.

**To view users in your org** => In Quick find box search Users then select Users.



### Create Users

1. In Quick find box navigate to *Users*.
2. Click *New User* or *Add multiple Users*.
3. Enter the user’s name, email address, and a unique username in the form of an email address. By default, the username is the same as the email address.
4.  Select the user license which this user will have. The license determines which profiles are available for each user.
5.  Select a profile, which specifies the user’s minimum permissions and access settings.
6.  Select the option to generate a new password and notify the user, then save.



### Deactivate a User

1.  From Setup, in the Quick Find box, enter Users, and then select  **Users**
2.  Click  **Edit**  next to the name of the user you want to deactivate.
3.  Clear the  **Active**  checkbox and click  **Save**. If you can’t immediately deactivate an account (for example, when the user is selected in a custom hierarchy field), you can freeze their account. That prevents the user from logging in to your organization while you’re working on deactivating them.
    -  On the Users page in Setup, click the username of the user whose account you want to freeze.
    -  Click  **Freeze**.



### Set Password Policy

Below steps will create password policies for all Users. (If there is any need to create different password policies for different users than we can create different profiles and give then different password policies as per our requirement.)
1. From Setup, in the Quick Find box, enter **Password Policies**, and then select **Password Policies**.
2.  Customize the password settings.
	-  How long should passwords be? Longer is usually better, within reason.
	-  How complex do you want your passwords? You can require alphabetical, numeric, uppercase, lowercase, or special characters.
	-  How many days is a password valid?
	-  How many times can someone try to log in with invalid credentials before being locked out?
3.  Choose what to do about forgotten passwords and locked accounts.
4.  Click  **Save**.



### Specify trusted IP Ranges

1.  From Setup, in the Quick Find box, enter  **Network Access**, and then select  **Network Access**.
2.  Click  **New**.
3.  Enter the start and end point of the range of trusted IP addresses, and click  **Save**.



### Restrict Login Access by IP Address Using Profile

1.  From Setup, in the Quick Find box, enter  **Profiles**, and then select  **Profiles**.
2.  Select a profile and click its name.
3.  Click  **Login IP Ranges**. (You need Enhanced Profile Interface Enabled to Use these settings)
    - Go to *User Management Settings* from Quick Find box.
    - Enable *Enhanced Profile User Interface.*
4.  Click  **New**.
5. Enter the start and end point of the range of trusted IP addresses, and click  **Save**.



### Restrict Login Access by Time

1.  From Setup, in the Quick Find box, enter  **Profiles**, and then select  **Profiles**.
2.  Click the profile you want to change.
3.  Under  **Login Hours**, click  **Edit**. (You need [Enhanced Profile Interface](https://help.salesforce.com/s/articleView?id=sf.users_profiles_about_enhanced_ui.htm&type=5) Enabled to Use these settings)
4.  Set the days and hours when users with this profile can log in to the organization.
    -   To allow users to log in at any time, click  **Clear all times**.
    -   To prohibit users from using the system on a specific day, set the start and end times to the same value.



## Profiles

- A profile is a collection of settings and permissions.
- Profile settings determine which data the user can see and permissions determine what the user can do with that data.
- A profile can be assigned to many users but a user can have only one profile at a time.



Below are the things a Profile can control

- Assigned App & Assigned Connected Apps (Custom App Settings) => *Apps to which profile has access to*.
- Object Settings
- App Permissions
- Apex Class & VF Page Access
- External Data Source Access
- Named Credential Access
- Flow Access
- Custom Permissions & Custom Metadata Type
- Custom Setting Definitions
- System Permissions



## Permission Set

- A permission set is a collection of settings and permissions that give user access to various tools and functions.
- Permission sets extend users functional access without changing their profile.
- Through Permission sets permission can be granted and any time it can be taken away as well.
- Users can have only one profile but they can have multiple permission sets.
- **Permission set is used to give permissions but it can't revoke permission from the user**.
- You can alsmost control everything that you can control with **Profile**.
- Expiration time can also be provided for **Permission Set**.



## Control Access to Objects

You can control whether a group of users can create, view, edit, or delete any records of that object.

### Manage Object Permissions

Object permissions can be set with the help of ***Profiles or Permission set***. 
- Every *Object* is bound with a *Tab* we create with it.
- Every tab has a *Profile* associated with it.
- So indirectly *Object* is associated with *Profile*
- **So we can say that what Object user will see is dependent on Profile User has**
- **Permission set can be used to grant additional permission to a user**.

There are 2 types of Profiles in a Salesforce org
1. Standard Profile => Predefined Profiles which are sufficient most of the times
2. Custom Profile => If creating a new Profile makes sense for an Org than one can create a *Custom Profile*.



### Create a Profile

1.  From Setup, in the Quick Find box, enter  **Profiles**, and then select  **Profiles**.
2.  Click  **Clone**  next to a profile similar to the one you want to create.
3.  Give your new profile a name, and save.



### Assign a Profile

1.  Make sure the Enhanced Profile User Interface is enabled in User Management Settings.
2.  From Setup, in the Quick Find box, enter  **Profiles**, and then select  **Profiles**.
3.  Click the name of the profile that you want to customize.
4.  Edit the profile, using the most restrictive settings and permissions you can for this user type. (Don’t worry about blocking the user from doing things they need to do. We'll open up more possibilities for them in the Use Permission Sets to Grant Access section below.)
5.  From Setup, in the Quick Find box, enter  **Users**, and then select  **Users**.
6.  Click  **Edit**  next to the user that you want to assign the profile to.
7.  In the  **Profile**  dropdown, select the profile that you just set up. Then, click  **Save**.



### Create a Permission Set

1.  From Setup, in the Quick Find box, enter  **Permission Sets**, and then select  **Permission Sets**.
2.  Click  **Clone**  next to the set you want to copy. A cloned permission set has the same user license as the original. To create a set with a different license, click  **New** instead.
3.  Enter a label and a description. The API name is a unique name used by the API and managed packages. It automatically replicates the label, but you can modify it.
4.  If this is a new permission set, select a user license option.
    -   If you plan to assign this permission set to multiple users with different licenses, select --None--.
    -   If only users with one type of license will use this permission set, select that user license.
5.  Click  **Save**  to go back to the permission set overview page.
6.  In the Permission set Overview page click on the Permission set we created than on **Manage Assignments** and than **Add Assignments**.



## Control Access to Fields



### Restrict field access with a Profile

1. From Setup, in the Quick Find box, enter Profiles, and then select Profiles.
2. Click the name of the profile that you want to change.
3. Click Object Settings and select the object for which you want to update the field settings.
4. Click Edit.
5. Under Field Permissions, for each field, specify the kind of access you want for users with this profile, and save your settings.



>  **One can also set field level permissions by going to Object manager and then navigating to field and pressing Set Field-Level Security**.

### Restrict field access with Permission Set

1. From Setup, in the Quick Find box, enter Permission Sets, and then select Permission Sets.
2. Select a permission set and click Object Settings.
3. Click the object you're working with, then click Edit.
4. Under Field Permissions, specify the kinds of access you need, then save this permission set.
5. Click Manage Assignments and select the users who you expect to need the permissions you’ve just specified. Click Add Assignments and Done.



## Permission Set Group

- A permission set Group is a bundle of different permission sets.
- A permission set group includes all the permissions available in the permission sets.
- One permission set can be included in more than one permission set groups.
- A user can be assigned **multiple permission set Groups**
- **Permission Set and Permission set Group** can be assigned together to a user.



### Creating Permission Set Group

1. Suppose you have 3 permission sets (PermS1, PermS2, PermS3)
2. There is a user which need all the permissions defined in (PermS1, PermS2, PermS3).
3. We can create Permission set for such use case.
4. Go to **Permission Set Groups** from quick search box.
5. Click on **New Permission Set Group** on the top right corner.
6. Provide a name for the permission set Group and then click Save.
7. Now in **Permission Sets** section click **Permission Sets in Group**
8. On the next page click **Add Permission Set** and then select all the permission sets which are required for the user.
9. From the next page you can click **Add Assignments** and select user to give permission set group to.
10. Or you can go to **Users** and select particular user and in the **permission set group assignment** you can set user to have a particular permission set group.
11. You can mute permission from permission set group, which will disable those permission in the permission set group but won't delete them.



## Record level Security

To control data access precisely, you can allow particular users to view specific fields in a specific object, but then restrict the individual records they're allowed to see.

***When object-level permissions conflict with record-level permissions, the most restrictive settings win.***

You control record-level access in four ways. They’re listed in order of increasing access. You use org-wide defaults to lock down your data to the most restrictive level, and then use the other record-level security tools to grant access to selected users, as required.
-   **Org-wide defaults** specify the default level of access users have to each other’s records.
-   **Role hierarchies**  ensure managers have access to the same records as their subordinates. Each role in the hierarchy represents a level of data access that a user or group of users needs.
-   **Sharing rules**  are automatic exceptions to org-wide defaults for particular groups of users, to give them access to records they don’t own or can’t normally see.
-   **Manual sharing**  lets record owners give read and edit permissions to users who might not have access to the record any other way.

### Setting org wide Sharing Defaults

There are some org wide record sharing access levels:

**Private**  => Only the record owner, and users above that role in the hierarchy, can view, edit, and report on those records.
**Public Read Only**  => All users can view and report on records, but only the owner, and users above that role in the hierarchy, can edit them.
**Public Read/Write**  => All users can view, edit, and report on all records.
**Controlled by Parent**  => A user can view, edit, or delete a record if she can perform that same action on the object it belongs to. (This setting applies on Master-detail relationship or lookup relationship where field is controlled by parent).

1.  From Setup, in the Quick Find box, enter  **Sharing Settings**, and then select  **Sharing Settings**.
2.  Click  **Edit**  in the Organization-Wide Defaults area.
3. For each object, select the default internal access and default external access.
4.  To disable automatic access using your hierarchies, deselect  **Grant Access Using Hierarchies**  for any custom object that doesn't have a default access of Controlled by Parent.

> **Default Internal Access** => This setting applies for user's inside current org.
>
> **Default External Access** => This settings applies for communities or experience sites *(These are websites which are created using salesforce).*

### Define a Role Hierarchy

1. From Setup, in the Quick Find box, enter **Roles**, and then select **Roles**.
2.  Just under the company name, click  **Add Role**. If the CEO role already exists, click  **Edit**.
3.  In the  **Label**  text box, enter CEO. The  **Role Name**  text box autopopulates with CEO.
4.  In the  **This role reports to**  text box, click the lookup icon    and click  **Select**  next to the name of your org. By choosing the name of the org in the  **This role reports to**  text box, we’re indicating that the CEO role is a top-level position in our role hierarchy and doesn't report to anyone.
5.  In the  **Role Name as displayed on reports**  text box, enter CEO. This text is used in reports to indicate the name of a role. Since a long role name, like Vice President of Product Development, takes extra space in your report columns, we recommend using a short but readable abbreviation.
6.  Leave any other options, such as  **Opportunity Access**, set to their defaults, and save.
7.  Now that you’ve created a role, you can assign the appropriate user to it. Click  **CEO**, and on the CEO role detail page, click  **Assign Users to Role**.
8.  In the  **Available Users**  drop-down list, select All Unassigned.
9.  Choose a user from the list, and click  **Add**  to move her to the  **Selected Users for CEO**  list, then save.

### Sharing Rules

#### Extend Access with Sharing Rules

Depending on the group member types available in your org, public groups can be a combination of:
-   individual users
-   roles
-   roles and subordinates
-   territories
-   territories and subordinates
-   other public groups

#### Define a Public Group

1.  From Setup, in the Quick Find, enter  **Public Groups**, and then select  **Public Groups**.
2.  Click  **New**. 
3.  Give your group a label. The  **Group Name**  text box populates automatically when you click it. This is the unique name used by the API and managed packages.
4.  In the  **Search**  drop-down list, choose from which individual users, other groups, or roles you’ll select users, and whether their subordinates are included. You can include a combination of member types in your public groups.
5.  In the  **Available Members**  list, select users, then click  **Add**.
6.  Click  **Save**.

#### Define a Sharing Rule

1.  From Setup, in the Quick Find box, enter  **Sharing Settings**, and then select  **Sharing Settings**. This is the same page used to define org-wide defaults.
2.  In the  **Manage sharing settings for**  drop-down list, choose the object for which to create the sharing rule. Choosing an object in this drop-down list allows you to focus in on the org-wide defaults and sharing rules for a single object at a time rather than looking at all of them in a long page—a useful thing if you've got a large org with multiple custom objects.
3.  In the Sharing Rules area, click  **New**  and give your rule a label. The  **Rule Name**  text box populates automatically when you click it.
4.  For the rule type, you can choose whether the sharing rule is based on the owner or based on criteria that records must match to be included. For this sharing rule, select  **Based on record owner**.
5.  For  **Select which records to be shared**, select a category from the first dropdown list, and a set of users from the second dropdown list or lookup field.
6.  For  **Select users to share with**, specify the users who get access to the data.
7.  Select a sharing access setting.
8.  Click  **Save**.



### Manual Sharing

1. Go to the record you want to share.
2. Open the record.
3. Click the drop down arrow on the top right corner.
4. Click **Sharing** and Select the User to which you want to share the rule
5. Set Access level to the user.
6. Selected Record will be shared with selected User.