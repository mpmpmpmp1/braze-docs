---
nav_title: LILT
article_title: LILT
description: "This reference article outlines the partnership between Braze and LILT."
alias: /partners/lilt/
page_type: partner
search_tag: Partner
---

# LILT

> [LILT](https://lilt.com/) is the complete AI solution for enterprise translation and content creation. LILT enables global organizations to scale and optimize their content, product, communications, and support operations, with AI agents and fully automated workflows.

_This integration is maintained by LILT._

## About this integration
The LILT Braze Connector enables the translation of HTML email templates with AI speed and enterprise-grade quality. Request brand-aligned Instant Translation or quality-guaranteed Verified Translation and receive multilingual email content from LILT directly in Braze. 

## Use cases

The LILT Braze integration automates and accelerates the translation process, enabling global marketing teams to launch their multilingual campaigns quickly and with brand consistency.

**Global Campaign Launch Acceleration**: Launch marketing campaigns across multiple regions simultaneously without delays from manual translation handoffs.
- *Scenario*: Your company is launching a new product across 10 different countries.
- *Solution*: Your marketing team finalizes the master English email template in Braze, tags it with `LILT: Ready`, and the LILT Connector automatically pulls the content. Domain-specific linguists review the AI translation prompts in the LILT Platform for quality assurance, and the Connector pushes the translated versions back into Braze.
- *Benefit*: Reduces the time-to-market for your global campaigns from days to hours, ensuring all customers receive the new product announcement at the optimal time.

**Instant, Brand-Aligned Localization**: Use LILT's AI for immediate, on-brand translations for time-sensitive communications.
- *Scenario*: A flash sale, limited-time offer, or urgent service interruption email needs to be deployed in key five geographic markets immediately.
- *Solution*: You tag the email template with `LILT: Instant`. LILT uses its AI and linguistic assets specific to your company (e.g., terminology, style guides) to generate a high-quality, brand-consistent translation within minutes.
- *Benefit*: Allows for hyper-responsive, real-time communications without sacrificing brand voice or quality, which is critical for time-sensitive marketing.

## Prerequisites

Before you start, you need the following:

| Prerequisite       | Description |                        
|-----------------------|-----------------|
| A LILT account   | A LILT account is required to take advantage of this partnership.  |
| A Braze REST API key  | A Braze REST API key with the following permissions:<br>- `templates.email.create`<br>- `templates.email.update`<br>- `templates.email.info`<br>- `templates.email.list`<br>- `templates.translations.source.get`<br>- `templates.translations.update`<br>- `templates.translations.get`<br>- `templates.translations.all.get`. <br><br> Create this key in the Braze dashboard from **Settings** > **API Keys**. |
| A Braze REST endpoint | [Your REST endpoint URL]({{site.baseurl}}/developer_guide/rest_api/basics/#endpoints). Your endpoint depends on the Braze URL for your instance.  |
{: .reset-td-br-1 .reset-td-br-2 role=“presentation”}


## Integration

### Step 1: Configure the LILT <> Braze Connector

1. Log into LILT and click into Connect. Click “New Connector” and select Braze.
	
![Braze connector in LILT.]({% image_buster /assets/img/lilt/image 1 select connector.png %})

2. Select the desired localization workflow for your Braze content.

![Braze workflow in LILT.]({% image_buster /assets/img/lilt/image 2 select workflow.png %})	

3. Enter and verify the necessary configuration details:
- Your Braze API Key
- Braze REST endpoint

![Complete API Credentials.]({% image_buster /assets/img/lilt/image 3 api creds.png %})	

4. Click **Verify** to test the setup. Once the connection is confirmed, save the configuration.

### Step 2: Prepare your Braze workspace

1. Activate the multi-language capabilities within your Braze workspace settings.

![Set up locales in Braze.]({% image_buster /assets/img/lilt/image 4 lilt locales.png %})	

2. Create the following tags in Braze for your LILT workflow: 
- `LILT: Ready`
- `LILT: In progress`
- `LILT: Sent to LILT`
- `LILT: Delivered`
- `LILT: Needs Attention`
- `LILT: Instant`

![Set up LILT tags in Braze.]({% image_buster /assets/img/lilt/image 5 lilt tags.png %})	

### Step 3: Send content to LILT for translation 

1. Once the LILT <> Braze Connector is set up, use Liquid translation tags within your Braze email templates to identify content for translation. 
- Example:  {% translation id_0 %}Hello, {{first_name}}!{% endtranslation %}
2. Initiate translation by updating the template tag to indicate the desired workflow: 
- Choose `LILT: Ready` for Verified Translation
- Choose `LILT: Instant` for brand-aligned Instant Translation
3. The LILT <> Braze Connector runs at your preset timing to pull the tagged content into LILT. Track translation progress, as content tags automatically update in Braze to reflect the stage of your project. 
	
![Braze email template with translation tags.]({% image_buster /assets/img/lilt/image 6 braze templates.png %})	
