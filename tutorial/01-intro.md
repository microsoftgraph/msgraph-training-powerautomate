<!-- markdownlint-disable MD002 MD041 -->

There are more than 230 out of box connectors for Microsoft Power Automate. Many of these connectors use the Microsoft Graph to communicate with specific endpoints of Microsoft products. Furthermore, there are other scenarios where we may need to call the Microsoft Graph directly from Power Automate using basic building blocks of the service, since there is no connector that communicates directly with the Microsoft Graph to cover the entire API.

In addition to addressing scenarios for calling the Microsoft Graph directly, a number of Microsoft Graph API endpoints only support [delegated permissions](https://docs.microsoft.com/graph/permissions-reference). The HTTP connector in Microsoft Power Automate enables very flexible integrations, including calling the Microsoft Graph. However, the HTTP connector lacks the capability of caching a user's credentials to enable specific delegated permission scenarios. In these cases, a custom connector can be created to provide a wrapper around the Microsoft Graph API and enable consuming the API with delegated permissions.

This lab covers both of the scenarios above. First, you will create a custom connector to enable integrations with Microsoft Graph which require [delegated permissions](https://docs.microsoft.com/graph/permissions-reference). Second, you will use the [$batch request endpoint](https://docs.microsoft.com/graph/json-batching), to provide access to the full power of the Microsoft Graph while using the delegated permissions that require an app to have a "signed-in" user present.

> [!NOTE]
> This is a tutorial on creating a custom connector for use in Microsoft Power Automate and Azure Logic Apps. This tutorial assumes you have read the [custom connector overview](https://docs.microsoft.com/connectors/custom-connectors/) to understand the process.

## Prerequisites

To complete this exercise in this post you will need the following:

- Administrator access to an Office 365 tenancy. If you do not have one, visit the [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) to sign up of a FREE developer tenant.
- Access to [Microsoft Power Automate](https://flow.microsoft.com/).

## Feedback

Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-powerautomate).
