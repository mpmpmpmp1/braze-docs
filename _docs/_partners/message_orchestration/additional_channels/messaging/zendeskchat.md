---
nav_title: Zendesk_Chat
article_title: Zendesk_Chat
description: "Learn how to integrate Zendesk with Braze"
alias: /partners/zendesk_chat/
page_type: partner
search_tag: Partner

---

# Zendesk

> Zendesk’s integration enables you to leverage webhooks from each platform to set up a two-way conversational SMS pipeline.

When a user requests support, a ticket is created in Zendesk. Agent responses are forwarded to Braze via an API-triggered SMS campaign, and user replies are sent back to Zendesk. 


## Prerequisites

Before you start, you'll need the following:

| Prerequisite             | Description                                                               |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| A Zendesk account            | A Zendesk account is required to take advantage of this partnership.|
| A Zendesk Basic Authorization Token | A Zendesk Basic Authorization Token will be used to make an outbound webhook request from Braze to Zendesk.|
| A Braze REST API Key         | A Braze REST API key with campaigns.trigger.send permissions. This can be created in the Braze dashboard from Settings > API Keys.|

## Use cases

- Enhance customer support efficiency by combining Braze’s SMS capabilities with Zendesk’s live agent responses, ensuring that user inquiries are addressed promptly by human support.


## Integrating Zendesk

### Step 1: Create a Webhook in Zendesk

1. First, within the Zendesk developer console, navigate to webhooks: https://{{url}}.zendesk.com/admin/apps-integrations/webhooks/webhooks
2. Under **Create Webhook**, select **Trigger or automation**.
3. In the **Endpoint URL** textbox, add the **campaign/trigger/send** endpoint.
4. Under **Authentication**, select **Bearer token** and add the Braze REST API key with permission to campaigns.trigger.send.

![An example Zendesk webhook.]({% image_buster assets/img/zendesk_images/chat1.png %})


### Step 2: Create an outbound SMS campaign

Next, you’ll create an SMS campaign that will listen for webhooks from Zendesk and send a custom SMS response to your customers.

#### Step 2.1: Compose your message

When Zendesk sends the content of a message via API, it comes in the following format:


**----------------------------------------------\n\n{Replier Name}, {Replier Date}\n\n{Message}**


Therefore we need to extract the detail we want from this string to display in the message, else a user will see this:

![An example SMS without formatting.]({% image_buster assets/img/zendesk_images/chat2.png %}){: style="max-width:80%;"}

In the Message textbox, add the following Liquid code along with any opt-out language or other static content:

{% raw %}
```liquid
{% assign body = {{api_trigger_properties.${msg_body}}} %}
{% assign msg = body | split: "

" %}
New message from Zendesk: 
{{msg[2]}}
 
Feel free to respond directly to this number!

```
{% endraw %}


![An example SMS with formatting.]({% image_buster assets/img/zendesk_images/chat3.png %}){: style="max-width:80%;"}

#### 2.2 Schedule the delivery

For the delivery type, select **API-Triggered delivery**; then copy the Campaign ID which will be used in the next steps.


![API Triggered delivery]({% image_buster assets/img/zendesk_images/chat4.png %})


Finally, under **Delivery Controls**, enable re-eligibility.

![Re-eligibility enabled under "Delivery Controls."]({% image_buster assets/img/zendesk_images/chat5.png %})

### Step 3: Create a Trigger in Zendesk to forward agent replies to Braze

Next, navigate to **Objects and rules** > **Business rules** > **Triggers** 

1. Create a new **category**, for example, **Trigger a message**
2. Create a new **trigger**, for example, **Respond via SMS Braze**
3. Under **Conditions**, select:
- **Ticket>Comment** is **Present and requester can see comment** so that the message is triggered whenever a new public comment is included in a ticket update
- **Ticket>Update** via is not **Web service (API)** so that when a user sends a message from Braze, it is not forwarded back to their cell phone. Only messages coming from Zendesk will be forwarded.

![Respond via SMS Braze.]({% image_buster assets/img/zendesk_images/chat6.png %})

Under **Actions**, select **Notify by Webhook** and choose the endpoint you created in step 1. Next, specify the body of the API call. Input the campaign_id from step 2 into the request body.

![Respond via SMS Braze JSON Body.]({% image_buster assets/img/zendesk_images/chat7.png %})

{% raw %}
```liquid
{
    "campaign_id": "{{YOUR_CAMPAIGN_ID}}",
    "recipients": [
        {
            "external_user_id": "{{ticket.requester.custom_fields.braze_id}}",
			"trigger_properties": {
    "msg_body": "{{ticket.latest_public_comment_html}}"
		},
		"attributes": {
        "zendesk_ticket" : "{{ticket.id}}",
	"zendesk_ticket_open" : "true"
    }
        }
    ]
}


```
{% endraw %}


### Step 4: Create a trigger in Zendesk to update a user when a ticket is closed


If you’d like to notify the user that the ticket has been closed, create a new campaign in Braze with the templated response body 

![Update a user when ticket is closed.]({% image_buster assets/img/zendesk_images/chat8.png %}){: style="max-width:65%;"}

Select **API Triggered delivery**, copy campaign ID 

Next, set up a trigger to notify Braze when the ticket is closed:
- Category: **Trigger a message**
- Under Conditions, select **Ticket>Ticket Status** is changed to **Solved**

![Solved ticket set up in Zendesk.]({% image_buster assets/img/zendesk_images/chat9.png %}){: style="max-width:65%;"}

Under **Actions**, select **Notify by Webhook** and choose the second endpoint you just created. From there, we need to specify the body of the API call:

![Solved ticket JSON Body.]({% image_buster assets/img/zendesk_images/chat10.png %}){: style="max-width:65%;"}

{% raw %}
```liquid
{
    "campaign_id": "{{YOUR_API_KEY}}",
    "recipients": [
        {
            "external_user_id": "{{ticket.requester.custom_fields.braze_external_id}}",
"trigger_properties": {
    "msg_body": "Your ticket has been closed"
		},
,

			"attributes": {
	"zendesk_ticket_open" : "false"
    }
        }
    ]
}



```
{% endraw %}

### Step 5: Add a Custom User Field in Zendesk
In Admin Center, click **People** in the sidebar, then select **Configuration** > **User fields**. Add custom user field braze_external_id.



### Step 6: Set up inbound-SMS forwarding

Next, you’ll create two new webhook campaigns in Braze so you can forward inbound SMS from customers to the Zendesk inbox.

|Number|Purpose|
|---|---|
|Webhook campaign 1|Creates a new ticket in Zendesk.|
|Webhook campaign 2|Forwards all conversational SMS responses sent inbound from the customer to Zendesk.|
{: .reset-td-br-1 .reset-td-br-2 }

#### Step 6.1: Create an SMS keyword category

In the Braze dashboard, go to **Audience**, choose your **SMS subscription group**, then select **Add Custom Keyword**. To create an exclusive SMS keyword category for Zendesk, fill out the following fields.

|Field|Description|
|---|---|
|Keyword Category|The name of your keyword category, such as `ZendeskSMS1`.|
|Keywords|Your custom keywords, such as `SUPPORT`.|
|Reply Message|The message that will be sent when a keyword is detected, such as "A customer service rep will reach out to you shortly."|


![An example SMS keyword category in Braze.]({% image_buster assets/img/zendesk_images/chat11.png %}){: style="max-width:65%;"}

#### Step 6.2: Create your first webhook campaign

In the Braze dashboard, create your first webhook campaign. This message will signal to Zendesk that support is being requested.

In the webhook composer:
- Webhook URL: https://{{url}}.zendesk.com/api/v2/tickets
- HTTP Method: POST
- Request Headers:
- Content-Type: application/json
- Authorization:  Basic {{Token}}
- Request body: 



{% raw %}
```liquid
{
  "ticket": {
    "subject": "Action Needed",
    "comment": {
      "body": "{{sms.${inbound_message_body}}}"
    },
"requester":{
"name": "{{${first_name}}} {{${last_name}}}",
"user_fields": {
"braze_external_id": "{{${user_id}}}"
}
},
    "priority": "normal",
    "type": "problem"
  }
}


```
{% endraw %}

![An example request with the two required headers.]({% image_buster assets/img/zendesk_images/chat12.png %}){: style="max-width:65%;"}


#### Step 6.3: Schedule the first delivery

For **Schedule Delivery**, select **Action-Based Delivery**, then choose **Send an SMS Inbound Message** for your trigger type. Also add the SMS subscription group and keyword category you set up previously.

![The "Schedule Delivery" page for the first webhook campaign.]({% image_buster assets/img/zendesk_images/chat13.png %})

Under **Delivery Controls**, enable re-eligibility.

![Re-eligibility selected under "Delivery Controls" for the first webhook campaign.]({% image_buster assets/img/zendesk_images/chat14.png %})

#### Step 6.4: Create your second webhook campaign

Set up a webhook campaign to forward remaining SMS messages from the user to Zendesk:

Because Zendesk sends the ticket ID as a string, create a content block to convert the string to an integer in order to leverage it in Zendesk’s webhook

{% raw %}
```liquid

{% assign var = {{custom_attribute.${zendesk_ticket}}} | to_i %}{{var}}

```
{% endraw %}

In the webhook composer:
- Webhook URL: https://{{url}}.zendesk.com/api/v2/tickets/{{content_blocks.${to_int}}}.json
- Request: PUT
- KVPs:
- - Content-Type:application/JSON
- - Authorization: Basic {{Token}}

Sample Body: 

{% raw %}
```liquid

{
  "ticket": {
    "comment": {
      "body": "Inbound message from {{${first_name}}} {{${last_name}}}: {{sms.${inbound_message_body}}}"
    }
}
}


```
{% endraw %}

#### Step 6.5: Complete second webhook campaign setup
- Set up an action based trigger for users who send an inbound message in category ‘Other’
- Set up re-eligibility criteria
- Add applicable audiences, in this case custom attribute **zendesk_ticket_open** is **true**
