Here's the converted Markdown content:

# Zendesk <> Braze Integration leveraging the same SMS

While Braze has some 2-way conversational abilities, there are use cases that require real human communication. Many of our customers leverage Zendesk for this, and we have seen an increase in requests to leverage the same number for both marketing and conversational use cases. Below is an example of how we can set this up.

## The general process:

1. When a user signals they need custom support, for example sending HELP, this will send an API call to Zendesk to open a ticket.
2. When an agent replies to the ticket, the response will be forwarded to Braze using an API-Triggered SMS message.
3. This will send two custom attributes - one with the ticket ID and one with ticket status = open
4. When a user replies, the contents of their SMS will be sent via API to Zendesk.
5. This will include the attribute ticket status = open and the ticket ID in the Webhook URL.
6. When an agent closes a ticket, notify Braze so that future SMS replies from the user are not sent to Zendesk.
7. This will send custom attribute ticket status = closed.
8. For this example, we have set up another API-Triggered Campaign that sends the user an SMS confirming the ticket is resolved; however, Zendesk can hit the User Track endpoint just as easily and follow these same steps.

## Setup:

Before beginning, create a basic authorization token in Zendesk to use in Braze. Similarly, create applicable API keys in the developer console of the Braze dashboard.

## Within Zendesk:

### Step Z.1: Create a Webhook

Within your developer console, navigate to webhooks:  
https://{{url}}.zendesk.com/admin/apps-integrations/webhooks/webhooks

Add in a new webhook endpoint for Braze’s [API-Triggered Delivery](https://www.braze.com/docs/api/endpoints/messaging/send_messages/post_send_triggered_campaigns/):

If you are using a user track endpoint for step 4, repeat this process with that API endpoint.

### Step Z.2: Create a trigger to forward agent replies to Braze

Next, navigate to triggers:  
https://{{url}}.zendesk.com/admin/objects-rules/rules/triggers

Create a new trigger:

- **Category:** Trigger a message
- **Under Conditions, select:**
  - Ticket>Comment is Present and requester can see comment so that the message is triggered whenever a new public comment is included in a ticket update
  - Ticket>Update via is not Web service (API) so that when a user sends a message from Braze, it is not forwarded back to their cell phone. Only messages coming from Zendesk will be forwarded.

- **Under Actions, select Notify by Webhook and choose the endpoint you just created. From there, we need to specify the body of the API call:**

```json
{
  "campaign_id": "{{YOUR_API_KEY}}",
  "recipients": [
    {
      "external_user_id": "{{ticket.requester.custom_fields.braze_id}}",
      "trigger_properties": {
        "msg_body": "{{ticket.latest_public_comment_html}}"
      },
      "attributes": {
        "zendesk_ticket": "{{ticket.id}}",
        "zendesk_ticket_open": "true"
      }
    }
  ]
}
```

Note your API key will come from Braze. Follow steps for the first campaign created in Step B.3.

### Step Z.3: Create a trigger to notify Braze when a ticket is closed

Set up an additional trigger in order to notify Braze when the ticket is closed:

- **Category:** Trigger a message
- **Under Conditions, select:**
  - Ticket>Ticket Status is changed to Solved

- **Under Actions, select Notify by Webhook and choose the second endpoint you just created. From there, we need to specify the body of the API call:**

```json
{
  "campaign_id": "{{YOUR_API_KEY}}",
  "recipients": [
    {
      "external_user_id": "{{ticket.requester.custom_fields.braze_id}}",
      "attributes": {
        "zendesk_ticket_open": "false"
      }
    }
  ]
}
```

Note your API key will come from Braze. This will come from the second API-triggered campaign created in Step B.3.

## Within Braze:

### Step B.1: Webhook to Zendesk for Ticket Creation

Set up a webhook campaign to create a keyword under the Help category to create a ticket in Zendesk:

In the webhook composer:

- **Webhook URL:** [https://{{url}}.zendesk.com/api/v2/tickets](https://{{url}}.zendesk.com/api/v2/tickets)
- **KVPs:**
  - Content-Type -> application/JSON
  - Authorization -> Bearer {{Token}}
- **Sample body:**

```json
{
  "ticket": {
    "subject": "Action Needed",
    "comment": {
      "body": "{{sms.${inbound_message_body}}}"
    },
    "requester": {
      "name": "{{${first_name}}} {{${last_name}}}"
    }
  }
}
```

