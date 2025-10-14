---
nav_title: StackAdapt
article_title: StackAdapt
description: "This reference article outlines the partnership between Braze and StackAdapt."
page_type: partner
search_tag: Partner

---


# StackAdapt

> [StackAdapt](https://www.stackadapt.com/) is the leading AI-powered marketing platform used by the most exceptional digital marketers to deliver targeted, performance-driven advertising.

_This integration is maintained by StackAdapt._

## About the Integration

The Braze and StackAdapt integration allows you to sync customer profile data from Braze into the StackAdapt Data Hub. By connecting the two platforms, you can create a unified view of your customers and activate first-party data to improve ad performance.

## What are the benefits

* **Re-engage lapsed customers:** Identify users who have unsubscribed from email marketing lists in Braze and target them with programmatic ads on StackAdapt to re-engage them through a different channel.
* **Create multi-channel experiences:** Extend a user's journey beyond email. For example, if a user clicks on an email campaign in Braze, you can use StackAdapt to show them a complementary programmatic ad, reinforcing the message and driving further action.
* **Personalize at scale:** Leverage granular data points from Braze, such as *Home City* or *Language*, to serve highly relevant, localized, and language-specific ads and emails.
* **Deepen understanding of your audience:** By syncing profile attributes, you can create richer audience segments in StackAdapt, enabling more precise targeting and personalized ad experiences.

## Prerequisites

| Requirement             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **StackAdapt Account**  | You need an active StackAdapt account with permissions to manage Data Hub integrations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Braze REST API key**  | A Braze REST API key with the following permissions:<br><br>- `users.export.ids`<br>- `users.export.segment`<br>- `email.unsubscribe`<br>- `email.hard_bounces`<br>- `messages.schedule_broadcasts`<br>- `campaigns.list`<br>- `campaigns.details`<br>- `canvas.list`<br>- `canvas.details`<br>- `segments.list`<br>- `segments.details`<br>- `purchases.product_list`<br>- `events.list`<br>- `feed.list`<br>- `feed.details`<br>- `templates.email.info`<br>- `templates.email.list`<br>- `subscription.status.get`<br>- `Subscription.groups.get`<br><br>This can be created in the Braze dashboard from **Settings > API Keys.** |
| **Braze REST endpoint** | [Your REST endpoint URL](https://www.braze.com/docs/api/basics/#endpoints). Your endpoint depends on the Braze URL for your instance.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## How it Works

The StackAdapt Data Hub connects directly to your Braze account to pull customer profile attributes. This allows you to leverage your Braze customer data directly within StackAdapt for advanced audience segmentation and activation.

### Data Flow

* StackAdapt initiates a secure connection to your Braze instance using the provided API credentials.
* StackAdapt retrieves customer profile data and specifically the properties you have selected and mapped.
* This data is then normalized and ingested into your StackAdapt Data Hub, becoming available for segmentation and use in your campaigns.
* The integration allows for scheduled data syncs (for example, daily) to ensure your StackAdapt audiences are kept up-to-date with the latest profile information from Braze.

## Fields Synced

StackAdapt can sync a variety of Braze profile fields, including, but not limited to:

{% tabs local %}
{% tab Standard attributes %}

**Standard Attributes:**
  * Email
  * Date of Birth
  * First Name
  * Last Name
  * Phone
  * Home City
  * Country
  * Gender
  * Time Zone
  * Created At
  * External ID
  * Language 

 
{% endtab %}

{% tab Custom Attributes %}

**Custom Attributes:**
Attributes that are specific to your app or business, defined based on your specific business needs.
{% endtab %}

{% tab Attribution Data %}

**Attribution Data**

  * Attributed Ad
  * Attributed Adgroup
  * Attributed Campaign
  * Attributed Source

 {% endtab %}
 {% tab Subscription Status %}

**Subscription Status:**
  
  * Email Subscription Status
  * Push Subscription Status 

It is crucial to accurately map fields in Braze that reflect user consent for marketing communications (for example, email subscription status). This ensures that your advertising efforts remain compliant with user preferences and privacy regulations.

{% endtab %}
{% endtabs %}

## Setting Up the Integration

Follow these steps to import your Braze customer profiles:

1. **Navigate to Data Hub Integrations**

   * Log in to your StackAdapt account.
   * From the left-hand navigation menu, select **Data Hub**.

2. **Import from Integration**

   * Click on the **Import Profiles** button.
   * Select **Braze** from the list of available integrations.

3. **Authenticate Your Braze Account**

   * You will be prompted to enter your Braze API credentials:

     * **Braze REST API Key:** (Found under *Settings > API Keys* in Braze).
     * As a best practice for security, we recommend creating a dedicated API key for your StackAdapt integration.
     * **Braze App Key:** (Found under *Settings > API Keys* or *Manage Apps* in Braze).
     * **Braze REST Endpoint URL:** Enter the base URL for your Braze instance (for example, `https://rest.iad-01.braze.com`).
   * Click **Connect** to verify the credentials.

   ![Braze Connection Screenshot in the StackAdapt UI.]({% image_buster /assets/img/stackadapt/StackAdapt_Braze_Connection_Settings.png %})

5. **Choose your connection and select your StackAdapt advertiser**

6. **Configure your Property Mappings**

   * Once connected, a mapping interface will be displayed.
   * StackAdapt will suggest default mappings and pre-select some of the properties. Review and confirm these.
   * If you want to import additional properties, make sure to select them by checking the checkbox on the left and specify if it contains PII and the data type.

  ![Braze Connection Screenshot in the StackAdapt UI.]({% image_buster /assets/img/stackadapt/StackAdapt_mappings.png %})

7. **Add your profiles to a List** or create a new one so it’s easy to group and segment your profiles.

8. Click **Activate Integration** to start the initial data sync.

## Important Considerations

* Importing **custom events and properties is not yet supported**, but this feature is under consideration for future development.
* **Data Latency:** It can take up to 24 hours to import all of the profile data.
* **Consent Management:** Ensure that your data collection practices in Braze align with privacy regulations and that you have the necessary consent to use customer data for advertising purposes. StackAdapt relies on the consent status passed from your source systems.
* **Attribute Consistency:** To maximize the effectiveness of your data, ensure consistency in how attributes are named and populated in Braze before syncing them to StackAdapt.
