---
nav_title: Jasper
article_title: Jasper
description: "This reference article outlines the integration between Braze and Jasper."
alias: /partners/jasper/
page_type: partner
search_tag: Partner
---

# Jasper 
> [Jasper](https://www.jasper.ai/) is an AI-powered content platform that empowers brands and marketing teams to create, manage, and scale high-quality, on-brand content across various channels including blogs, ads, and social media. This integration is officially maintained by Jasper.

_This integration is maintained by Jasper._

## About the Integration

The integration between Jasper and Braze empowers marketing teams to streamline content creation and campaign execution. With Jasper, teams can generate high-quality, on-brand copy in minutes. Braze then enables the delivery of these messages to the right audience at the optimal time. This integration fosters seamless workflows, reduces manual effort, and drives stronger engagement outcomes.

## Key Benefits

* **Faster Campaign Execution:** Launch campaigns in minutes, not weeks.
* **Consistent Brand Voice:** Jasper templates ensure all generated copy adheres strictly to brand guidelines.
* **Targeted Content Generation:** Leverage audience segments, style guides, and proprietary knowledge items for highly customized messaging.
* **Dynamic Personalization:** Utilize Liquid placeholders (e.g., `{{${first_name}}}`) for scalable personalization within Braze.
* **Error Reduction:** Automated workflows minimize copy-paste errors and reduce manual steps.

## Prerequisites

| Requirement         | Description  |
| ------------------- | ------------ |
| Jasper Account      | You need a Jasper account to utilize this partnership. |
| Braze REST API Key  | A Braze REST API key with the following permissions. <br>  <br>`templates.email.create` <br> `templates.email.update` <br>`content_blocks.create` <br>`content_blocks.update` <br><br>This key can be generated in the Braze dashboard by navigating to **Settings > API Keys**.  |
| Braze REST Endpoint | Your REST endpoint URL. Your specific endpoint depends on the Braze URL for your instance. Refer to the [Braze API Basics: Endpoints](https://www.google.com/url?q=https://www.braze.com/docs/api/basics/%23endpoints&sa=D&source=editors&ust=1757963526724172&usg=AOvVaw04w_dej7JF-hz0X_h6cjmD) documentation for more details. |

## Integration Methods

There are two primary methods for generating content in Jasper and updating Braze templates:

1. **Using Jasper's API Directly**
2. **Using Jasper Studio to Build a Braze-Ready Custom App**

## Method 1: Using Jasper's API Directly

This method is ideal for teams who wish to programmatically create and update email HTML templates in Braze, bypassing manual setup in the Jasper UI and Braze.

### Step 1: Jasper Setup

1. **Obtain a Jasper API Key:** Follow the instructions in [Jasper's API documentation](https://www.google.com/url?q=https://developers.jasper.ai/docs/getting-started-1&sa=D&source=editors&ust=1757963526726122&usg=AOvVaw3InHqZZTILoEC73mOfvUdh) to generate your API key.
2. **Utilize Pre-Built Templates:** Jasper offers over 40 optimized templates. For generating Braze HTML email templates, use the following:
   * **Template ID:** `skl_BC53D8AC5B4B47E8BE557EBB706E9B47`
3. **Understand Input Schema:** The following fields are required when making a request to generate content for a Braze HTML email template:
   * `emailObjective`: Clearly define the goal of the email.
   * `ctaLink`: The URL for your call-to-action.
   * `unsubscribeLink`: Required for marketing emails.
   * `brandColor`: Your brand's primary color in hexadecimal format (e.g., `#4dfa8a`).
   * **Optional Parameters:**
     * `toneId` for brand voice application.
     * `audienceId` for audience segmentation.
     * `styleId` for style guide application.
     * `knowledgeIds` (up to 3 items) for enhanced content context.
4. **Generate Output:** Execute the template via the Jasper API. This will produce a JSON payload containing the `subject`, `preheader`, and `body` (HTML content).

{% tabs %}
{% tab Sample Request %}

### Sample Request

```
curl --location 'https://api.jasper.ai/v1/templates/skl_BC53D8AC5B4B47E8BE557EBB706E9B47/run?toneId=ton_811696974b3c4db4b3ac0041685c3b7c&knowledgeIds=kno_0a62fc17529e4fe69a71f30b6f0e88a7&audienceId=aud_0199117a690a7cc98481f8700916e2a6' \
--header 'Content-Type: application/json' \
--header 'x-api-key: ••••••' \
--data '{
  "inputs": {
    "emailObjective": "Announce a webinar and highlight Jasper + Braze integration benefits. Use {{${firstname}}} in the subject and body. Body length ~400 words. Include CTA buttons for registration and footer with unsubscribe link. Apply brand color to buttons and links.",
    "ctaLink": "https://yourbrand.com/register",
    "unsubscribeLink": "{{${unsubscribe_link}}}",
    "brandColor":"#4dfa8a"
  },
  "options": {
    "outputCount": 1,
    "outputLanguage": "English",
    "inputLanguage": "English",
    "languageFormality": "less"
  }
}'
```
{% endtab %}
{% tab Sample Output %}

### Sample Output
```
{
  "subject": "GlowUp Serum is Here! Limited-Time 20% Off!",
  "preheader": "GlowUp Serum is here with a 20% launch discount for 7 days only!",
  "body": "<html> ... </html>"
}
```
{% endtab %}
{% endtabs %}

### Step 2: Braze Setup

1. **Create an Email Template in Braze:** Using the `subject`, `preheader`, and `body` generated by Jasper in Step 1, make a POST request to the Braze REST API to create a new email template. Ensure your Braze REST API key has the necessary permissions (`templates.email.create` and `templates.email.update`).


### Sample Braze API Request (Create Email Template)

```
curl --location --request POST 'https://rest.iad-03.braze.com/templates/email/create' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <YOUR_BRAZE_API_KEY>' \
--data '{
  "template_name": "email_template_jasperapi_20231104T142300Z",
  "subject": "GlowUp Serum is Here! Limited-Time 20% Off!",
  "preheader": "GlowUp Serum is here with a 20% launch discount for 7 days only!",
  "body": "<html> ... </html>"
}'
```


## Method 2: Using Jasper Studio to Build a Braze-Ready Custom App

Jasper Studio is a no-code platform within Jasper that allows marketing teams to build tailored AI apps without requiring IT support. You can design a custom app that generates JSON structures specifically formatted for Braze's API, or simply generate content that can be manually added to your Braze messages.

## What You Can Build

1. **Create an App:** From your Jasper home screen, click `Create an App.`
2. **Specify App Type:** Define the app you want to create (e.g., "Braze HTML Email Template" or "Content Block Template").
3. **Customize Input Prompts:** Jasper will generate input prompts based on your description. Edit these fields to your liking. For an HTML email template, you might include input forms for: Subject line, preheader, HTML body, tags, inline CSS toggle, and template name.
4. **Integrate Knowledge Embeds:** Add guidance on Liquid best practices to ensure consistent personalization and dynamic content.
5. **Edit LLM Instructions:** Refine the instructions provided to the Large Language Model (LLM) for content generation.
6. **Provide Example Output:** Give an example of the desired output. This can include automated JSON output formatted for Braze payloads.
7. **Generate and Export:**
  * **Direct Copy/Paste:** Content can be copied and pasted directly into the Braze platform.
  * **JSON Output:** Generate JSON output. This payload can then be used to directly call Braze’s endpoint via `curl`, middleware, or integrated into your email operations workflow.

![A screenshot of a computer AI-generated content may be incorrect.](images/image1.png)

{% tabs %}
{% tab Example JSON Output (Custom App) %}

## Example JSON Output (Custom App)

```
{
  "template_name": "email_webinar_2025",
  "subject": "Join Our Webinar, {{${firstname}}}!",
  "preheader": "Unlock the potential of seamless integration.",
  "body": "<html> ... </html>",
  "tags": ["jasperapi"],
  "should_inline_css": true
}
```
{% endtab %}
{% tab Sample Braze API Request (Using Custom App Output) %}

## Sample Braze API Request (Using Custom App Output)

```
curl --location --request POST 'https://rest.iad-03.braze.com/templates/email/create' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <YOUR_BRAZE_API_KEY>' \
--data '{
  "template_name": "email_template_jasperapi_20231104T142300Z",
  "subject": "GlowUp Serum is Here! Limited-Time 20% Off!",
  "preheader": "GlowUp Serum is here with a 20% launch discount for 7 days only!",
  "body": "<html> ... </html>"
}'
```
{% endtab %}
{% endtabs %}

Alternatively, if you are a marketer, you can create your custom app to align with brand guidelines to generate content without HTML and copy and paste, and use Braze templates for styling.

# References

* [Jasper API Documentation](https://www.google.com/url?q=https://developers.jasper.ai/reference/gettemplate-1&sa=D&source=editors&ust=1757963526752804&usg=AOvVaw31An2qmVBuPuJOLfjzviAF)
* [Braze API: Create Email Template](https://www.google.com/url?q=https://www.braze.com/docs/api/endpoints/templates/email_templates/post_create_email_template/%23request-parameters&sa=D&source=editors&ust=1757963526753462&usg=AOvVaw29hMMV0s4t2g1-wysVlGOt)
* [Braze API: Content Blocks](https://www.google.com/url?q=https://www.braze.com/docs/api/endpoints/templates/content_blocks_templates/post_create_email_content_block&sa=D&source=editors&ust=1757963526753795&usg=AOvVaw2tLbt0FXD1wAmk-JaaAwnb)
* [Jasper Help Center](https://www.google.com/url?q=https://help.jasper.ai/hc/en-us/articles/36783295610395-Jasper-Studio?utm_source%3Dchatgpt.com&sa=D&source=editors&ust=1757963526753114&usg=AOvVaw3xnY4Zpiq_YKJAdD9ZBMNY)

