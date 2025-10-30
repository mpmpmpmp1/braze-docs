---
nav_title: Smartling
article_title: Smartling
description: "This reference article outlines the partnership between Braze and Smartling, a cloud-based software for localization. The Braze Connector supports the translation of HTML email templates, Content Blocks, Canvases, and campaign email messages."
alias: /partners/smartling/
page_type: partner
search_tag: Partner
---

# Smartling

> [Smartling][https://www.smartling.com/] is an end-to-end cloud translation management software for customers looking to automate the translation of websites, applications, and customer experiences.

_This integration is maintained by Smartling._

## About the integration

The Braze Connector supports translations for Campaigns and Canvases ([Email](https://www.braze.com/docs/user_guide/message_building_by_channel/email/using_locales/#prerequisites), [Push](https://www.braze.com/docs/user_guide/message_building_by_channel/push/using_locales/#prerequisites), and [IAM](https://www.braze.com/docs/user_guide/message_building_by_channel/in-app_messages/using_locales)), Email Templates, and Content Blocks. Translations are supported in both HTML and Drag-and-Drop editors where supported. 

{% alert note %}
Depending on your use case, you can manage translations for Content Blocks or Email Templates using either the legacy translation workflow or the updated one. In the updated workflow, using Braze's multi-language support and locales in messages, translation tags are added to the Content Block or Email Template. However, Smartling executes translations at the message level. The content is translated only once it’s included in a Campaign or Canvas and the target locale is set. Please see the **Managing translations for Content Blocks and Email Templates** section for more information.
{% endalert %}


## Prerequisites

| Requirement                   | Description                                                                                                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Smartling account             | A [Smartling account](https://dashboard.smartling.com/) is required to take advantage of this partnership.                                                          |
| Smartling translation project | To connect your Braze account with Smartling, you must first sign in and [create a translation project](https://help.smartling.com/hc/en-us/articles/115003074093). |
| Braze REST API key            | A Braze REST API key with the following permissions: <br>- campaigns.translations.get<br>- campaigns.translations.update<br>- campaigns.list<br>- campaigns.details<br>- canvas.translations.get<br>- canvas.translations.update<br>- campaigns.list<br>- campaigns.list<br>- campaigns.details<br>- templates.email.create<br>- templates.email.update<br>- templates.email.list<br>- templates.email.info<br>- templates.translations.get<br>- templates.translations.update<br>- content_blocks.info<br>- content_blocks.list<br>- content_blocks.create<br>- content_blocks.update<br><br> This can be created in the Braze dashboard from **Settings > API Keys**. |
| Braze REST endpoint           | [Your REST endpoint URL](https://www.braze.com/docs/api/basics/#endpoints). Your endpoint will depend on the Braze URL for your instance.             |
| Braze Multi Language Settings | [Complete Multi Language Settings in Braze](https://www.braze.com/docs/user_guide/administrative/app_settings/multi_language_settings/#prerequisites) |


## Integration

### Step 1: Set up multi language settings in Braze

Refer to the [instructions](https://www.braze.com/docs/user_guide/administrative/app_settings/multi_language_settings/#prerequisites) for setting up locales in Braze.

### Step 2: Set up the Braze project in Smartling TMS

Refer to Smartling [documentation](https://help.smartling.com/hc/en-us/articles/13248549217435) for details on connector configuration.

#### Connecting Braze to Smartling

1. In [Smartling](https://dashboard.smartling.com/), create a [Braze Connector](https://help.smartling.com/hc/en-us/articles/115003074093) project type in your Smartling account.

![Braze connection in Smartling.]({% image_buster /assets/img/smartling/image1_Connecting .png_Braze_to_Smartling.png %})

2. In this project, select **Settings** > **Braze Settings** > **Connect to Braze**.
   * Enter the required fields like API URL and API Key. If the Test Connection is successful, save Connection. If the test is not successful, double check you’ve inputted the correct API URL and API Key.

![Braze connection in Smartling API settings.]({% image_buster /assets/img/smartling/image2_API.png %})

3. Add additional project languages

![Braze connection in Smartling Project Languages.]({% image_buster /assets/img/smartling/image3_project_languages.png %}) assets/img/smartling/image3_project_languages.png

4. In Braze Settings, verify that the values in the Target Language (Braze) column match the locales configured in Braze multi-language settings. The locale naming convention must match exactly.

![Braze connection in Smartling Language Confirmation.]({% image_buster /assets/img/smartling/image4_language_confirmation.png %})

### Step 3: Add Translation Tags to your Braze message

Refer to the [instructions](https://www.braze.com/docs/user_guide/message_building_by_channel/email/using_locales/?tab%3Dhtml%2520editor#prerequisites) on how to add translation tags to your messages:

* [Email](https://www.braze.com/docs/user_guide/message_building_by_channel/email/using_locales/#prerequisites)
* [Push](https://www.braze.com/docs/user_guide/message_building_by_channel/push/using_locales/#prerequisites)
* [In App Messages](https://www.braze.com/docs/user_guide/message_building_by_channel/in-app_messages/using_locales)

Here is an example of a HTML Email campaign with translation tags.

![Braze email with translation tags.]({% image_buster /assets/img/smartling/image5_translation_tags.png %})

You must save the message as a draft before you can select locales.

### Step 4: Manage Translations in Smartling

Once the Braze connector has been connected and set up, you will find Braze content in the Braze tab in your Smartling project. Refer to Smartling [documentation](https://help.smartling.com/hc/en-us/articles/13248577069979) to learn more.

Smartling provides advanced features to search and select content by:

* Keyword search
* Braze content type
* Braze tagging

1. In the example below, you can see the New Year promotion email campaign that was created in Step 3.

![Braze email with translation tags.]({% image_buster /assets/img/smartling/image6_ny_promotion.png %})

2. Once you’ve located the campaign you want to translate, select the folder, choose the variants, and click Request Translation.

![Request Translations.]({% image_buster /assets/img/smartling/image7_request_translation.png %})

3. Create a new job for the translation.

![Create a new job for the translation.]({% image_buster /assets/img/smartling/image8_request_translation.png %})

4. Once the job has been authorized, you can edit each translation in the CAT tool.

![Translation CAT Tool.]({% image_buster /assets/img/smartling/image9_translation_job.png %})

5. After the translations are complete, save and submit your translation to Braze.

![Submit translation to Braze.]({% image_buster /assets/img/smartling/image10_translations.png %})

### Step 5: Preview the Message as a Multi-Language User in Braze

In Braze, preview your campaign as a multi-language user to confirm that the translations were applied correctly.

![Multi language user preview.]({% image_buster /assets/img/smartling/image11_preview.png %})

## Managing translations for Content Blocks and Email Templates

Content Blocks and Email Templates are managed under the Templates & Media section in Braze.

### Translation stored as part of the message component.

Translation tags belong on the Content Block or Email Template. However, Smartling executes translations at the message level: the content is translated only once it’s included in a Campaign or Canvas and the target locale is set.

### Considerations with this approach:

* Translation tags have to be manually added to the content block for both HTML and DnD content block editors.
* Locales are selected at the message level, not on the content blocks themselves.
* For canvas, we recommend using the Row function to insert content blocks into your message instead of manually adding them with a liquid tag. Note that dragging a content block from the preview into an email makes a local copy; any changes to the "parent" content block will not propagate to other campaigns using that block.
* If you do use a content block liquid tag, be sure to include at least one translation tag directly in the email body. Manually adding the translation tag will allow you to select the locales from the multi language drop down. Smartling will pick up the translation tags for the content block. You can add a ‘comment’ tag to ensure the text is not visible to the end user.

### Translations embedded as part of a Content Block or Email Templates.

If you prefer to manage translations directly within a Content Block or Email Template, refer to the legacy instructions in [Smartling's documentation](https://help.smartling.com/hc/en-us/articles/13248577069979-Translating-with-the-Braze-Connector). This method uses a language attribute and Liquid if/else logic to display text in different languages.

## FAQ

### Are translation tags supported for DnD editor?

For DnD editor (Email, Content Block, IAM), translation tags must be manually added as liquid tags.

### How to translate text within a liquid tag?

Smartling recognizes liquid tags and makes them uneditable variables in the UI. Any other text within the liquid tag such as default text, or filters like join, add, etc. also become uneditable.

**Workaround:** The user can remove the liquid variable in the Smartling UI and recreate the liquid tag with the translated default text. A warning will appear when saving the translation.
