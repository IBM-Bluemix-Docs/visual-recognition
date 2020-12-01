---

copyright:
  years: 2020
lastupdated: "2020-12-01"

keywords: faqs, Frequently Asked Questions,Visual Recognition faqs

subcollection: visual-recognition

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}

---

# FAQs for {{site.data.keyword.visualrecognitionshort}}
{: #vr-use-faqs}

{{site.data.keyword.visualrecognitionfull}} is discontinued. Existing instances are supported until 1 December 2021, but as of 7 January 2021, you can't create instances. Any instance that is provisioned on 1 December 2021 will be deleted.
{: deprecated}

FAQs for {{site.data.keyword.visualrecognitionshort}} might include questions about custom models, images, or deleting data. To find all FAQs for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).
{: shortdesc}

## Can I build a custom model using a GUI?
{: #interface}
{: faq}

To work in a graphical interface where you can create your own custom models, use {{site.data.keyword.DSX}}. To learn more, watch the video [Get Started with  {{site.data.keyword.visualrecognitionshort}} in a {{site.data.keyword.DSX}} project](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/videos.html#vizrec){: external}, then follow the steps in [Getting started](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/get-started-wdp.html){: external} to sign up and start working.

## How are class and classifier defined?
{: #class-define}
{: faq}

To understand the difference between a "class" and a "classifier," let’s use dog breeds as an example. Each dog breed, such as Husky, Golden Retriever, and so on, is a class. "Dog Breed" is a classifier, defined as a group of classes. A custom classifier is a group of classes that are trained against each other.

## Does the number of images used to train the classifier affect performance?
{: #performance}
{: faq}

The performance of the {{site.data.keyword.visualrecognitionshort}} service is not affected by the number of images.  The image volume affects the time it takes to train, with more images resulting in a longer training time.  To maximize performance when you submit many images, review the [Guidelines for high volume classifying](/docs/visual-recognition?topic=visual-recognition-customizing#customizing-guidelines-classifying).

## What are the guidelines for negative images?
{: #negative}
{: faq}

A negative image defines what the classifier is **not**. The set of negative images should be visually similar to the positive examples, but not completely different. For example, if you are creating a classifier of "Fruits," your negative examples can consist of images of various vegetables. Keep in mind that negative examples in the same training are optional and are provided to refine your classifier. For additional information, see [Guidelines for training classfiers](/docs/visual-recognition?topic=visual-recognition-customizing).

## Can I delete images in a class or delete classes in a classifier after training?
{: #delete-after-train}
{: faq}

It is not possible to delete or remove images from an existing class. It is possible only to add images to a class.
If you need to delete or remove images from a class for any reason, you can create a new classifier, exclude the unwanted images, and train that newly created class.

## Can I delete data permanently? What data is stored?
{: #delete-data}
{: faq}

You can delete your data permanently. Uploaded photos are not saved to hard disk and are deleted from memory immediately after you send the request.  By default, IBM Watson services log these upload requests and their results.  You can choose to opt out of this logging as described in [Controlling request logging for Watson services](/docs/watson?topic=watson-gs-logging-overview).

## If I have multiple API keys, how many concurrent requests can I make?
{: #api-requests}
{: faq}

The concurrency request limit per API key is 20 to 30 requests. If you have multiple {{site.data.keyword.visualrecognitionshort}} API keys, each key has a limit of 20 to 30 concurrent requests for each {{site.data.keyword.visualrecognitionshort}} service instance. The concurrency is calculated separately.
