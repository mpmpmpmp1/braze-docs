Sure! Here's your HTML content converted to standard Markdown syntax:

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
| Braze REST API key               | A Front REST API key will be used to make an outbound webhook request from Braze to Front. |
| Currents                         | To export data back into Optimizely, you need to have Braze Currents set up for your account. |
| Optimizely URL and Token         | This can be obtained by navigating to your Optimizely dashboard and copying the ingestion URL and token. |

# Integration

## Step 1: Configure the integration

1. Go to the **App Directory** in ODP.
2. Select the **Braze** app.
3. Click **Install App**.
4. Go to the **Settings** tab.
5. In the **Authorization** section, enter your Braze **REST API Key**, select your Braze **Instance URL**, and click **Verify API Key**.
6. Create a Custom Currents Export in Braze using the endpoint and token provided in ODP. This is required to sync Braze events to ODP.
7. In the **Segments** section, select the Braze segments you want to sync to ODP from the **Segments to Sync** multi-select list and [add any additional field mappings](https://www.google.com/url?q=https://support.optimizely.com/hc/en-us/articles/29918568615949-Integrate-Braze%23h_01J6Z1P53JVDBFZ758Q78CK1QB&sa=D&source=editors&ust=1733948158380300&usg=AOvVaw3WSAND5ie3LCVuSxUlLanR) you want between Braze and ODP. If you want to sync all segments, click **Import All Customers**. After you complete this, you must click **Save**.

   You must select segments here to import Braze customer profiles. If you do not select any segments, the integration will not import any customer profiles.

### Step 2. Map data fields

The app has default data field mappings between Braze and ODP. For example, the **Email** field in Braze is mapped to the **Last Seen Email** field in ODP.

If there are additional data fields in Braze that you want to map to ODP:

1. In the **Segments** section of the app, select the Braze field from the **Braze User Data Fields** drop-down list.
2. Select the ODP field from the **ODP Customer Fields** drop-down list.
3. Click **Save Field Map**.

You can also delete any data field mappings that are not required:

1. In the **Segments** section of the app, select the field mapping you want to delete from the **Field Map** drop-down list.
2. Click **Delete Field Map**.

### Step 3: Sync data from ODP to Braze

After you configure the app, you can set up an activation in ODP to sync your ODP customer data to Braze.

1. Go to **Activation > Engage**.
2. Click **Create New Campaign**.
3. To set up an automated, recurring sync, click **Behavioral**.
4. Click **Create From Scratch**.
5. Enter a name for your activation that represents the data you are syncing to Braze (for example, **Braze Data Sync**).
6. In the **Enrollment** section, you can sync data for customers that match a segment, or you can sync data for customers that trigger an event (like when ODP registers that a customer opens an email).

- **Customers that match a segment** – Select your desired segment and click ...

---

You can copy this directly as markdown into your system clipboard. Let me know if you need any adjustments!