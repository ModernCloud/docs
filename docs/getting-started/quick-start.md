We'll build a simple, production-ready CRUD application in just a few minutes, right inside your browser.

First, sign up to Modern Cloud.

Once you are logged into the app, you'll see your endpoints, functions, and all other resources, including your DynamoDB tables, on the left-hand side pane. We'll start by creating our table. Expand the DynamoDB menu item on the left and click **New Table**.

<div style="text-align: center; margin: 30px 0;">
<img src="/assets/create-table.png" width="50%" />
</div>

You should see the following pop-up:

<div style="text-align: center; margin: 30px 0;">
<img src="/assets/create-table-popup.png" width="70%" />
</div>

For the *Name* enter **users**, and for the *Hash Key*, enter **UserID**. Leave the remaining as is and click Create. We now have our DynamoDB table ready which we can use to insert and retrieve data from our lambda endpoints.

Now, it's time to create our write endpoint. Expand the Endpoints menu item on the left and click **new endpoint**.

<div style="text-align: center; margin: 30px 0;">
<img src="/assets/create-endpoint.png" width="50%" />
</div>

You should see the following pop-up:

<div style="text-align: center; margin: 30px 0;">
<img src="/assets/create-endpoint-popup.png" width="70%" />
</div>

Enter the details for our new write endpoint, a user-friendly name such as **Create User** and select **POST** as the method. Finally, for the path, enter **users**. Then, click Create.

We are now ready to write our code. Click on the newly created endpoint on the left menu, and the editor should open as a new tab. Copy and paste the following code:

```javascript linenums="1"
const AWS = require("aws-sdk");
const dbClient = new AWS.DynamoDB.DocumentClient({apiVersion: '2012-08-10'});
 
exports.handler = async (event) => {
  let params = JSON.parse(event.body);
  await dbClient.put({
    TableName: 'users',
    Item: {
      email: params.email,
      name: params.name
    }
  }).promise();
  return {
    statusCode: 200,
    body: JSON.stringify({})
  }
};
```

Because we are using a node-js package, we need to make sure the package is specificed. On the right pane, select **Packages**. Click **Add Package** button and search for **aws-sdk**. The latest stable version will be automatically entered but you can modify that if you want to use a different version.

<div style="text-align: center; margin: 30px 0;">
<img src="/assets/add-package.png" width="60%" />
</div>

Now, on the right pane, select **Deployment** from the drop-down menu at the top right corner. Then, click the deploy button under dev section. After a few seconds, your endpoint should be ready for testing!

You can click on the generated link to access your endpoint and start testing!

Let's quickly explore a few more things. On the top-right corner, from the drop-down menu, select **Logs**. You can easily see your logs here. By selecting **Overview**, and you can see all the basic metrics associated with your endpoint.

We are always eager to hear your feedback! Reach out to us via contact@moderncloud.io and say hello!