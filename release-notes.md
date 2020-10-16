---

copyright:
  years: 2019, 2020
lastupdated: "2020-10-16"

keywords: new features,updates,what's new,changelog,change log,release notes,visual recognition release notes

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

# Release notes
{: #release-notes}

The following new features and changes to the service are available.
{: shortdesc}

## Service API Versioning
{: version}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2018-03-19`.

## Beta features
{: #beta}

{{site.data.keyword.IBM_notm}} releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment.

## Changes
{: #changelog}

The following new features and changes to the service are available.

### 16 October 2020
{: #16october2020}

You can no longer create a Lite plan instance of the {{site.data.keyword.visualrecognitionshort}} service. However, existing Lite plan instances remain available.  You can create new instances as billable Standard plans.

### 28 April 2020
{: #28april2020}

- **Android support for object detection**

    You can now download custom object detection models to use in your Android apps.

    - For more information about the method, see **Get a model** in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v4#get-a-model){: external}.
    - For an example app and sample model, see [{{site.data.keyword.visualrecognitionshort}} on Android](https://github.com/matt-ny/rscnn){: external}.

### 20 March 2020
{: #20march2020}

- **New Germany location**
    - You can now create {{site.data.keyword.visualrecognitionshort}} instances in the Frankfurt location.

### 12 December 2019
{: #12december2019}

- **Full support for IBM Cloud IAM**

    - {{site.data.keyword.visualrecognitionshort}} now supports the full implementation of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). API keys for Watson services are no longer limited to a single service instance. You can create access policies and API keys that apply to more than one service, and you can grant access between services.
    - To support this change, the API service endpoints use a different domain and include the service instance ID. The pattern is `api.{location}.{offering}.watson.cloud.ibm.com/instances/{instance_id}`.

        Example URL for an instance hosted in the Dallas location: `api.us-south.visual-recognition.watson.cloud.ibm.com/instances/6bbda3b3-d572-45e1-8c54-22d6ed9e52c2`

        The previous public endpoint domain was `watsonplatform.net`.

        For more information about the URLs, see the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3#service-endpoint){: external}.

        These URLs do not introduce a breaking change. The new URLs work both for your existing service instances and for new instances. The original URLs continue to work on your existing service instances for at least one year (until December 2020).
    - For more information about IAM, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).
- **New network and data security features** (not supported for VisRec)
    - **Support for data encryption with customer-managed keys**
        - Users of Premium plans can integrate {{site.data.keyword.keymanagementservicefull}} with {{site.data.keyword.visualrecognitionshort}} to encrypt their data and manage encryption keys. For more information, see [Protecting sensitive information in your Watson service](/docs/watson?topic=watson-keyservice).
    - **Support for private network endpoints** (not supported for VisRec)
        - Users of Premium plans can create private network endpoints to connect to {{site.data.keyword.visualrecognitionshort}} over a private network. Connections to private network endpoints do not require public internet access. For more information, see [Public and private network endpoints](/docs/watson?topic=watson-public-private-endpoints).

### 13 November 2019
{: #13november2019}

- Updates to v4 of the API
    - **New endpoint: Get training usage**

        To see how many v4 (Custom Object Detection) training events have occurred in your account, you can run the **Get training usage** (`GET /v4/training_usage`) endpoint. For details, see the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v4#get-training-usage).

    - **New image size: Download a thumbnail version**

        With the **Get a JPEG file of an image** endpoint in v4 of the API (`GET /v4/collections/{collection_id}/images/{image_id}/jpeg`), you can now download a thumbnail version of your images by specifying `size=thumbnail`. The full size version remains the default. For more information, see the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v4#get-a-jpeg-file-of-an-image).

- **New South Korea location**
    - You can now create {{site.data.keyword.visualrecognitionshort}} instances in the Seoul location.

        {{site.data.keyword.DSX}} does not support the Seoul location, so service instances that you create outside of {{site.data.keyword.DSX}} are not available in that tool.

### 7 October 2019
{: #7october2019}

- **General availability of Custom Object Detection**

    The Custom Object Detection features moved from Beta to General availability (GA). Custom Object Detection identifies items and their location in an image.

    For more information, see [Custom Object Detection Generally Available](https://medium.com/ibm-watson/ibm-watson-visual-recognition-custom-object-detection-generally-available-906b2ae77969){: external} in the <em>IBM Watson blog</em>.

### 12 September 2019
{: #12september2019}

- **Detect faces methods removed**

    As of 12 September 2019, the **Detect Faces** methods are removed from {{site.data.keyword.visualrecognitionshort}}. These methods include `GET /v3/detect_faces` and `POST /v3/detect_faces`.
- **Text recognition in natural scenes closed**

    As of 11 September 2019, the Text model private beta feature is closed. There are no plans for another beta or general release.

### 16 August 2019
{: #16august2019}

- **Custom Object Detection avaiable in Beta**
    - Custom Object Detection identifies items and their location in an image. The service detects these items based on a set of images with labeled training data that you provide. For details, see [Custom Object Detection (Beta)](/docs/visual-recognition?topic=visual-recognition-object-detection-overview)
    - Custom Object Detection is supported by the [Visual Recognition v4 API (Beta)](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v4){: external}

### 21 March 2019
{: #21march2019}

- **Change to viewing service credentials**
    - Users can now see service credential information only that is associated with the role assigned to your {{site.data.keyword.cloud_notm}} account. For example, if you are assigned a `reader` role, any `writer` or higher levels of service credentials are not visible.

        This change does not affect API access for users or applications with existing service key credentials. Only the viewing of credentials within {{site.data.keyword.cloud_notm}} is affected.

        For more information about service keys and user roles, see [Authenticating to Watson services](/docs/watson?topic=watson-iam).

### 15 January 2019
{: #15january2019}

- **Translation for gender in Detect Faces**
    - The **Detect Faces** methods now return translated labels for "Male" and "Female" when you provide the language in the **Accept-Language** request header. For details see the [API reference](https://{DomainName}/apidocs/visual-recognition#detect-faces-in-images){: external}.

### 1 October 2018
{: #01october2018}

- **Service instances created before May 23, 2018 are deleted.**

    - As previously notified, all {{site.data.keyword.visualrecognitionshort}} instances created before May 23, 2018 are no longer active. Data from the instances is now deleted. See [Migrating](/docs/visual-recognition?topic=visual-recognition-migrating#migrating) for details about how to move to a new service instance.
    - Service instances created after this date are not affected.
    - If you have any questions, contact [IBM support](https://cloud.ibm.com/login?redirect=/unifiedsupport/supportcenter){: external}.

### 1 August 2018
{: #01august2018}

- **General availability of Food and Explicit models**

    The Food and Explicit models moved from Beta to General availability (GA). The Food model recognizes more food and meals than the General (default) model. The Explicit model identifies what might be considered pornographic images.

    No code change are required. Both models are free under the Lite plan and cost $0.002 per image under the Standard plan.

    For more information, see [Updates to Watson Visual Recognition](https://www.ibm.com/blogs/watson/2018/06/updates-to-ibm-watson-visual-recognition-%E2%80%A8price-reduction-for-custom-classification-%E2%80%A8food-and-explicit-model-are-now-ga/){: external} in the <em>Watson blog</em>.

### 1 July 2018
{: #01july2018}

- **New pricing for custom models**
    - Starting July 1, 2018, classifying an image with a custom model costs half the earlier rate and is now $0.002 per image. For details and other important information, see [Updates to Watson Visual Recognition \- Price reduction for Custom Classification](https://www.ibm.com/blogs/watson/2018/06/updates-to-ibm-watson-visual-recognition-%E2%80%A8price-reduction-for-custom-classification-%E2%80%A8food-and-explicit-model-are-now-ga/){: external} in the <em>Watson blog</em>.

### 21 June 2018
{: #21june2018}

- **Additional language support**

    - The **Classify** methods now support Chinese (Simplified and Traditional) and Portuguese (Brazilian) in the output of `default` (General) model classes. For the full list of languages, see [Supported languages](/docs/visual-recognition?topic=visual-recognition-language-support-top#language-support-top).
    - All languages are now also supported in the responses from the **Food** and **Explicit** models.


### 22 May 2018
{: #22may2018}

- **New API authentication process**

    You now authenticate with Identity and Access Management (IAM) at a new endpoint:

    - Use a different endpoint URL for new instances. The default endpoint is `https:/gateway.watsonplatform.net/visual-recognition/api/`. To find the URL for your service instance, check the credentials by clicking the instance from the {{site.data.keyword.cloud_notm}} [Resource list](https://{DomainName}/login?redirect=%2Fresources){: external}.
    - Modify how you authenticate to the API. You provide either an IAM key or access token for your service instance. See [Migrating](/docs/visual-recognition?topic=visual-recognition-migrating#migrating) for examples.

    For service instances created before May 23, 2018, the authentication process and endpoint have not changed. Authenticate by providing the `api_key` query parameter.

- **Updates to the Lite plan**

    Lite plans created after May 22, 2018 are changing:

    - New Lite plan instances continue to be available after 30 days if you use them every month.
    - You can create and retrain two custom models under the new Lite plan.
    - Lite plans include up to 1,000 events a month. Each image that you send for classification, detection, or training is an event. Downloading a Core ML model doesn't count toward the event limit.

    If your needs exceed the Lite plan, update to a billable account. [Explore](https://{DomainName}/catalog/visual-recognition){: external} the pricing plans.

- **Information security**

    We updated the documentation to include some new details about data privacy. Read the details in [Information security](/docs/visual-recognition?topic=visual-recognition-information-security#information-security).

### 12 April 2018
{: #12april2018}

- **Support for retraining a custom model on the Lite plan**

    Under the Lite plan, you no longer have to delete and create another custom model when you want to update or retrain the model. You can now update a custom model as long as you remain under daily and monthly [limits](https://{DomainName}/catalog/visual-recognition){: external} of the plan.

    If you need to have multiple models or multiple versions of the same model, update from the Lite plan to a billable account.

- **New minor version with support for CORS**

    **Version:** `2018-03-19`

    We now support Cross-Origin Resource Sharing (CORS) headers when you specify `version=2018-03-19` in requests.

### 5 April 2018
{: #5april2018}

- **Fix for Face model score issue**

  The range for the age score in the Face model is restored to the original range of 0 to 1. For details, see the [Known issues](#2april2018) for 2 April 2018.

- **New form-data parameters**

    The **Classify images** and **Detect faces in images** methods support new form-data parameters. Classify images supports separate `url`, `classifier_ids`, `threshold`, and `owners` parameters, and Detect faces supports `url`.

    In the past, you encoded the values in a JSON string and passed the **parameters** form-data parameter. You can use the new method of passing these values in separate form-data parameters for all application development. For details, see the [API reference](https://{DomainName}/apidocs/visual-recognition){: external}.

### 2 April 2018
{: #2april2018}

- **General availability of enhanced Face model**

    The updated face detection model is now in General availability (GA).

    This enhanced model uses broader training data sets for increased accuracy of facial detection for age and gender. For example, age predictions are improved by reducing the range between `min` and `max`. The fixed 9-year age range in the previous model is replaced with a dynamic and smaller range. The average age range is now 4.9 years.

    - Changes to the API

    Other differences between the enhanced and previous Face model:
        - The enhanced model supports .gif and .tif image formats.
        - The enhanced model supports larger file sizes: up to 10 MB for image files and up to 100 MB for .zip files.
        - The enhanced model does not include `FaceIdentity` information in the response. The identity information refers to the `name` of the person, `score`, and `type_hierarchy` knowledge graph.

    For details about the API, see the [API reference](https://{DomainName}/apidocs/visual-recognition/#detect-faces-in-images){: external}.

    - Known issues

        - Form parameters cannot include the **Content-Type**. For example, this request fails to analyze the **url** parameter because it includes `;type=text/plain`:

            ```bash
            curl -F url="https://example.com/images/prez.jpg;type=text/plain" \
            "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/detect_faces?api_key={api-key}&version=2016-05-20"
            ```
            {: pre}

        - The age score has a range of 0 to 0.3. We are working to restore the original range of 0 to 1.

    - Beta endpoint deprecated

    The beta endpoint at `/v3/detect_faces_beta` is deprecated and will not be accessible after May 17, 2018. Make sure that your requests point to `/v3/detect_faces`.

### 20 March 2018
{: #20march2018}

- **Integration with Apple Core ML**

    {{site.data.keyword.visualrecognitionshort}} now includes support for the Apple Core ML model format. You can use a Core ML version of your {{site.data.keyword.visualrecognitionshort}} model on your iOS apps.

    **Start developing**: To get started developing with {{site.data.keyword.visualrecognitionshort}} and Core ML, check out these projects on GitHub:

    - Classify images locally: [{{site.data.keyword.visualrecognitionshort}} with Core ML](https://github.com/watson-developer-cloud/visual-recognition-coreml){: external}.
    - Integrate {{site.data.keyword.discoveryfull}} with the results: [{{site.data.keyword.visualrecognitionshort}} and Discovery with Core ML](https://github.com/watson-developer-cloud/visual-recognition-with-discovery-coreml){: external}.
    - Explore the SDK: [Swift SDK](https://github.com/watson-developer-cloud/swift-sdk){: external}.

- **Changes to the API**

    The following backward-compatible changes to the API are included in the integration:

    - A new `core_ml_enabled` field that indicates whether a classifier model can be downloaded as a Core ML model. The field is returned in the response for calls to `GET and POST /v3/classifiers` and `GET /v3/classifiers/{classifier_id}`.
    - A new `GET /v3/classifiers/{classifier_id}/core_ml_model` method to download a Core ML model as an .mlmodel file.  You can download Core ML model files for custom models created after March 19.
    - A new `updated` field with the latest training date of the model. The `updated` field matches either the `retrained` field or the `created` field.

    For details about the API changes for Core ML, see the [API reference](https://{DomainName}/apidocs/visual-recognition#retrieve-a-core-ml-model-of-a-classifier){: external}.

- **New tool available: Watson Studio**

    [Watson Studio](https://dataplatform.cloud.ibm.com/registration/stepone?target=watson_vision_combined&context=wdp&apps=watson_studio&cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_VisualRecognition-_-docs){: external} is the new integrated environment that includes a replacement for the beta {{site.data.keyword.visualrecognitionshort}} tool. Watson Studio supports not only {{site.data.keyword.visualrecognitionshort}} but also many other {{site.data.keyword.cloud_notm}} services and resources. You can use Watson Studio with all your existing {{site.data.keyword.visualrecognitionshort}} instances and classifiers.

     Watson Studio provides a collaborative environment in the cloud. With Watson Studio, developers, subject matter experts, data scientists, and others can build and train {{site.data.keyword.visualrecognitionshort}} and other AI models. You can also use Watson Studio to access the built-in General and Face models.

     Watson studio also supports Core ML. You can download a Core ML model file for your custom model.

    [Get started](https://dataplatform.cloud.ibm.com/registration/stepone?target=watson_vision_combined&context=wdp&apps=watson_studio&cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_VisualRecognition-_-docs){: external} with Watson Studio.

- **Updated deep learning architecture for custom models**

    {{site.data.keyword.visualrecognitionshort}} now uses a faster and more efficient deep learning network architecture for classification. The updated models also can differentiate more strongly between the top class and the rest of the classes. This approach might result in somewhat longer training times. The new architecture is used to train new custom models. When you retrain existing older models, the original architecture is used.

    The following example shows the differentiation with the new architecture:

    ![Man archery bow and arrow. Photo by Annie Spratt on Unsplash](images/archery.jpg)

    <table>
      <tr>
        <th>Original class and score</th>
        <th>Updated class and score</th>
      </tr>
      <tr>
        <td>Archery</br>0.99 </td>
        <td><strong>archery<strong></br>0.9</td>
      </tr>
      <tr>
        <td>Auto Racing</br>0.996398</td>
        <td><strong>biking</strong></br>0.004</td>
      </tr>
      <tr>
        <td>Biking</br>0.0500174</td>
        <td><strong>fishing</strong></br>0.001</td>
      </tr>
      <tr>
        <td>Fishing</br>0.11029</td>
        <td><strong>golf</strong></br>0.031</td>
      </tr>
      <tr>
        <td>Golf</br>0.0980796</td>
        <td><strong>gymnastics</strong></br>0.029</td>
      </tr>
      <tr>
        <td>Gymnastics</br>0.964391</td>
        <td><strong>judo</strong></br>0.021</td>
      </tr>
      <tr>
        <td>Judo</br>0.339119</td>
        <td><strong>racing</strong></br>0.002</td>
      </tr>
      <tr>
        <td>Skating</br>0.0393602</td>
        <td><strong>skating</strong></br>0.061</td>
      </tr>
      <tr>
        <td>Skiing</br>0.0310527</td>
        <td><strong>skiing</strong></br>0.003</td>
      </tr>
      <tr>
        <td>Track and Field</br>0.208147</td>
        <td><strong>track</strong></br>0.035</td>
      </tr>
    </table>

- **French language support**

    The **Classify** methods now support French in the output of `default` model classes. For the full list of languages, see [Supported languages](/docs/visual-recognition?topic=visual-recognition-language-support-top#language-support-top).

### 23 February 2018
{: #23february2018}

- **Enhanced Face model available in beta**

    An updated face detection model is available. This beta model uses broader training data sets for increased accuracy of facial detection for age and gender. For more information, see [Increasing the Accuracy of IBM’s Watson {{site.data.keyword.visualrecognitionshort}} service](https://www.ibm.com/blogs/watson/2018/02/increasing-accuracy-ibms-watson-visual-recognition-service/){: external} and [Mitigating Bias in AI Models](https://www.ibm.com/blogs/research/2018/02/mitigating-bias-ai-models/){: external}.

    - The beta model is available at `/v3/detect_faces_beta`.

    Differences between the beta and general availability (GA) models:
    - The beta model supports .gif and .tif image formats; this enhancement is expected to be applied to the GA model.
    - The beta model supports larger file sizes: up to 10 MB for image files and up to 100 MB for .zip files. This enhancement is expected to be applied to the GA model.
    - Beta face detection does not include `FaceIdentity` information in the response.
    - The beta model's POST request requires a non-empty filename. The GA Face model does not enforce this constraint.
    - The beta model's POST request supports a separate form parameter called `url`. The GA model encloses that information in the `parameters` JSON object. For details, see the [API explorer](https://{DomainName}/apidocs/visual-recognition/#detect-faces-in-images){: external}.

- **Face identity deprecated**

    The identity information in the response of the GA Face model is deprecated and will be removed from the API on **April 2, 2018.** The identity information refers to the `name` of the person, `score`, and `type_hierarchy` knowledge graph.

### 16 January 2018
{: #16january2018}

- **Lite account and plan replaces the Free plan**

    A Lite account is free; no credit card is required. However, Lite plan service instances are deleted after 30 days.

    The maximum number of API calls that you can make with the Lite plan is slightly different from the Free plan. You can make a maximum of 7,500 API calls per month at 250 calls per day on the Lite plan.

    To update to a billable account when you have custom classifiers, create another service instance and re-create your custom classifiers.

### 11 December 2017
{: #11december2017}

<ul>
  <li>
    <strong>Increased accuracy and output with the General model</strong>
      <p>
        The General model, which contains several thousand tags, now detects more secondary objects and has improved scene detection. These improvements help recognize the less prominent aspects of an image. In addition, the average number of tags returned per image has increased to 10.
      </p>
      <p>
        The following image shows an example of the tags returned before the update and the additional tags that are now returned.
      </p>
      <img src="images/tree-flower.jpg" alt="Photograph of azalea plant">
      <table>
        <tr>
          <th>Original tags</th>
          <th>Additional tags</th>
        </tr>
        <tr>
          <td></td>
          <td>
          Tag: tree<br/>
          Score: 0.799</td>
        </tr>
        <tr>
          <td></td>
          <td>
          Tag: flower<br/>
          Score: 0.792</td>
        </tr>
        <tr>
          <td>
          Tag: alpine azalea<br/>
          Score: 0.696</td>
          <td></td>
        </tr>
        <tr>
          <td>
          Tag: plant<br/>
          Score: 0.868</td>
          <td></td>
        </tr>
        <tr>
          <td>
          Tag: azalea<br/>
          Score: 0.617</td>
          <td></td>
        </tr>
        <tr>
          <td>
            Tag: swamp azalea<br/>
          Score: 0.5</td>
          </td>
          <td></td>
        <tr>
          <td>
            Tag: reddish orange color<br/>
          Score: 0.1</td>
          </td>
          <td></td>
        </tr>
      </table>
    <li>
      <strong>New Explicit model available in beta</strong>
      <p>
        The Explicit model, which launches in beta, classifies whether an image contains pornographic content and is inappropriate for general use. You can include the Explicit model with other models for combined analysis. For example, include both the `default` and `explicit` classifier IDs in your request to return image tags and whether the image contains explicit content.
      <p>
        For details about the API call, see the **Classify images** method in the [API reference](https://{DomainName}/apidocs/visual-recognition/#classify-images){: external}.
      </p>
    </li>
    <li>
      <strong>Support for larger file sizes</strong>
      <p>
        The <strong>Classify images</strong> methods now support image files up to 10 MB and .zip files up to 100 MB.
    </li>
    <li>
      <strong>Array required when passing classifier IDs</strong>
      <p>
        The API now enforces an array when you pass in `classifier_ids` as part of the **parameters** object in the **Classify images** method. Previously, you could pass a classifier ID as a string. For more information, see the parameters description and example file in the [API reference](https://{DomainName}/apidocs/visual-recognition/#classify-images){: external}.
      </p>
    </li>
</ul>

### 8 September 2017
{: #8september2017}

- **Beta Similarity Search and collections closed**: As of September 8, 2017, the beta period for Similarity Search is closed. For more information, see [Visual Recognition API – Similarity Search Update](https://www.ibm.com/blogs/cloud-archive/2017/08/visual-recognition-api-similarity-search-update/){: external}.

### 30 June 2017
{: #30june2017}

- **Improved tagging**: We increased the number of training images for the default classifier. That increase improve the ability to recognize accurately the overall ‘scene’ of an image. For details, see [Further Enhancements for General Tagging Feature](https://www.ibm.com/blogs/cloud-archive/2017/07/watson-visual-recognition-sees-enhancements-general-tagging-feature/){: external}
- **Additional languages**: The **Classify images** method now supports Korean, Italian, and German in addition to English, Arabic, Spanish, and Japanese.

    For details about the API call, see the **Classify an image** method in the [API reference](https://{DomainName}/apidocs/visual-recognition/#classify-images){: external}.

### 16 May 2017
{: #16may2017}

- **New food classifier is available: Beta**

    A new beta food recognition model provides enhanced specificity and accuracy for images of food items. The **Classify an image** method allows you to add this new classifier, "food", to the `classifier_ids` parameter.

### 5 April 2017
{: #5april2017}

- **New {{site.data.keyword.visualrecognitionshort}} tool is available: Beta**

    A new beta feature, the {{site.data.keyword.visualrecognitionshort}} tool, is available. This tool helps you work more easily with the {{site.data.keyword.visualrecognitionshort}} service. By entering your {{site.data.keyword.cloud_notm}} API key, you can use a GUI to access General Tagging and Face Detection features, as well as to seamlessly create, retrain, and delete custom classifiers associated with your API key, without needing to code.

### 8 March 2017
{: #8march2017}

- **Updated language support for general classifier tagging**

    The general classifier now returns tags in all supported languages.

- **Known issues**

    **FIXED 04-13-2017**: Repeatedly calling `GET /classifiers` while training or retraining is in progress, in order to check the status, can result in killing the training job. To workaround this issue, poll a new classifier's status using `GET /classifiers/{classifier_id}`. In other words, use the classifier `GET` for a single classifier ID, rather than `GET /classifiers`, which gets all classifiers, and can trigger this issue. Note that `GET /classifiers/{classifier_id}` is also faster.

### 15 December 2016
{: #15december2016}

- **Improved general classifier tagging**

    - The general classifier's deep learning algorithms have been updated. There is a significant improvement in tag quality for all languages, and a significant increase in the volume of English tags returned by the service. This high-quality tag output is also available when you create your own custom classifier.
    - Color tagging has been added. The service now returns the top one or two colors in the image.

- **Known issues**

    - Images submitted to the demo with EXIF metadata tags do not specify orientation (landscape versus portrait) correctly to the service. iPhone uploaded images may contain EXIF metadata tags. The workaround for this is to update your image metadata to not rely on EXIF metadata tags to specify the orientation of your image. Often, you can do this just by opening the image on your computer and saving it. For example, on a Mac, opening in Preview and then saving the image sets the correct orientation tags.
    - Sending images to the {{site.data.keyword.visualrecognitionshort}} service with [EXIF tag](https://en.wikipedia.org/wiki/Exif){: external} values of 8, 3 or 6 can add latency. The service rotates the pixels of the image to the encoded viewpoint. You can save time by pre-rotating your images, or by removing the EXIF headers if they are not important to your {{site.data.keyword.visualrecognitionshort}} task.

### 1 December 2016
{: #1december2016}

- **New pricing**

    {{site.data.keyword.IBM_notm}} has lowered the pricing of custom classifiers on the {{site.data.keyword.visualrecognitionshort}} service and increased what's available on the free plan. For more information, see the [{{site.data.keyword.visualrecognitionshort}} pricing page](https://www.ibm.com/cloud/watson-visual-recognition/pricing).

### 7 October 2016
{: #7october2016}

- **Face detection enhancements**

    The service has a new face-detection algorithm that improves the responses of the `GET` and `POST /v3/detect_faces` methods. The service adjusted the filtering of low-confidence age, name, and gender facial detections. As a result, more faces are found, and a larger range of confidences are returned.

### 8 September 2016
{: #8september2016}

- **Similarity Search BETA**

    Users can now upload their own collection of images, use an image to search that collection for similar images, and then the service returns the top 100 most similar images. Similarity search can be utilized for any purpose, and users can custom train the service on collections of up to 1 million images each.

- **Text recognition is now closed beta**

    The `POST` and `GET /v3/recognize_text` methods have gone back into closed beta. {{site.data.keyword.IBM_notm}} looks forward to continuing to support BETA clients that use the service, with no current plans for another open beta.

### 1 August 2016

- **Introductory pricing ending**

    Custom classifier training and retraining, custom image classification, and custom classifier storage is no longer free. For information on the pricing, see the {{site.data.keyword.visualrecognitionshort}} service [pricing page](https://www.ibm.com/cloud/watson-visual-recognition/pricing){: external}.

### 5 July 2016
{: #5july2016}

- **Updating custom classifiers**

    Custom classifiers are no longer limited to a fixed set of training data. A user can now update existing classifiers with new images, or add additional positive or negative example classifiers to an existing trained classifier. By supplying additional example images for Watson to learn from, the service can make a user's classifier more accurate. Custom classifiers can now learn over time, continuously getting better at understanding visual information.

- **Known issues**

    **FIXED 04-13-2017**: Users may get a 500 error code after 30 or 90 seconds when updating an existing classifier. Despite the error, there is a good chance that the retrain request completes successfully. Wait at least 2 minutes, and then check the status of the classifier by using the `GET classifiers/{classifier\_id}` method. If the status is "ready" and the "retrained" timestamp has been updated, the retraining request which generated the 500 code was successful. Otherwise, if the "retrained" timestamp has not been updated, there is an explanation added to the response which says why the retraining failed, and the service will revert the classifier to the version there was before the retrain request was issued.

### 20 May 2016
{: #20 may 2016}

This is the General Availability release of the {{site.data.keyword.visualrecognitionshort}} service. This release introduces Version 3 of the service, and is a breaking change. This release incorporates functionality from the AlchemyVision service, which has been deprecated.

Any custom classifiers that were created while the service was in Beta must be recreated in a GA instance of the service.

The following changes and updates were made to the {{site.data.keyword.visualrecognitionshort}} service:

- **Version date:** To utilize the features of this release, use `2016-05-20` as the value for the `version` parameter.
- **Classes and classifiers:** Single classifiers are now called "classes". In GA, a group of classes is called a "classifier".
- **Classification:** Use the `POST` or `GET /v3/classify` methods to quickly and accurately identify a variety of subjects and scenes with default classes.
- **Face detection:** Use the `POST` or `GET /v3/detect_faces` methods to detect faces in images and get information about them, such as where the face is located in the image and the estimated age range and gender for each face. The service can also identify many celebrities by name and can provide a knowledge graph so that you can perform interesting aggregations into higher-level concepts.
- **Multi-faceted custom classifiers:** You can now create and train highly specialized classifiers that are defined by several classes. For example, you can create a "new\_red\_car" classifier that is defined by the classes "new\_cars" and "red\_cars". To learn more  about creating multi-faceted classifiers, see [Structure of the training data](/docs/visual-recognition?topic=visual-recognition-customizing#structure).
- **Asynchronous training:** Training of custom classifiers is now asynchronous, so training calls complete quickly while your custom classifier continues to learn in the background. To check on the training status of your custom classifier and find out when it is available for use, call the `GET /v3/classifiers/{classifier_id}` method and check the `status` response parameter.

### 2 December 2015
{: #2december2015}

The newest release of the {{site.data.keyword.visualrecognitionshort}} service is a breaking change that introduces a new version of the {{site.data.keyword.visualrecognitionshort}} API (v2). Version 1 of the {{site.data.keyword.visualrecognitionshort}} service is available for use until the service exits beta.

To immediately start using version 2 of the API, understand and update your code to reflect these changes:

- In version 1 of the service, you analyzed images by labels. In version 2 of the service, labels are called **classifiers**. Classifiers have a unique classifier ID indicated by the `classifier_id` parameter and a short name indicated by the `name` parameter.
- The `POST /v1/recognize` method for analyzing an image is now the `POST /v2/classify` method. The `labels_to_check` parameter is renamed to `classifier_ids`.
- The `GET /v1/tag/labels` method for retrieving a list of labels in V1 is now the `GET /v2/classifiers` method for retrieving a list of classifiers.
- In addition to retrieving a list of classifiers, you can also retrieve details for a specific classifier with the new `GET /v2/classifiers/{classifier_id}` method.
- Version 2 of the Beta {{site.data.keyword.visualrecognitionshort}} API enables you to create custom classifiers with the new `POST /v2/classifiers` method. To learn more about creating custom classifiers, see [Creating custom classifiers](/docs/visual-recognition?topic=visual-recognition-tutorial-custom-classifier#tutorial-custom-classifier).
- Version 2 of the Beta {{site.data.keyword.visualrecognitionshort}} API also enables you to delete custom classifiers with the new `DELETE /v2/classifiers` method.
- Version 2 of the Beta {{site.data.keyword.visualrecognitionshort}} API requires the `version` parameter. Specify the release date of the version of the API you want to use in `MM-DD-YYYY` format.
