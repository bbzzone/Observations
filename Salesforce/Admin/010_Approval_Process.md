# Approval Process

- An approval process is an automated process.
- It is implemented to approve records.
- We can specifies the steps those are necessary for approval.
- It allows steps to apply to all records or just records that have certain attributes.
- In approval process we can also define who will be approving at each step.
- Approver can take steps that when a record is approved, rejected or recalled.



In **Login Access Policies** (quick find) you can set administrator to be logged in as any user. And also in **session management** remove *Force relogin after Login-As-User*.



1. From quick find box search **Approval Process** and click on it.
2. Select the object for which you want to **Manage Approval Processes for**.
3. Now select **Create New Approval Process** and **Use Standard Setup Wizard**.
4. Set Process name and Unique name and then click next.
5. One can use **Criteria** or **Formula Field**.
6. Select the **Approver** Role in the **Next Automated Approver Determined By** picklist. Suppose Records Owners have different Managers than approval request will automatically be sent to Record owners Manager.
7. **Approver Field of Opportunity owner** is used to set approver user. Suppose we have a record owned by User A and now if this option is selected Manager of logged in user will be the approver, which doesn't make sense. We need manager of record owner to be the approver that's why we need to check this.
8. Set Record Editability Properties, whether **Record Owner** can edit field while approval request is in process.
9. On the next page select an email template for **Approver** to notify them that an **Approval Request** is assigned to them.
10. Add fields to **Approval Page** (It is a page where Approver will approve or reject a request). Selected fields will be displayed on Approval Page.
11. Check **Approval Page history information** if you want to know who submitted the approval request and who has already approved the request. Click **Next**
12. Select the **Initial Submitter**. (The person who submitter the approval request => Most of the times it will be Record Owner but for a shared record it may be different)
13. You can also check **Allow submitters to recall approval requests**, if you want submitters to recall approval requests. Click **Save** now to create Approval Process.
14. Click **Activate** to activate the Approval process.



Approval Process is created. Now we need to attach following things with:-

- [**Initial Submission Action**](#Setting-Initial-Submission-Actions) (Like locking the record until approval request is not completed or modifying a field to tell users that Approval request is pending or under process).

- [**Approval Steps**](#Approval-Steps) => Process which will be followed during Approval Process.
- **Rejection Actions** (Similar to Submission Actions but fire only when Approval request is Rejected).
- **Recall Actions** => Actions to do when Approval request is Recalled.



## Setting Initial Submission Actions

1. On saving if you open the approval request you just created, you can associate **Tasks, Email Alert, Field Update, Outbound Message** with it.
2. Click on **Add New** on Initial Submission Actions and add desired action. One can add multiple actions too.
3. For now take an example of field update.
4. On Field Update Page provide Name and Unique Name to the field.
5. Now from the dropdown menu select the Field you want to update.
6. In the **Specify New Value** section select the Value you want to give for updating the field.
7. Click **Save** and from now while starting any approval process for that object this field will be updated.



## Approval Steps

These are the steps which will decide the flow of the approval process.

1. Click **New Approval Step**
2. Specify Name and Step Number and click **Next**
3. On the next page set the **criteria** for step to be executed.
4. You can select whether all approval requests will have to go through this step or only specific (by setting criteria).
5. Select the Assigned Approver (Who will be assigned this approval step)
   - You can give right to user to select the approver manually.
   - You can also automatically set the approver.
6. Now you can **Save** the approval step.
7. **If the criteria is satisfied then this approval request will fire otherwise approval request will be *Approved automatically***.



You can have multiple Approval Steps depending on the requirement of the task.

