---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Migrating
{: #migrating}

Migrate to a new instance of the {{site.data.keyword.visualrecognitionfull}} service after May 22, 2018.
{: shortdesc}

To migrate your current models/classifiers and training data, you are first required to provision a new instance of the {{site.data.keyword.visualrecognitionshort}} service. Then, take the images you used to train the models in your current {{site.data.keyword.visualrecognitionshort}} service instance, and use those images to re-create your custom models in your new {{site.data.keyword.visualrecognitionshort}} service instance.

1.  Create a new instance of the {{site.data.keyword.visualrecognitionshort}} service:
      - Go to the [{{site.data.keyword.visualrecognitionshort}} page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/visual-recognition){: new_window} in the {{site.data.keyword.cloud_notm}} catalog.
      - Select a plan and click **Create**.

1.  From the service dashboard, select your new {{site.data.keyword.visualrecognitionshort}} service instance, then:
     - Click the **Service credentials** tab and select *View credentials*.
     ![Service credentials tab](images/apikey1.png)
     - Copy the API key as indicated here.
     ![Service credentials tab](images/apikey2.png)

1.  Modify how you call your service. There are two options to authenticate: token and API key. The token option provides greater security if, for example, your API request is somehow compromised, because the token expires after one hour. The API key is a more basic authentication method, and does not expire.

    - Authenticating with an Identity and Access Management (IAM) token

      Use the API key you copied to generate an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) token. For more details, see [How to get an IBM Cloud IAM token using an API key ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam/apikey_iamtoken.html).

      Pass the access token from the response to {{site.data.keyword.visualrecognitionshort}} as a header with a bearer token. For example, specify the token in cURL with the syntax `--header 'Authorization: Bearer {access_token}'`.  Here are some call examples:

      **Note**: The `gateway.watsonplatform.net` endpoint might not be your service endpoint. Check the URL on the Service credentials page of your service dashboard.

      *Classify an image using the default models*

      ``` curl
       curl -X POST --header "Authorization: Bearer eyJhbGciOi......KIi8hdFs" \
       -F "images_file=@my_image.jpg" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"
      ```

      *Detect faces in images*

      ``` curl
       curl -X POST --header "Authorization: Bearer eyJhbGciOi......KIi8hdFs" \
       -F "images_file=@my_faces_image.jpg" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/detect_faces?version=2018-03-19"
      ```

      *Retrieve a list of classifiers*

      ``` curl
       curl -X GET --header "Authorization: Bearer eyJhbGciOi......KIi8hdFs" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers?version=2018-03-19"
      ```

    - Authenticating with an API key directly

      Pass basic authentication information using the syntax `-u "username:password"`, where username is always `apikey` and password is the API key you copied. Here are some call examples:

      **Note**: The `gateway.watsonplatform.net` endpoint might not be your service endpoint. Check the URL on the Service credentials page of your service dashboard.

      *Classify an image using the default models*

      ``` curl
       curl -X POST -u "apikey:{apikey}" \
       -F "images_file=@my_image.jpg" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"
      ```

      *Detect faces in images*

      ``` curl
       curl -X POST -u "apikey:{apikey}" \
       -F "images_file=@my_faces_image.jpg" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/detect_faces?version=2018-03-19"
      ```

      *Retrieve a list of classifiers*

      ``` curl
       curl -X GET -u "apikey:{apikey}" \
       "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers?version=2018-03-19"
      ```

1. [Re-create and train your custom models](tutorial-custom-classifier.html#creating-a-custom-model), using your chosen authentication method, in your new instance of the {{site.data.keyword.visualrecognitionshort}} service.
