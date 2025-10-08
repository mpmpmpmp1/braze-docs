---
nav_title: Swym
article_title: Swym
description: "This reference article outlines the partnership between Braze and Swym, that empowers shoppers to save products and seamlessly continue their journey across website, mobile app, and retail stores."
alias: /partners/swym/
page_type: partner
search_tag: Partner
layout: dev_guide
---

# Swym

> [Swym](https://getswym.com) helps ecommerce brands capture shopping intent with Wishlists, Save for Later, Gift Registry, and Back-in-Stock alerts. Using rich, permission-based data, merchants can craft hyper-targeted campaigns and deliver personalized shopping experiences that drive engagement, boost conversions, and increase loyalty.

*This integration is maintained by Swym.*

## About the integration

The Swym and Braze integration empowers merchants to deliver highly personalized, event-driven marketing campaigns that convert shopper intent into sales. Merchants can leverage the integration to make it easy for shoppers to pick up where they left off, to collaborate with others throughout their shopping journey and to deploy high performance retargeting campaigns.

## Prerequisites

Before you start, you'll need the following:

| Prerequisite          | Description                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Swym  | Swym Wishlist Plus and/or Back in Stock app(s) must be installed on your e-commerce platform (Shopify or BigCommerce), and you must be on the Enterprise plan.       |
| A Braze REST API key  | A Braze REST API key with `users.track` permissions. <br><br> This can be created in the Braze dashboard from **Settings** > **API Keys**. |
| A Braze REST endpoint | [Your REST endpoint URL](https://www.braze.com/docs/api/basics/#endpoints). Your endpoint will depend on the Braze URL for your instance.                                                 |
{: .reset-td-br-1 .reset-td-br-2}

## Use cases

By connecting Swym’s Wishlist Plus and Back in Stock Alerts apps with Braze, merchants can automatically send shopper activity events such as wishlist adds, back-in-stock subscriptions, price drop alerts, and reminders, into Braze as custom events. These events can then be used to trigger automated messages in Braze, ensuring timely, relevant, and engaging communication that brings shoppers back to purchase.

## Integrating Swym

### Step 1: Connect your Swym app to Braze

Currently, the Braze integration with Swym is a managed integration and is not self-serve. To get started, contact support@getswym.com and provide the following information so that Swym can set up the integration on your behalf:

1. Generate a REST API key in your Braze dashboard with the `users.track` permission. For step-by-step guidance, you can refer to the [Braze API Guide](https://www.braze.com/docs/api/basics/#about-rest-api-keys).

![An image of Generating API key from Braze.]({% image_buster /assets/img/swym/braze-api-key.png %})

{% alert important %}
Please share credentials securely using [OneTimeSecret](https://onetimesecret.com/) (a one-time, self-destructive link tool) to keep your API keys protected.
{% endalert %}

2. Braze manages multiple instances for its dashboard and REST endpoints. Please provide the correct REST endpoint for the instance you are provisioned. For guidance, refer to the [Braze API Guide](https://www.braze.com/docs/api/basics/#endpoints).

3. Once the API key and Instance URL has been shared with Swym's Support team, they will set up the integration for you and respond with a confirmation.

4. After the setup is completed, the custom events from Swym will be automatically registered in Braze. You can verify the integration by checking the Custom Events section in the Braze dashboard.

- In the Braze dashboard, navigate to *Data Settings > Custom Events* to view the list of Swym events that are registered.

- To view the properties of each Swym event, select Manage Properties for the corresponding custom event.

- These properties contain the event values that can be used to personalize your messages.

- If the custom events appear, it confirms that your Swym app is successfully connected with your Braze account.

![An image of custom properties in Braze.]({% image_buster /assets/img/swym/braze-custom-properties.png %})

### Step 2: Subscribe to events you want to send to Braze

From your Wishlist Plus app, go to the Marketing tab and find the Automations section. Here, you will enable the events you want to subscribe to. 

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

 

### Step 3: Create a Braze Campaign or Canvas

You will have to build a separate Campaigan or Cavnas for each of the events you subscribed to in order to automate sending out personalised messages to your shoppers. For step-by-step guidance, you can refer to [Braze's documentation](https://www.braze.com/docs/user_guide/getting_started/campaigns_canvases/#campaigns)).
   
![An image of action based event]({% image_buster /assets/img/swym/braze-canvas-setup.png %})

For detailed information refer to the [Swym help center](https://help.getswym.com/en/articles/12344153-braze-integration) or contact support@getswym.com. 
