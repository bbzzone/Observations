# Duplicate and Matching Rule

- Duplicate rule *prevents creation of duplicate recrods. It gives warning or block record creation*
- In matching rule we need to set criteria for Duplicate checks.



## Duplicate Rule

This we can find in Setup page by searching in quick find box.

1. Go to quick find box and search for **Duplicate Rule**.
2. Click **New Rule**. 
3. Add **Rule Name** and description.
4. Now the important option is **Record-level Security** => If we select Enforce Sharing Rules, it will apply duplication check on **records which user has access to**. If we set bypass sharing rules it will run duplicate check on **all records**.
5. Now select **Actions** when we create a new record. If we want to Allow duplicate record with warning we can set allow, alert, report. If we want to block duplicate record creation. This will work on edit too.
6. Set Alert Text for warning or error.
7. Set [Matching rule](#Matching-Rule) like which field we want to compare for finding duplicacy in records.
8. Select New Matching Rule or select a matching rule that is available at the time. (Save Duplicate Rule on Prompt)
9. **Condition** will decide whether matching Rule will fire or not.



## Matching Rule

1. You can Navigate to Matching Rule by going to quick find box.
2. Click on **New Rule**
3. Then select the **Object** we need matching Rule on.
4. On next page Enter **Rule Name** and Description
5. In the **Mathcing Criteria** section select the field on which we want to compare 2 objects and save the matching Rule
6. After saving the matching Rule activate the matching Rule.



# Activities

These are the 4 options available under activities

- Task
- Event
- Call
- Email

These are various activities which are useful when connecting with clients or other org members to log or to remind or assign someone a task.

For these options to be enabled we need to go to particular object and in the **Details** we need to click **Edit** and from there we need to check **Allow Activities** from the **Optional Features** Section.

After enabling this, **Activity component** will be automatically visible on Record Page. If for some reason Activities component is not visible you can add it by modifying **Record Lightning Page**.



# Feed Tracking

Feed tracking enabled changes in selected fields and these changes are shown in Chatter component. It shows old value, new value and the user who changed those.

1. In Quick find box Search Feed Tracking.
2. Select the object on which you want to enable feed tracking.
3. Now check the box **Enable Feed Tracking**.
4. After that select the fields we want to track and then **Save**.
5. Now we need to go to Object and add **Chatter component** to Record Page Layout if it is not available by default.
6. Now on changing any tracked field, it will show a message in chatter component.



**Chatter Components are specific to specific records**.



# Field History Tracking

Like Feed Tracking it shows the changes that happened in the selected fields. It shows Previous value, new value and the person who changed the value. **But unlike Feed tracking, chages are shown in the Histroy related field.**

1. To enable Field History Tracking on a particular field we need to navigate to object manager.
2. Then select the object and go to *Fields & Relationships*.
3. Click on the *Set History Tracking* in the top right corner of the page.
4. On the selection page we have to select the fields on which we want to enable tracking.
   - **We can't track new and old values in *text-area long* and *text-area rich*, we can only track changes only on these fields**.
5. Now to make it visible we need to go to object detail page and then edit the object to check **Track Field History**. That will make sure that **History Related List** will be visible in Page Layout.
6. Now go to **Page Layout** and add *History Related List* in the Page Layout.
7. Any changes to the selected fields will reflect on record page's **Related tab**.



# View Setup Audit Trails

This shows a list of changes cone by users in the org in different components. One can download changes done in past 6 months.

**To view Setup Audit Trails** we simply need to search this in quick find box and on clicking on it, it will show all the changes that were made on the org.