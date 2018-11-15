<!-- markdownlint-disable MD002 MD041 -->

The Flow you created in the previous exercise uses the `$batch` API to make two individual requests to the Microsoft Graph. Calling the `$batch` endpoint this way provides some benefit and flexibility, but the true power of the `$batch` endpoint comes when executing multiple requests to Microsoft Graph in a single `$batch` call. In this exercise, you will extend the example of creating a Unified Group and associating a Team to include creating multiple default Channels for the Team in a single `$batch` request.

Open [Microsoft Flow](https://flow.microsoft.com) in your browser and sign in with your Office 365 tenant administrator account. Select the Flow you created in the previous step and choose **Edit**.

Choose **New step** and type `Batch` in the search box. Add the **MS Graph Batch Connector** action. Choose the ellipsis and rename this action to `Batch POST-channels`.

Add the following code into the **body** text box of the action.

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Marketing Collateral",
        "description": "Marketing collateral and documentation."
      }
    },
    {
      "id": 2,
      "dependsOn": [
        "1"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Vendor Contracts",
        "description": "Vendor documents, contracts, agreements and schedules."
      }
    },
    {
      "id": 3,
      "dependsOn": [
        "2"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "General Client Agreements",
        "description": "General Client documents and agreements."
      }
    }
  ]
}
```

Notice the three requests above are using the [dependsOn](https://developer.microsoft.com/en-us/graph/docs/concepts/json_batching#sequencing-requests-with-the-dependson-property) property to specify a sequence order, and each will execute a POST request to create a new channel in the new Team.

Select each instance of the `REPLACE` placeholder, then select **Expression** in the dynamic content pane. Add the following formula into the **Expression**.

```js
body('Batch_PUT-team').responses[0].body.id
```

![A screen shot of the expression in the dynamic content pane](./images/flow-channel1.png)

Choose **Save**, then choose **Test** to execute the Flow. Select the **I'll perform the trigger** action radio button, then choose **Test**. Enter a unique group name in the **Name** field without spaces, and choose **Run flow** to execute the Flow.

![A screen shot of the Run flow dialog](./images/flow-team4.png)

Once the Flow starts, choose the **See flow run activity link**, then choose the running Flow to see the activity log.

When the Flow completes, the final output for the `Batch POST-channels` action has a 201 HTTP Status response for each Channel created.

![A screen shot of the successful flow activity log](./images/flow-channel2.png)

Finally, open the [Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) again and paste the following into the query text box.

```text
https://graph.microsoft.com/beta/teams/GROUP_ID/channels
```

Replace the `GROUP_ID` with your new Group's `id` property and click **Run Query**.

> [!TIP]
> You can find the `id` of the new Group by checking the `id` returned in the `Batch POST-groups` actions output in our Flow.

The query should return results similar to the image below with the default **General** channel and the three channels we created using our `$batch` action with 3 requests.

While the above `Batch POST-channels` action was implemented in this tutorial as a separate action, the calls to create the channels could have been added as additional calls in the `Batch PUT-team` action. This would have created the Team and all Channels in a single batch call. Give that a try on your own.

Finally, remember that [JSON Batching](https://developer.microsoft.com/en-us/graph/docs/concepts/json_batching) calls will return an HTTP status code for each request. In a production process, you may want to combine post processing of the results with an [`Apply to each`](https://docs.microsoft.com/en-us/flow/apply-to-each) action and validate each individual response has a 201 status code or compensate for any other status codes received.