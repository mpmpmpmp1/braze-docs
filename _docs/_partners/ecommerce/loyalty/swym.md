---
nav_title: Swym
article_title: Swym
description: "This reference article outlines the partnership between Braze and Swym, that empowers shoppers to save products and seamlessly continue their journey across website, mobile app, and retail stores."
alias: /partners/swym/
page_type: partner
search_tag: Partner
---

<!-- In most cases, the ARTICLE_TITLE will be your company name. If your tool requires several separate pages on Braze Docs, you can add a relevant page descriptor to your title, such as "MyCompany Analytics." -->
# Swym

<!-- The description starts with a '>' character and contains an introduction to your company, a link to your main site, and a concise overview of your integration. In a following paragraph, highlight the the relationship between your company and Braze and how this partnership helps your customers. -->
> [Swym](https://getswym.com) helps ecommerce brands capture shopping intent with Wishlists, Save for Later, Gift Registry, and Back-in-Stock alerts. Using rich, permission-based data, merchants can craft hyper-targeted campaigns and deliver personalized shopping experiences that drive engagement, boost conversions, and increase loyalty.

*This integration is maintained by Swym.*

## About the integration

The Swym + Braze integration empowers merchants to deliver highly personalized, event-driven marketing campaigns that convert shopper intent into sales. The merchants leverage our platform to make it easy for shoppers to pick up where they left off, to collaborate with others throughout their shopping journey and to deploy high performance retargeting campaigns

<!-- Most partner integrations will require the following prerequisites. However, you may add additional prerequisites as needed. -->
## Prerequisites

Before you start, you'll need the following:

| Prerequisite          | Description                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Swym  | Swym Wishlist Plus and/or Back in stock app(s) installed in your ecommerce platform (Shopify/BigCommerce) and you are on the Enterprise plan.              |
| A Braze REST API key  | A Braze REST API key with `users.track` permissions. <br><br> This can be created in the Braze dashboard from **Settings** > **API Keys**. |
| A Braze REST endpoint | [Your REST endpoint URL](https://www.braze.com/docs/api/basics/#endpoints). Your endpoint will depend on the Braze URL for your instance.                                                 |
{: .reset-td-br-1 .reset-td-br-2}

<!-- An optional section you can use to outline the typical or atypical use cases for your integration. -->
## Use cases

By connecting Swym’s Wishlist Plus and Back in Stock Alerts apps with Braze, merchants can automatically send shopper activity events—such as wishlist adds, back-in-stock subscriptions, price drop alerts, and reminders—into Braze as custom events. These events can then be used to trigger automated email and SMS campaigns via Braze Canvases, ensuring timely, relevant, and engaging communication that brings shoppers back to purchase.

<!-- Create step-by-step instructions for integrating your tool with Braze. It's important to be concise and only outline the minimum necessary steps. -->
## Integrating Swym

### Step 1: Connect your Swym app to Braze

At present, the Braze integration with Swym is not self-serve—it’s a managed integration. To get started, please reach out to support@getswym.com and provide the following details so that Swym can set up the integration on your behalf:

*a. API key:* Generate an API key in your Braze dashboard:

Settings > APIs and Identifiers > Create API Key

- While creating the key, make sure to enable the `users.track` permission under User Data.

- For step-by-step guidance, you can refer to the [Braze API Guide](https://www.braze.com/docs/api/basics/#about-rest-api-keys).

![An image of Generating API key from Braze.]({% image_buster /assets/img/swym/braze-api-key.png %})

**Important:** Please share credentials securely using [OneTimeSecret](https://onetimesecret.com/) (a one-time, self-destructive link tool) to keep your API keys protected.

*b. Instance URL:* Braze manages a number of different instances for our dashboard and REST endpoints. Please share the correct REST endpoint based on which instance you are provisioned to. You can refer to [this API guide](https://www.braze.com/docs/api/basics/#endpoints) from Braze for further help.

Once the API key and Instance URL has been shared with Swym's Support team, they will set up the integration for you and respond with a confirmation.

After the setup is completed, the custom events from Swym will be automatically registered in Braze. You can verify the integration by checking the Custom Events section in the Braze dashboard.

- In the dashboard open Data Settings > Custom Events to view the list of Swym events registered.

- The properties of each Swym event can be viewed by choosing Manage properties against each custom event.

- These properties hold the values of the events that we send out which can be rendered in the Email/ SMS templates.

- If the custom events appear, it confirms that your Swym app is successfully communicating with your Braze account.

![An image of custom properties in Braze.]({% image_buster /assets/img/swym/braze-custom-properties.png %})

### Step 2: Subscribe to events you want to send

From your Wishlist Plus app, head over to the Marketing tab and scroll to the “Automations” section. Here, you will notice various events that you can subscribe to. Enable the desired events.

![An image of Events to be subscribed.]({% image_buster /assets/img/swym/braze-event-subscription.png %})

**Swym Wishlist Plus App Events:**

| Event Name | When this event is triggered |  
|------------|------------------------------|  
| Share Wishlist | When a shopper shares a wishlist with someone else |  
| Add to Wishlist | When a shopper adds an item to their wishlist |  
| Wishlist Reminder | Reminder about items in a shopper’s wishlist|   
| Saved for Later Reminder | Reminder about a shopper’s Saved for Later items |  
| Price Drop alert | Product on a wishlist goes on sale |  
| Low Stock alert | Product on a wishlist is running low on stock |  
| Back in Stock alert | Product on a wishlist is restocked |  

 
**Swym Back in Stock Alerts App Events:**

| Event Name | When this event is triggered |  
|------------|------------------------------|  
| Back in Stock Acknowledgement | Shopper subscribes to be notified when a product is back in stock |  
| Restock Alert | Product a shopper requested a back-in-stock alert for is restocked |  
| Restock Reminder | Follow-up alert (usually ~24 hrs after the first restock alert, configurable)|   

 

### Step 3: Create Canvas(es) in Braze

You will have to build a separate Canvas for each of the events you subscribed to in order to automate sending out personalised emails to your shoppers.

1. Navigate to Braze Dashboard > Messaging > Canvas and start creating a new Canvas.

2. In the Trigger section, select Custom Event as the trigger for your flow.

3. Choose Swym events for which you would like to build the Canvas.

4. To send out an email/ SMS, drag and drop the Message component from the sidebar into the Canvas and select Email/ SMS channel as per your need.

5. In Canvas, custom event properties can be used in Liquid in any Message step that follows an Action Paths step. For example, when referencing `event_properties`, use this Liquid snippet: `{{event_properties.${property_name}}}`.
   
![An image of action based event]({% image_buster /assets/img/swym/braze-canvas-setup.png %})

For detailed information refer to [Swym help center](https://help.getswym.com/en/articles/12344153-braze-integration)
