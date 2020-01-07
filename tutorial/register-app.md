<!-- markdownlint-disable MD002 MD041 -->

In this exercise, you will create a new Azure Active Directory Application which will be used to provide the delegated permissions for the custom connector.

Open a browser and navigate to [Azure Active Directory admin center](https://aad.portal.azure.com). Choose the **Azure Active Directory** link in the left navigation menu, then choose the **App registrations** entry in the **Manage** section of the **Azure Active Directory** blade.

![A screen shot of the Azure Active Directory blade in the Azure Active Directory admin center](./images/app-reg1.png)

Choose the **New application registration** menu item at the top of the **App Registrations** blade.

![A screen shot of the App Registrations blade in the Azure Active Directory admin center](./images/app-reg2.png)

Enter `MS Graph Batch App` in the **Name** field, and `https://localhost.com/$batch` in the **Sign-on URL** field and choose **Create**.

![A screen shot of the create form for a new app registration in the Azure Active Directory admin center](./images/app-reg3.png)

On the **MS Graph Batch App** page, copy the **Application ID** of the application. You'll need this in the next exercise.

![A screen shot of the registered application page](./images/app-reg4.png)

Choose the **Settings** gear under the application name, then choose the **Required Permissions** menu item in the Settings blade. Choose **Add** at the top of the **Required Permissions** blade.

![A screen shot of the Required permissions blade](./images/app-perms1.png)

Choose the **Select an API** option in the **Add API access** blade, then select the **Microsoft Graph** item and choose **Select** at the bottom of the blade.

![A screen shot of the Select an API blade](./images/app-perms2.png)

On the **Enable Access** blade, scroll down to the **Delegated Permissions** section. Select the **Read and write all groups** delegated permission, then choose **Select** at the bottom of the blade. Choose **Done** at the bottom of the **Add API access** blade.

 ![A screen shot of the Enable Access blade](./images/app-perms3.png)

Choose the **Keys** menu item on the **Settings** blade. Enter `forever` in the **Key description** and select **Never expires** from the **Duration** drop down menu. Choose **Save** at the top of the **Keys** blade. Copy the key value for the new key. You'll need this in the next exercise.

![A screen shot of the Keys blade](./images/app-key1.png)

> [!IMPORTANT]
> This step is critical as the key will not be accessible once you close this blade. Save this key to a text editor for use in upcoming exercises.

To enable management of additional services accessible via the Microsoft Graph, including Teams properties, you would need to select additional, appropriate scopes to enable managing specific services. For example, to extend our solution to enable creating OneNote Notebooks or Planner plans, buckets and tasks you would need to add the required permission scopes for the relevant APIs.
