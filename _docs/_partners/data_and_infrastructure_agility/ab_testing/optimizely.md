---
nav_title: Optimizely
article_title: Optimizely
description: "Learn how to integrate Optimizely with Braze."
alias: /partners/optimizely/
page_type: partner
search_tag: Partner
layout: dev_guide
---

Optimizely is a leading digital experience platform that offers experimentation and content management tools for digital products and marketing campaigns.

The Braze and Optimizely integration is a two-way integration that allows you to:

- Sync your Braze customer segments and events to Optimizely Data Platform (ODP) nightly to enrich Optimizely customer profiles, reports, and segmentation.
- Send Braze Currents events from Braze to Optimizely’s reporting tool.
- Sync ODP customer data and events to Braze to enrich your Braze customer data and trigger Braze messaging based on customer events in ODP.

# Prerequisites

| Requirement                     | Description |
|----------------------------------|-------------|
| Optimizely Data Platform Account | An ODP account is required to take advantage of this partnership. |
| Braze REST API key               | A Braze REST API key with the following permissions: `users.track`,`users.export.segments`,`segments.list`,`campaigns.trigger.send`,`canvas.trigger.send` |
| Currents                         | To export data back into Optimizely, you need to have Braze Currents set up for your account. |
| Optimizely URL and Token         | This can be obtained by navigating to your Optimizely dashboard and copying the ingestion URL and token. |

# Integration

### Step 1: Configure the integration

1. Go to the **App Directory** in ODP.
2. Select the **Braze** app.
3. Click **Install App**.
4. Go to the **Settings** tab.
5. In the **Authorization** section, enter your Braze **REST API Key**, select your Braze **Instance URL**, and click **Verify API Key**.
6. Create a Custom Currents Export in Braze using the endpoint and token provided in ODP. This is required to sync Braze events to ODP.
   ![Optimizely Authorization](/assets/img/optimizely_image1.png)
7. In the **Segments** section, select the Braze segments you want to sync to ODP from the **Segments to Sync** multi-select list and [add any additional field mappings](https://www.google.com/url?q=https://support.optimizely.com/hc/en-us/articles/29918568615949-Integrate-Braze%23h_01J6Z1P53JVDBFZ758Q78CK1QB&sa=D&source=editors&ust=1733948158380300&usg=AOvVaw3WSAND5ie3LCVuSxUlLanR) you want between Braze and ODP. If you want to sync all segments, click **Import All Customers**. After you complete this, you must click **Save**.
 ![Optimizely Braze Segment Sync](/assets/img/optimizely_image2.png)

{% alert tip %} You must select segments here to import Braze customer profiles. If you do not select any segments, the integration will not import any customer profiles. {% endalert %}

### Step 2. Map data fields

The app has default data field mappings between Braze and ODP. For example, the **Email** field in Braze is mapped to the **Last Seen Email** field in ODP.

![Optimizely Braze Segment Map Fields](/assets/img/optimizely_image3.png)

If there are additional data fields in Braze that you want to map to ODP:

1. In the **Segments** section of the app, select the Braze field from the **Braze User Data Fields** drop-down list.
2. Select the ODP field from the **ODP Customer Fields** drop-down list.
3. Click **Save Field Map**.

![Optimizely Braze Segment Save Field Maps](/assets/img/optimizely_image4.png)

You can also delete any data field mappings that are not required:

1. In the **Segments** section of the app, select the field mapping you want to delete from the **Field Map** drop-down list.
2. Click **Delete Field Map**.

![Optimizely Braze Segment Delete Field Maps](/assets/img/optimizely_image5.png)

### Step 3: Sync data from ODP to Braze

After you configure the app, you can set up an activation in ODP to sync your ODP customer data to Braze.

1. Go to **Activation > Engage**.
2. Click **Create New Campaign**.
3. To set up an automated, recurring sync, click **Behavioral**.
4. Click **Create From Scratch**.
5. Enter a name for your activation that represents the data you are syncing to Braze (for example, **Braze Data Sync**).
6. In the **Enrollment** section, you can sync data for customers that match a segment, or you can sync data for customers that trigger an event (like when ODP registers that a customer opens an email).
   - **Customers that match a segment** – Select your desired segment and click **Next**.
     ![Optimizely Select Segment](/assets/img/optimizely_image6.png)
   - **Customers that trigger an event** – Expand the **Filter** drop-down list and select the ODP event that you want to use as the trigger for this data sync to Braze. Expand **Automation Rules** and adjust as desired.
     ![Optimizely Trigger Event](/assets/img/optimizely_image7.png)

7. Expand **Touchpoints**.
8. Click to edit **Touchpoint 1** and select **Braze**.
9. Expand the **Targeting** section and select the **Target Identifier**.
10. Select one of the following options for **Add Users To** in the **Configure** section:
    - **Campaign** – Add customers to a specific campaign in Braze. After choosing this option, you must select the Braze campaign.
    - **Canvas** – Add customers to a specific canvas in Braze. After choosing this option, you must select the Braze canvas.
    - **Profile Update Only** – Update only the Braze customer profile.

11. (Optional) Select the **Number of Additional Fields** you want to sync to Braze (up to 20).  
    A drop-down list and input field display for the number of additional fields you selected. In each **Field #** drop-down list, select the Braze field you want to populate. In each corresponding **Field # Value**, enter the ODP field you want to send to the selected Braze field. For example, if you selected **Company Name** from the **Field #** drop-down list, enter `{{customer.company_name}}` for the corresponding **Field # Value**.

12. Click **Save** and then click your activation name in the breadcrumb trail.
13. Click **Select start time and schedule** in the **Touchpoints** section if you selected **Customers that match a segment** for the enrollment.
14. Complete the following settings, then click **Apply**.
    - **Recurring or Continuous** – Select **Recurring**.
    - **Start Date** – Enter the date you want to send the data to Braze.
    - **End** – Defaults to **Never**. If you want to end the Braze data sync on a specific date, set that here.
    - **Repeats** – Set to **Daily**.
    - **Repeat Every** – Set to **1 day**.
    - **Timing** – Enter the time you want to send the data to Braze.
    - **Time Zone** – Select the time zone in which you want to send this data.

15. Click **Save** and then click **Go Live**. Your sync starts at your designated start date and time (or when the trigger event occurs).

## Troubleshoot the data sync

To ensure data is syncing as expected from ODP to Braze:

1. Go to **Account Settings > Event Inspector** in ODP.
2. Click **Start Inspector**.
3. When data is available in the inspector, a number displays next to **Refresh**. Click to view the data.
4. The raw data that ODP and Braze sends back and forth displays. Click **View Details** to see the formatted version of that raw data.
5. Data fields sent from Braze back to ODP start with `_braze`.

Each data sync is also logged in the [ODP activity log](https://www.google.com/url?q=https://support.optimizely.com/hc/en-us/articles/4407268804365-Use-the-Activity-Log&sa=D&source=editors&ust=1733948158385124&usg=AOvVaw2tMOxzcTKfL0-oYLT4IMpP):

1. Go to **Account Settings > Activity Log**.
2. Filter the categories by **braze**.
3. Click **View Details** for a formatted view of the log details, including the number of matches.

Let me know if you need further assistance!
