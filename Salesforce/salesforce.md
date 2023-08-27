# Salesforce

There are 2 type of roles in salesforce. **Salesforce admin** and **Salesforce Developer**.

There are 2 approaches to develop in salesforce

1. Point and Click Tools (Declarative approach)
2. Programmatic approach.

It is always better to know both approaches. There are various languages used in salesforce.

## Languages

There are different types of languages used in salesforce. The main one used is **APEX** which is very similar to JAVA.

1. **APEX** will be used to write business functionality of business logic. Salesforce is completely based on MVC (Model View Controller) architecture where Controller contributes, simply means APEX is used to write Controllers. 
2. **Visualforce** is a markup language which is used to create UI in salesforce. We can't create Lightning UI with the help of Visualforce.
3. **Lightning web Components** was included in salesforce in 2016. Components in Salesforce were getting too outdated, so they created a new library like react to improve used interface with mobile responsiveness which is now called as Lightning framework. With the help of Lightning we can create UI as well as some part of Controller with the help of javascript.



Salesforce has many important things which are helpful while understanding the salesforce paltform. Few of those are-

- **OOPS in APEX** =>If someone is familiar with JAVA, he probably will be familiar with OOPS already. OOPS concepts like Abstraction using abstract classes and interfaces are helpful.
- **SOQL/SOSL** => SOQL is Salesforce Object Query language which is very similar to SQL and SOSL is Salesforce Object Search Language which is used to Search for some keywords in Salesforce.
- **DML(Data Manupolation Language) and Database Class** =>When we need to get something from the database or read something from the database, we use SOQL or SOSL. But when we need to put something in the database or need to change something inside database(like delete, insert, update) we will use **Database Class**. 
- **APEX Triggers** => This is one of the most important topics on Salesforce developmentlike . Triggers are used to automate things in Salesforce. (One should use declarative approach over Programatic approach when possible). We can use *Process Builders, Workflows, Lightning tools for declarative approach*. 
- **APEX Testing** => If one is trying to deploy code from his sandbox to production it is compulsory to write test classes. These test classes are basically test functionality of APEX classes. In this we create test classes and use Unit Testing to test our APEX classes. Testing is automated using Selenium.
- **Governor Limits and Batch APEX** => Salesforce has put limits on various operations like number of records that can be queried, inserted, updated or deleted in a single transaction, limit on number of records that can be processed by a single Apex transaction. Limit on number of CPU time and heap space that can be utilized by a single transaction. If transactions exceeds any of limits provided by Salesforce, it will throw a governor limit exception. **Batch APEX** allows you to proccess data in smaller chunks, which helps to avoid governor limit exceptions. It works in 3 steps *start, execute and finish*. Batch APEX runs in background (asynchronously) So it doesn't block the user interface.
- **APIs and Integrations** => It is another important part of salesforce. If we want to connect salesforce platform with some other application or another platform we use APIs and integrate them with salesforce.
- **Deployment Methodologies**



**PD 1** is a certification for salesforce which can be very useful in a resume. This acts as a validation that you are good salesforce development.
