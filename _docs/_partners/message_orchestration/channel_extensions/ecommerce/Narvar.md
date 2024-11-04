# Narvar

Narvar is a post-purchase platform that enhances customer loyalty through order tracking, delivery updates, and returns management.

The Braze and Narvar integration enables brands to leverage Narvar’s notification events to trigger messages directly from Braze, keeping customers informed with timely updates.

# Prerequisites

| Requirement           | Description                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------|
| Narvar Account        | A Narvar account is required to take advantage of this partnership.                           |
| Braze REST API key    | A Braze REST API key with messages.send permission.                                           |
| Braze REST endpoint   | Your REST endpoint URL. Your endpoint will depend on the Braze URL for your instance.         |

### Integration Scope

#### Supported Notifications:

The integration currently supports the following Narvar notification events:
- Delivery Anticipation
- Carrier Delay
- Delivered Standard

#### Supported Channels

- Push Notifications

If you’re interested in additional notification types or channels, please contact your Braze and Narvar CSM.

### Integration Details

For each notification event, Narvar directly makes a request to Braze’s /messaging/send endpoint to send a push message for each opted-in consumer.

Currently, Narvar directly configures the push notification payloads for each message, as there is no push notification design interface in Narvar. The Narvar team will align with your team on payload requirements. Payloads are customizable to the same degree as if you were sending the events through your own system, including support for variable content placeholders (e.g., order data, consumer details).

### Getting Started with the Braze-Narvar Integration

1. **Contact your Narvar CSM** to express interest in the integration.
2. **Designate Braze environments** for staging and production.
3. **Generate API Key** in Braze for Narvar’s use.
4. **Generate Campaign Key(s)** in Braze as needed.
5. **Provide API and Campaign keys** to Narvar through a secure one-time link.
6. **Share Push Notification Payload Details** to finalize setup.