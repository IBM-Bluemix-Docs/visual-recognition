---

copyright:
  years: 2019, 2020
lastupdated: "2020-01-30"

keywords: visual recognition,activity,tracker,events,API,public API,subscription,binding

subcollection: visual-recognition

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:table: .aria-labeledby="caption"}

# Activity Tracker events
{: #at_events}

When you have {{site.data.keyword.visualrecognitionshort}} provisioned as a service in your {{site.data.keyword.cloud_notm}} account, you can see the following events in the [{{site.data.keyword.cloud_notm}} Activity Tracker with LogDNA](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).
{: shortdesc}

## List of events
{: #at-pubapi}

| Action | Description |
| -- | -- |
| watson-vision-combined.classifiers-core-ml-model.get | Retrieve a Core ML model file of a classifier |
| watson-vision-combined.classifiers.post | Train a new multi-faceted classifier on the uploaded image data |
| watson-vision-combined.classifiers.delete | Delete a classifier |
| watson-vision-combined.user-data.delete | Delete all data associated with a specified customer ID |
| watson-vision-combined.collection-images.get | Retrieve an image from a collection |
| watson-vision-combined.collection-images.post | Add an image to a collection |
| watson-vision-combined.collection-images.delete | Delete an image from a collection |
| watson-vision-combined.collection.delete | Delete all data associated with a specified image collection |

## Where to view events
{: #at-view}

Activity Tracker events are available in the Activity Tracker **account domain** that is available in the {{site.data.keyword.cloud_notm}} region where the events are generated.
