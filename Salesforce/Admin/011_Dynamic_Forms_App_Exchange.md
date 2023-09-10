# Dynamic Forms

These are some custom fields which are added into a section inside **Lightning Page Builder** in **Record Lighting Page**.

1. Go to **Lightning app builder** or go to a record page and click on gear icon then **Edit Page**.
2. Add some sections.
3. From the left pane add some fields to the section you created before.
4. Save and activate the record.
5. Now this is our **Dynamic Form**.



# Object Specific Actions

When we open a record there are some buttons which are different for different object on the record page. These are also called quick actions or **Object Specific Actions**. 

To create these actions

1. Navigate to Object you want to add these actions on from Object Manager.
2. From there click on **Button, Links and Actions**.
3. Click on **New Action** from top right corner.
4. On the next Page select **Action type**.
5. Select the target object which will be affected by that action.
6. Add label which will be the button name on record page and click save.
7. If you selected create new record, you will have to add a layout where you need to select the fields which you want to use while creating the record.
8. We can also set predefined values for the fields when they are created using actions.
9. Now Action is created but it is not added to page layout.
10. Go to the page layout and Select **Mobile & Lightning Actions** and add the button to page layout.



This can be used to **create fields** in Object which have a relation to the current Object or are child of current Object. Advantage of this is that Relationship field will be prepopulated and we won't have to enter the value for that field.



# Global Action

These type of actions will be available for whole org.

**To create global action**

1. We need to navigate to **Global Actions**
2. Click on **Create New Action**.
3. Select the action you want to trigger
4. Accordingly select other fields.
5. After **saving** the record create the layout and save it.
6. Now navigate to **Publisher Layout** from quick find.
7. **Create or Edit** the layout and add the Global action to the layout.
8. On saving  action will display in global actions list.



# Related List Single

Suppose we have a class object and it has 10 Student children. Usually when i open a single student record i won't see other students which have same class. But this one can achieve with the help of related list single.

1. **Related List Single** is a component in **Lightning App Builder**
2. Open **Record Lightning Page** 
3. From left pane add Related List Single Component.
4. Now after clicking on the Component it will open a menu in right pane.
5. From there select the parent object and it's children we want to see.
6. Save and Activate the Layout.