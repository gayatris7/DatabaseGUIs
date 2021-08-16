# Database GUIs - Building Admin Panels with Low-Code

Low-code platform gives teams a quick and easy solution to create interactive admin panels and other database guis that are more powerful and robust than most CRUD interfaces.

### What problem is it solving?
There are times when there is dependcy on database manager/administrator to delve into the database because the ready to use admin tool does not support operations that may be required. Say you have just launched your SaaS tool online and to understand the kind of users signing up, you need to get the information captured by the developer into the database because you don't have direct access to read it or comprehend it. While this may not be a big problem when you are at a very early stage but as the project grows having developers or systems administrators log into the database to fetch you some information or to make some changes to settings it not the most viable option - 

1. It takes up valuable time of developers or the system admins to do the job that can otherwise be done by semi-technical people 
2. You cannot give access to just anyone. Any database call needs to be executed with a lot of caution as the action is on live data.

**Why admin panels?** Admin panels are vital internal tools to securely allow users to read the information (for example sales lead information, username, user email, signup date, sessions, pages visited and so on) and then take some action with the information. Admin panels also help control user/access permissions, so only specific users can read, update or delete records. An added advantage comes when you are able to configure multiple sources of truth to a single admin panel and then user APIs to take action in an external tool, for example sending emails to leads using SendGrid, or reminders to sales representatives over Slack.

Small and medium sized companies with small dev teams always have their plates full with their product, website, or customer facing requirements, making it difficult to justify investing time into coding and creating admin panels that are to be used internally by the business teams, something the customers will never see.

Low-code platform [DronaHQ](https://www.dronahq.com/?utm_source=github&utm_medium=mongodb-admin-panel) give a fast way to build custom admin tools on top of existing databases and apps in under minutes. With native integration to databases, database administrators can visually create frontends and share the tool with their teams in a click. In this article, I share the step by step process of creating a custom **MongoDB Admin Panel on DronaHQ in under 30 minutes** . We will be integrating with the customer database present in MongoDB to notify the admin or sales managers on Slack every time a new customer is added to the database.

### DronaHQ – MongoDB Integration
For this example, you need to be signed in to your [DronaHQ accounts](https://studio.dronahq.com/login.aspx). If you are DronaHQ user, you can follow along with us here.

![DronaHQ API Connectors](https://www.dronahq.com/wp-content/uploads/2021/07/image16-768x445.png)

First, head over to the panel menu on the left and click on “ + Connectors.” A list of connectors will pop up. Under the connectors menu select “MongoDB.”

![DronaHQ API Integration](https://www.dronahq.com/wp-content/uploads/2021/07/image12-768x335.png)

#### Step 1: Entering Basic Details for the Database Connector

Enter a name for the connector that you would like to use. This will be used to refer to the connector while you are building the app.

After you are done adding a name and description for the connector (I chose to write the purpose of this connector as my description), click on “Continue.”

![MongoDB Integration DronaHQ](https://www.dronahq.com/wp-content/uploads/2021/07/image14-768x364.png)

#### Step 2: Adding the Connection String from MongoDB

Under the Connection Strings Section, click on “Continue.” It will prompt you to “Test your Connection.” Click on “Test.” You will be asked to select the “Environment” in which the Connector should be available. You can choose between Dev, Beta, and Prod. 

I will select Prod as I  need the connector to work in the live app that the customer support team will use. 

To get the Connection String, head back to your MongoDB database. In my app, I am using MongoDB Atlas. Head over to Clusters > then click on Connect. 

![MongoDB Atlas](https://www.dronahq.com/wp-content/uploads/2021/07/image7-768x363.png)

#### Step 3: Configuring the Database and Testing

Click on Connect your Application to get the Configuration link in the next step.

![MongoDB API Configuration](https://www.dronahq.com/wp-content/uploads/2021/07/image2.png)

Here’s the process by MongoDB on [how to get the configuration link and use it in your apps](https://docs.mongodb.com/guides/cloud/connectionstring/).

![image](https://user-images.githubusercontent.com/83713635/129563786-8e52ec6d-2a12-4333-ad1b-27ab231caac6.png)

Once you have this link, head back to DronaHQ and enter the copied link into the box. The subsequent field will auto-populate. Click on “Submit” and proceed to 

![MongoDB Integration DronaHQ](https://user-images.githubusercontent.com/83713635/129563918-27b02146-78ac-4d6b-bc4a-9f98744097b1.png)

Once these configurations are done, you need to Test the request and connection. If the authentication is successful, you will get the response accordingly. You can now click Continue to Finish and Save your configuration. You will notice the connector is added to the list. 

#### Step 4: Adding query to the database 

This is an important step. 

Here you configure the [various actions MongoDB](https://www.dronahq.com/connect-mongodb/?utm_source=github&utm_medium=mongodb-admin-panel) supports. For example, if your action is Find the parameters would be Filter, projection, sort, limit, and skip, and you can use this to read the data. If you choose InsertOne as an action, the parameter will change to Insert as Key: Value string to write to the database. Once you have assigned the necessary values, you can Run the query. The response can be seen as per the parameters given.

![image](https://user-images.githubusercontent.com/83713635/129564163-3efbd142-3d81-4c5a-9283-8688a227994c.png)

![MongoDB IntegrationDronaHQ](https://www.dronahq.com/wp-content/uploads/2021/07/image10-768x370.png)

Next, you need to Enter a service name, the collection, and the action. 

Let’s name it “FindData.” For our customer portal use case, I will select the “Find” action. Under the Collection dropdown menu, you will be able to see the databases in your cluster. Pick the one you want to use in your app.

Once you are done, click on **RUN** on the top right corner. You will be able to see the first 10 rows. 

![MongoDB Integration DronaHQ](https://www.dronahq.com/wp-content/uploads/2021/07/image17-768x219.png) 

Note: Only the last row will be saved. If the final row has Name, Email, Contact, Address, Company fields, only those will reflect in your app later (jump to see)

![MongoDB Integration DronaHQ](https://www.dronahq.com/wp-content/uploads/2021/07/image18-768x338.png)

Click on “Save” to proceed to the next step. 

You can now view the queries you saved and use in your apps later under your specific connector under Custom Database connectors.

![MongoDB Connector DronaHQ](https://www.dronahq.com/wp-content/uploads/2021/07/image1-768x163.png)

###Building Admin Panel

#### Step 1: Building an app from scratch
On the left menu, click on “Apps,” and then click on the “ + “ sign to start building your app from scratch.
Note: At this step, you are very likely to find a relevant app template (like Customer Support Tool, Sales Dashboard, Customer Feedback, Refund Tool, and so on) under the “TEMPLATES” heading, but in this article, we will be making the app from scratch. If you already have an app on DronaHQ, you can use the connectors we just configured in those apps too. 

![Building Admin Panel](https://user-images.githubusercontent.com/83713635/129564538-24af5555-a6a5-4048-8f03-5ed15ea607d0.png)

Let’s give our app a name and a description.

![MongoDB Admin Panel](https://www.dronahq.com/wp-content/uploads/2021/07/image20-768x369.png) 

#### Step 2: Creating the Screens/UI 
The app will open up in a new tab like in the image below. To make things faster, I will pick a template screen from the Screen Marketplace. To select an app screen, click on the “ + Add.” 

![Admin Panel UI](https://www.dronahq.com/wp-content/uploads/2021/07/image15-768x478.png) 

You can browse through a list of Screens, Menus, Pop-ups, Trays. For this app, let’s go with the Two Column with Tabs screen.

![Screen Marketplace](https://www.dronahq.com/wp-content/uploads/2021/07/image6-768x370.png)

You will see the screen is added to your app: 

![Admin Panel UI](https://www.dronahq.com/wp-content/uploads/2021/07/image13-768x358.png) 

#### Step 3: Using MongoDB connectors in App
For this, I can use the table grid control. 

To do that, we click on the Table Grid Control, then click on the database icon as shown below in the image.  

![MongoDB Admin Panel](https://www.dronahq.com/wp-content/uploads/2021/07/image11-768x355.png)

This will pop open a menu on the right of the screen that displays the various methods you can bind your data to the Table Grid control.

Click on the Database icon and head over to add the Custom Function. Here is what the formula should look like: 

BINDAPI([MongoDB.result.rows.Name,MongoDB.result.rows.Email,MongoDB.result.rows.Phone,MongoDB.result.rows.Company,MongoDB.result.rows.Address,MongoDB.result.rows.City,MongoDB.result.rows.ZIP,MongoDB.result.rows.Country])

You can use a similar formula for all other databases like orders list, payment details, etc.

This brings us to the end of part 1 of the app-building process. In part 2, I will be 

- Adding and updating data from the MongoDB GUI 
- Delete record in the MongoDB Database

DronaHQ has a growing library of native integrations to let you pull in and combine data from different sources, including your databases and APIs.  So if you want to enrich your MongoDB data with some data from another source, you can do so with a ready connector.
