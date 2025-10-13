---
nav_title: Oppizi
article_title: Oppizi 
alias: /partners/oppizi/
description: "This reference article outlines the partnership between Braze and Oppizi."
page_type: partner
search_tag: Partner
---

# Oppizi

> [Oppizi](https://www.oppizi.com/) is the global leader in offline marketing, providing a one-stop solution for businesses to run measurable, targeted direct mail and flyering campaigns.

_This integration is maintained by Lob._

## Prerequisites

| Requirement                    | Description                                                                   |
| ------------------------------ | ----------------------------------------------------------------------------- |
| Oppizi account                 | An active Oppizi account is required to use this integration.                 |
| Oppizi API key                 | Found in your Oppizi account, under **Integrations -> Braze**.                |
| Oppizi Direct Mail workflow ID | Create a workflow in Oppizi on the Direct Mail Workflow page to obtain an ID. |

## Use Cases

With the Oppizi integration, you can:

* **Send automated direct mail postcards** using Braze triggers connected to Oppizi's webhook and direct mail workflows.
* **Configure thresholds, waves, and limits** in Oppizi direct mail workflows to control the sending of your campaigns.
* **Design professional postcards** with Oppizi’s built-in design tool – no design experience required.
* **Track campaign performance** in real time with Oppizi’s dashboard.

## Integration

### Step 1: Generate your Oppizi API Key 

You need to generate your Oppizi API Key in order to use it in your webhook template in Braze.

1. Log in to Oppizi.
2. Go to **Integrations > Braze**.
3. Generate your API Key.
4. Manage your keys from the same page (revoke or create new ones as needed).

### Step 2: Create a Braze webhook template

Create an Oppizi webhook template to use in future campaigns or Canvases by navigating to **Templates > Webhook Templates** in the Braze platform.

**Webhook Settings:**

* **Webhook URL**: [https://webhook.oppizi.com/events](https://webhook.oppizi.com/events)
* **Request Body**: Raw text - format detailed in the section below.

**Request Method and Headers:**

Oppizi requires an HTTP method along with the following HTTP headers to be included in the template.

* **HTTP Method**: POST
* **Request Headers**:
  * **Authorization**: Bearer <oppiziAPIKey>
  * **Content-Type**: application/json


![A message error log showing the time, app name, channel, and error message. The error message includes the message alert and the status code.]({% image_buster /assets/img_archive/error_log.png %})

**Request Body:**

The request body must include the field **oppiziWorkflowID**. This ID is generated when a workflow is created in Oppizi, and it is required to specify which direct mail workflow your recipients should be added to. Each direct mail workflow in Oppizi has a unique ID, so if you create an Oppizi webhook template in Braze, make sure to always update the workflow ID to the correct one.

Additionally, make sure all required custom attributes are set up in your Braze account for your recipients’ postal addresses, as these are necessary for sending direct mail.

![A message error log showing the time, app name, channel, and error message. The error message includes the message alert and the status code.]({% image_buster /assets/img_archive/error_log.png %})

{% raw %}
```json
{
"event" : "workflow.addRecipient",
"oppiziWorkflowID" : "<oppiziWorkflowID>",
"recipient" : {
"brazeID" : "{{${braze_id}}}",
"firstName" : "{{${first_name}}}",
"lastName" : "{{${last_name}}}",
"address1" : "{{custom_attribute.${address1}}}",
"address2" : "{{custom_attribute.${address2}}}",
"city" : "{{custom_attribute.${city}}}",
"country" : "{{${country}}}",
"zipCode" : "{{custom_attribute.${zipCode}}}",
"state" : "{{custom_attribute.${state}}}"
}
```
{% endraw %}

### Step 3. Create a Direct Mail Workflow in Oppizi

1. In Oppizi, go to **Direct Mail Workflow > Create workflow**
2. Configure workflow details, including thresholds, waves, postcard format, and artwork.
3. In the webhook details section, you’ll find a ready-to-use request body, including your workflow ID, that you can paste directly into Braze.

### Step 4. Preview and test your request in Braze

After adding your request body containing Oppizi’s workflow ID, preview the request and run a test to confirm successful setup. Once validated, you'll be ready to go with your automated direct mail campaigns.
