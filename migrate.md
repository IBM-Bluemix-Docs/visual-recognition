---

copyright:
  years: 2019, 2020
lastupdated: "2020-12-01"

keywords: migrating

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Migrating
{: #migrating}

{{site.data.keyword.visualrecognitionfull}} is discontinued. Existing instances are supported until 1 December 2021, but as of 7 January 2021, you can't create instances. Any instance that is provisioned on 1 December 2021 will be deleted.
{: deprecated}

To migrate your current models (classifiers), provision a new instance of the {{site.data.keyword.visualrecognitionshort}} service. For custom models, retrain the model by creating another model (classifier) with the images from the earlier model.
{: shortdesc}

{{site.data.keyword.visualrecognitionfull}} service instances created **before** 23 May 2018 have a host URL of `gateway-a.watsonplatform.net`. You must migrate those instances to a new {{site.data.keyword.visualrecognitionshort}} service instance to continue to use them.
{: deprecated}

1.  Create another instance of the {{site.data.keyword.visualrecognitionshort}} service:
    1.  Go to the [{{site.data.keyword.visualrecognitionshort}}](https://{DomainName}/catalog/visual-recognition){: external} page in the catalog.
    1.  Select a plan and click **Create**.
1.  Copy the new credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` value.
1.  [Re-create and train your custom models](/docs/visual-recognition?topic=visual-recognition-tutorial-custom-classifier#tutorial-custom-classifier) in your new instance of the {{site.data.keyword.visualrecognitionshort}} service.
1.  Modify how you call your service.

    You provide either an Identity and Access Management (IAM) key or access token for your service instance. Tokens provide greater security because they must be periodically renewed and they support requests without your embedding service credentials in every call. API keys use basic authentication and do not expire.

    - For more information about tokens, see [Authenticating with IAM tokens](/docs/watson?topic=watson-iam#iam).
    - For more information about using an IAM API key, see the [API reference](https://{DomainName}/apidocs/visual-recognition/#authentication).
