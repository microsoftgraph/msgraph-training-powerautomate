<!-- markdownlint-disable MD002 MD041 -->

In this exercise, you will create a new Azure Active Directory Application which will be used to provide the delegated permissions for the custom connector.

Open a browser and navigate to [Azure Active Directory admin center](https://aad.portal.azure.com). Choose the **Azure Active Directory** link in the left navigation menu, then choose the **App registrations** entry in the **Manage** section of the **Azure Active Directory** blade.

![A screen shot of the Azure Active Directory blade in the Azure Active Directory admin center](./images/app-reg-preview1.png)

Choose the **New registration** menu item at the top of the **App Registrations** blade.

![A screen shot of the App Registrations blade in the Azure Active Directory admin center](./images/app-reg-preview2.png)

Enter `MS Graph Batch App` in the **Name** field. In the **Supported account types** section, select **Accounts in any organizational directory**. Leave the **Redirect URI** section blank and choose **Register**.

![A screen shot of the Register an application blade in the Azure Active Directory admin center](./images/app-reg-preview3.png)

On the **MS Graph Batch App** blade, copy the **Application (client) ID**. You'll need this in the next exercise.

![A screen shot of the registered application page](./images/app-reg-preview4.png)

Choose the **API permissions** entry in the **Manage** section of the **MS Graph Batch App** blade. Choose **Add a permission** under **API permissions**.

![A screen shot of the API permissions blade](./images/app-perms-preview1.png)

In the **Request API permissions** blade, choose the **Microsoft Graph**, then choose **Delegated permissions**. Search for `group`, then select the **Read and write all groups** delegated permission. Choose **Add permissions** at the bottom of the blade.

 ![A screen shot of the Request API permissions blade](./images/app-perms-preview2.png)

Choose the **Certificates and secrets** entry in the **Manage** section of the **MS Graph Batch App** blade, then choose **New client secret**. Enter `forever` in the **Description** and select **Never** under **Expires**. Choose **Add**.

![A screen shot of the Certificate and secrets blade](./images/app-key-preview1.png)

Copy the key value for the new key. You'll need this in the next exercise.

![A screen shot of the new client secret](./images/app-key-preview2.png)

> [!IMPORTANT]
> This step is critical as the key will not be accessible once you close this blade. Save this key to a text editor for use in upcoming exercises.

To enable management of additional services accessible via the Microsoft Graph, including Teams properties, you would need to select additional, appropriate scopes to enable managing specific services. For example, to extend our solution to enable creating OneNote Notebooks or Planner plans, buckets and tasks you would need to add the required permission scopes for the relevant APIs.
