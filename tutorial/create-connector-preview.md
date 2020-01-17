<!-- markdownlint-disable MD002 MD041 -->

In this exercise, you will create a new custom connector which can be used in Power Automate or in Azure Logic Apps. The Open API definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.

Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com). Sign in with your Office 365 tenant administrator account. In the left-hand menu, expand **Data** and choose **Custom connectors**.

![A screen shot of the Custom connectors menu item in Microsoft Power Automate](./images/flow-conn1.png)

On the **Custom connectors** page choose the **New custom connector** link in the top right, then select the **Import an OpenAPI file** item in the drop-down menu. Enter `MS Graph Batch Connector` in the **Connector name** text box. Choose **Import** button to upload the Open API file. Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created. Choose **Continue** to upload the OpenAPI file.

 ![A screen shot of the Create custom connector dialog](./images/flow-conn3.png)

On the connector configuration page, choose the **Security** link in the navigation menu. Fill in the fields as follows.

- **Choose what authentication is implemented by your API**: `OAuth 2.0`
- **Identity Provider**: `Azure Active Directory`
- **Client id**: the application ID you created in the previous exercise
- **Client secret**: the key you created in the previous exercise
- **Login url**: `https://login.windows.net`
- **Tenant ID**: `common`
- **Resource URL**: `https://graph.microsoft.com` (no trailing /)
- **Scope**: Leave blank

Choose **Create Connector** on the top-right

![A screen shot of the Security tab in the connector configuration](./images/flow-conn4.png)

After the connector has been created, copy the generated **Redirect URL**.

![A screen shot of the generated Redirect URL](./images/flow-conn5.png)

Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise. Select **Overview** on the **MS Graph Batch App** blade, then select **Add a Redirect URI**. Add the **Redirect URL** you copied in the **Redirect URI** field and choose **Save**.

![A screen shot of the Reply URLs blade in the Azure portal](./images/flow-conn-preview6.png)
