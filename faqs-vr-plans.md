---

copyright:
  years: 2020, 2021
lastupdated: "2021-01-11"

keywords: faqs, Frequently Asked Questions, Visual Recognition faqs

subcollection: visual-recognition

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:deprecated: .deprecated}

---

# FAQs about {{site.data.keyword.visualrecognitionshort}} plans
{: #vr-plans-faqs}

{{site.data.keyword.visualrecognitionfull}} is discontinued. Existing instances are supported until 1 December 2021, but as of 7 January 2021, you can't create instances. Any instance that exists on 1 December 2021 will be deleted.
{: deprecated}

FAQs for {{site.data.keyword.visualrecognitionshort}} plans might include questions about plan features or pricing. To find all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).
{: shortdesc}

## What is the definition of event in a pricing plan?
{: #event}
{: faq}

Each image that you send for classification, detection, or training is an event.

## Am I charged for failed training requests?
{: #price-calc}
{: faq}

If a request for training or retraining images fails, that failed request does not result in any charges.  The cost is calculated based on successfully completed requests.

## Can I estimate my costs?
{: #estimate}
{: faq}

You can use the cost estimator to estimate your potential costs for planning purposes.  For more information, see [Estimating your costs](/docs/billing-usage?topic=billing-usage-cost).

After you start to use {{site.data.keyword.visualrecognitionshort}}, you can view the estimated costs for the services used per month from the [Usage](https://cloud.ibm.com/billing/usage) page in the console. For more information, see [Viewing your usage](/docs/billing-usage?topic=billing-usage-viewingusage).

## Are there limits to the number of image classifiers that I can build?
{: #build-limit}
{: faq}

- The Lite plan allows for 1,000 events (images) per month and the ability to train two Custom Models.
- For a Standard plan, you have unlimited image classifiers per month, with the pricing evaluated per event (image).
For more information about plan limits, see [the catalog page](https://{DomainName}/catalog/visual-recognition){: external}.

## What are the custom model features for the Lite plan?
{: #lite-custom}
{: faq}

The Lite plan gives you the ability to train two Custom Models at a time. If you want to change either of these two custom classifiers, or create a third one, then delete one of the existing custom classifiers.

If you change to a Standard plan, you can retrain a classifier as many times as needed and have unlimited image classifications per month.

## How many classes can I create with a Lite plan?
{: #lite-classes}
{: faq}

You can create as many classes as you need. However, you are limited to 1,000 events (images) and two custom classifiers with a Lite plan. For best results, use at least 50 images per class.

## For how long can I use a Lite plan?
{: #lite-duration}
{: faq}

Because {{site.data.keyword.visualrecognitionshort}} is discontinued, existing instances are supported only until 1 December 2021. As of 7 January 2021, you can't create instances. You must use your {{site.data.keyword.visualrecognitionshort}} Lite plan service every month to keep it available. Any instance that exists on 1 December 2021 will be deleted.

## Am I charged for exports to Core ML?
{: #core-ml}
{: faq}

Core ML downloads are free for either the Lite or Standard plan. In addition, downloading a Core ML model doesn't count toward the event limit.
There is no charge for off-line classification, in which you download the model and run classification on an iOS device.  There is a charge for training the model and online classification, in which you call and classify using the API.

## Are API keys part of the pricing plan?
{: #apikey}
{: faq}

There is no cost associated with creating multiple API keys per service.  You are charged, however, for the transactions made by each of your API keys.
