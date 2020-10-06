---

copyright:
  years: 2019, 2020
lastupdated: "2020-10-06"

keywords: visual recognition,visual recognition project,VisualRecognition,getting started,classify images, analyze images,tag images,image classification,image recognition,sample code

subcollection: visual-recognition

content-type: tutorial
account-plan: lite
completion-time: 10m

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
{:curl: .ph data-hd-programlang='curl'}
{:go: .ph data-hd-programlang='go'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:unity: .ph data-hd-programlang='unity'}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:step: data-tutorial-type='step'}


# Getting started with {{site.data.keyword.visualrecognitionshort}}
{: #getting-started-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

This tutorial guides you through simple image recognition with {{site.data.keyword.visualrecognitionfull}}. You use the built-in models to analyze the images.
{: shortdesc}

To work in a graphical interface where you can create your own custom models, use <span class="hide-dashboard">[{{site.data.keyword.DSX}}](https://dataplatform.cloud.ibm.com/registration/stepone?target=watson_vision_combined&context=wdp&apps=watson_studio&cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_VisualRecognition-_-docs){: external}</span><span class="hide-in-docs">[{{site.data.keyword.DSX}}](tooling-url){: external}</span>, part of Cloud Pak for Data as a Service, and follow the [video](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/videos.html#vizrec){: external}.
{: tooling-url}
{: tip}

## Before you begin
{: #prerequisites}

- {: hide-dashboard} Create an instance of the service:
    1.  Go to the [{{site.data.keyword.visualrecognitionshort}}](https://{DomainName}/catalog/visual-recognition){: external} page in the catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- {: hide-dashboard} Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` and `URL` values.
- {: curl} Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```sh
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se](https://curl.haxx.se/){: external}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command-line location.
- {: dotnet-standard} Install the [.NET SDK](https://github.com/watson-developer-cloud/dotnet-standard-sdk){: external}.
    - {: dotnet-standard} Package Manager

        ```sh
        Install-Package IBM.Watson.VisualRecognition.v3 -Version 4.0
        ```
        {: codeblock}

    - {: dotnet-standard} .NET CLI

        ```sh
        dotnet add package IBM.Watson.VisualRecognition.v3 -version 4.0
        ```
        {: pre}

    - {: dotnet-standard} PackageReference

        ```xml
        <PackageReference Include="IBM.Watson.VisualRecognition.v3" Version="4.0.0" />
        ```
        {: codeblock}
- {:go} Install the [Go SDK](https://github.com/watson-developer-cloud/go-sdk){: external}.

    ```sh
    go get -u github.com/watson-developer-cloud/go-sdk@v1
    ```
    {: go}
    {: pre}
- {: java} Install the [Java SDK](https://github.com/watson-developer-cloud/java-sdk){: external}.
    - {: java} Maven

        ```xml
        <dependency>
          <groupId>com.ibm.watson</groupId>
          <artifactId>ibm-watson</artifactId>
          <version>[8,9)</version>
        </dependency>
        ```
        {: codeblock}

    - {: java} Gradle

        ```sh
        compile 'com.ibm.watson:ibm-watson:8.+'
        ```
        {:pre}
- {: javascript} Install the [Node SDK](https://github.com/watson-developer-cloud/node-sdk){: external}.

    ```sh
    npm install ibm-watson@^5
    ```
    {:pre}
- {: python} Install the [Python SDK](https://github.com/watson-developer-cloud/python-sdk){: external}.

    ```sh
    pip install --upgrade "ibm-watson>=4.0.1"
    ```
    {:pre}
- {: ruby} Install the [Ruby SDK](https://github.com/watson-developer-cloud/ruby-sdk){: external}.

    ```sh
    gem install ibm_watson
    ```
    {:pre}
- {: unity} Download the [Unity SDK](https://github.com/watson-developer-cloud/unity-sdk){: external} and the [Unity SDK Core](https://github.com/IBM/unity-sdk-core){: external}.

    The IBM Watson Unity SDK has the following requirements.

    - The SDK requires Unity version 2018.2 or later to support TLS 1.2. Set the project settings for both the **Scripting Runtime Version** and the **Api Compatibility Level** to `.NET 4.x Equivalent`.
    - The SDK does not support the WebGL projects. Change your build settings to any platform except `WebGL`.

{{site.data.keyword.Bluemix_dedicated_notm}} plans authenticate by using `-u "{username}:{password}"` instead of `-u "apikey:{apikey}"`. Use the username and password values for your instance in the examples in this tutorial.
{: note}
{: curl}

## Classify an image
{: #classify}
{: step}

1.  Issue the following call to classify [an image](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/640px-IBM_VGA_90X8941_on_PS55.jpg){: external}. <span class="hide-dashboard">Replace `{apikey}` and `{url}` with the service credentials you copied earlier.</span>

    ```sh
    curl -u "apikey:{apikey}"{: apikey} "{url}/v3/classify?url=https://ibm.biz/BdzLPG&version=2018-03-19"{: url}
    ```
    {: pre}
    {: curl}

    ```cs
    IamAuthenticator authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
        );

    VisualRecognitionService visualRecognition = new VisualRecognitionService("2018-03-19", authenticator);
    visualRecognition.SetServiceUrl("{url}"{: url});

    var result = visualRecognition.Classify(
        url: "https://ibm.biz/BdzLPG"
        );

    Console.WriteLine(result.Response);
    ```
    {: dotnet-standard}
    {: codeblock}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/IBM/go-sdk-core/core"
      "github.com/watson-developer-cloud/go-sdk/visualrecognitionv3"
    )

    func main() {
      authenticator := &core.IamAuthenticator{
        ApiKey: "{apikey}"{: apikey},
      }

      options := &visualrecognitionv3.VisualRecognitionV3Options{
        Version: "2018-03-19",
        Authenticator: authenticator,
      }

      visualRecognition, visualRecognitionErr := visualrecognitionv3.NewVisualRecognitionV3(options)

      if visualRecognitionErr != nil {
        panic(visualRecognitionErr)
      }

      visualRecognition.SetServiceURL("{url}"{: url})

      result, response, responseErr := visualRecognition.Classify(
        &visualrecognitionv3.ClassifyOptions{
          URL: core.StringPtr("https://ibm.biz/BdzLPG"),
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    import com.ibm.cloud.sdk.core.service.security.IamOptions;
    import com.ibm.watson.visual_recognition.v3.VisualRecognition;
    import com.ibm.watson.visual_recognition.v3.model.ClassifiedImages;
    import com.ibm.watson.visual_recognition.v3.model.ClassifyOptions;

    public class ClassifyUrlDefault {

      public static void main(String[] args) {

        IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
        VisualRecognition visualRecognition = new VisualRecognition("2018-03-19", authenticator);
        visualRecognition.setServiceUrl("{url}"{: url});

        ClassifyOptions classifyOptions = new ClassifyOptions.Builder()
            .url("https://ibm.biz/BdzLPG")
            .build();
        ClassifiedImages result = visualRecognition.classify(classifyOptions).execute().getResult();
        System.out.println(
            "\n******** Classify with the General model ********\n" + result
                + "\n******** END Classify with the General model ********\n");
      }

    }
    ```
    {: java}
    {: codeblock}

    ```javascript
    const fs = require('fs');
    const VisualRecognitionV3 = require('ibm-watson/visual-recognition/v3');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const visualRecognition = new VisualRecognitionV3({
      version: '2018-03-19',
      authenticator: new IamAuthenticator({
        apikey: '{apikey}'{: apikey},
      }),
      url: '{url}'{: url},
    });

    const classifyParams = {
      url: 'https://ibm.biz/BdzLPG',
    };

    visualRecognition.classify(classifyParams)
      .then(response => {
        const classifiedImages = response.result;
        console.log(JSON.stringify(classifiedImages, null, 2));
      })
      .catch(err => {
        console.log('error:', err);
      });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from ibm_watson import VisualRecognitionV3
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

    authenticator = IAMAuthenticator('{apikey}'{: apikey})
    visual_recognition = VisualRecognitionV3(
        version='2018-03-19',
        authenticator=authenticator
    )

    visual_recognition.set_service_url('{url}'{: url})

    url = 'https://ibm.biz/BdzLPG'

    classes_result = visual_recognition.classify(url=url).get_result()
    print(json.dumps(classes_result, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/authenticators"
    require "ibm_watson/visual_recognition_v3"
    include IBMWatson

    authenticator = Authenticators::IamAuthenticator.new(
      apikey: "{apikey}"{: apikey}
    )
    visual_recognition = VisualRecognitionV3.new(
      version: "2018-03-19",
      authenticator: authenticator
    )
    visual_recognition.service_url = "{url}"{: url}

    url= "https://ibm.biz/BdzLPG"

    classes = visual_recognition.classify(url)
    puts JSON.pretty_generate(classes.result)
    ```
    {: ruby}
    {: codeblock}

    ```cs
    var authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
    );

    while (!authenticator.CanAuthenticate())
        yield return null;

    var visualRecognition = new VisualRecognitionService("2018-03-19", authenticator);
    visualRecognition.SetServiceUrl("{url}"{: url});

    ClassifiedImages classifyResponse = null;
    VisualRecognitionService.Classify(
        callback: (DetailedResponse<ClassifiedImages> response, IBMError error) =>
        {
            Log.Debug("VisualRecognitionServiceV3", "Classify result: {0}", reponse.Response);
            analyzeResponse = response.Result;
        },
        url: "https://ibm.biz/BdzLPG"
        )
    );

    while (classifyResponse == null)
        yield return null;
    ```
    {: unity}
    {: codeblock}

    The response includes the classes that are identified in the image from the built-in General model (`"classifier_id": "default"`) and a confidence score for each class. The score represents a percentage, and higher values represent higher confidences. By default, responses from the **Classify** calls don't include classes with a score lower than `0.5` (50%).

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "circuit board",
                  "score": 0.578,
                  "type_hierarchy": "/electrical device/computer circuit/circuit board"
                },
                {
                  "class": "computer circuit",
                  "score": 0.755
                },
                {
                  "class": "electrical device",
                  "score": 0.757
                },
                {
                  "class": "disk controller",
                  "score": 0.553,
                  "type_hierarchy": "/controller/disk controller"
                },
                {
                  "class": "controller",
                  "score": 0.558
                },
                {
                  "class": "central processing unit",
                  "score": 0.535
                },
                {
                  "class": "PC board",
                  "score": 0.501,
                  "type_hierarchy": "/electrical device/computer circuit/PC board"
                },
                {
                  "class": "CPU board",
                  "score": 0.5,
                  "type_hierarchy": "/electrical device/computer circuit/CPU board"
                },
                {
                  "class": "electronic equipment",
                  "score": 0.6
                },
                {
                  "class": "memory device",
                  "score": 0.599
                },
                {
                  "class": "microchip",
                  "score": 0.592
                },
                {
                  "class": "jade green color",
                  "score": 0.838
                },
                {
                  "class": "emerald color",
                  "score": 0.787
                }
              ]
            }
          ],
          "source_url": "https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/640px-IBM_VGA_90X8941_on_PS55.jpg",
          "resolved_url": "https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/640px-IBM_VGA_90X8941_on_PS55.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 0
    }
    ```
    {: codeblock}

## Classify with the Food model
{: #classify-food}
{: step}

{{site.data.keyword.visualrecognitionshort}} also includes a built-in Food model that might be more accurate for your images with food items.

1.  Issue a call to classify an [image of food](https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg){: external} against the Food model. <span class="hide-dashboard">Replace `{apikey}` and `{url}` with the service credentials you copied earlier.</span>

    ```sh
    curl -u "apikey:{apikey}"{: apikey} -F "classifier_ids=food" "{url}/v3/classify?url=https://ibm.biz/Bd2NPs&version=2018-03-19"{: url}
    ```
    {: pre}
    {: curl}

    ```cs
    IamAuthenticator authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
        );

    VisualRecognitionService visualRecognition = new VisualRecognitionService("2018-03-19", authenticator);
    visualRecognition.SetServiceUrl("{url}"{: url});

    var result = visualRecognition.Classify(
        url: "https://ibm.biz/Bd2NPs",
        classifierIds: new List<string>()
            {
                "food"
            }
        );

    Console.WriteLine(result.Response);
    ```
    {: dotnet-standard}
    {: codeblock}

    ```go
    package main

    import (
      "encoding/json"
      "fmt"
      "github.com/IBM/go-sdk-core/core"
      "github.com/watson-developer-cloud/go-sdk/visualrecognitionv3"
    )

    func main() {
      authenticator := &core.IamAuthenticator{
        ApiKey: "{apikey}"{: apikey},
      }

      options := &visualrecognitionv3.VisualRecognitionV3Options{
        Version: "2018-03-19",
        Authenticator: authenticator,
      }

      visualRecognition, visualRecognitionErr := visualrecognitionv3.NewVisualRecognitionV3(options)

      if visualRecognitionErr != nil {
        panic(visualRecognitionErr)
      }

      visualRecognition.SetServiceURL("{url}"{: url})

      result, response, responseErr := visualRecognition.Classify(
        &visualrecognitionv3.ClassifyOptions{
          URL: core.StringPtr("https://ibm.biz/Bd2NPs"),
          ClassifierIds: []string{"food"},
        },
      )
      if responseErr != nil {
        panic(responseErr)
      }
      b, _ := json.MarshalIndent(result, "", "  ")
      fmt.Println(string(b))
    }
    ```
    {: go}
    {: codeblock}

    ```java
    import java.util.Collections;

    import com.ibm.cloud.sdk.core.service.security.IamOptions;
    import com.ibm.watson.visual_recognition.v3.VisualRecognition;
    import com.ibm.watson.visual_recognition.v3.model.ClassifiedImages;
    import com.ibm.watson.visual_recognition.v3.model.ClassifyOptions;

    public class ClassifyUrlFood {

      public static void main(String[] args) {

        IamAuthenticator authenticator = new IamAuthenticator("{apikey}"{: apikey});
        VisualRecognition visualRecognition = new VisualRecognition("2018-03-19", authenticator);
        visualRecognition.setServiceUrl("{url}"{: url});

        ClassifyOptions classifyOptions = new ClassifyOptions.Builder()
            .url("https://ibm.biz/Bd2NPs")
            .classifierIds(Collections.singletonList("food"))
            .build();
        ClassifiedImages result = visualRecognition.classify(classifyOptions).execute().getResult();
        System.out.println(
            "\n******** Classify with the Food model ********\n" + result
                + "\n******** END Classify with the Food model ********\n");
      }

    }
    ```
    {: java}
    {: codeblock}

    ```javascript
    const fs = require('fs');
    const VisualRecognitionV3 = require('ibm-watson/visual-recognition/v3');
    const { IamAuthenticator } = require('ibm-watson/auth');

    const visualRecognition = new VisualRecognitionV3({
      version: '2018-03-19',
      authenticator: new IamAuthenticator({
        apikey: '{apikey}'{: apikey},
      }),
      url: '{url}'{: url},
    });

    const classifyParams = {
      url: 'https://ibm.biz/Bd2NPs',
      classifierIds: ['food'],
    };

    visualRecognition.classify(classifyParams)
      .then(response => {
        const classifiedImages = response.result;
        console.log(JSON.stringify(classifiedImages, null, 2));
      })
      .catch(err => {
        console.log('error:', err);
      });
    ```
    {: javascript}
    {: codeblock}

    ```python
    import json
    from ibm_watson import VisualRecognitionV3
    from ibm_cloud_sdk_core.authenticators import IAMAuthenticator

    authenticator = IAMAuthenticator('{apikey}'{: apikey})
    visual_recognition = VisualRecognitionV3(
        version='2018-03-19',
        authenticator=authenticator
    )

    visual_recognition.set_service_url('{url}'{: url})

    url = 'https://ibm.biz/Bd2NPs'
    classifier_ids = ["food"]

    classes_result = visual_recognition.classify(url=url, classifier_ids=classifier_ids).get_result()
    print(json.dumps(classes_result, indent=2))
    ```
    {: python}
    {: codeblock}

    ```ruby
    require "json"
    require "ibm_watson/authenticators"
    require "ibm_watson/visual_recognition_v3"
    include IBMWatson

    authenticator = Authenticators::IamAuthenticator.new(
      apikey: "{apikey}"{: apikey}
    )
    visual_recognition = VisualRecognitionV3.new(
      version: "2018-03-19",
      authenticator: authenticator
    )
    visual_recognition.service_url = "{url}"{: url}

    classes = visual_recognition.classify(
      url= "https://ibm.biz/Bd2NPs"
      classifier_ids= ["food"]
    )
    puts JSON.pretty_generate(classes.result)
    ```
    {: ruby}
    {: codeblock}

    ```cs
    var authenticator = new IamAuthenticator(
        apikey: "{apikey}"{: apikey}
    );

    while (!authenticator.CanAuthenticate())
        yield return null;

    var visualRecognition = new VisualRecognitionService("2018-03-19", authenticator);
    visualRecognition.SetServiceUrl("{url}"{: url});

    ClassifiedImages classifyResponse = null;
    VisualRecognitionService.Classify(
        callback: (DetailedResponse<ClassifiedImages> response, IBMError error) =>
        {
            Log.Debug("VisualRecognitionServiceV3", "Classify result with Food model: {0}", response.Response);
            classifyResponse = response.Result;
        },
        url: "https://ibm.biz/Bd2NPs",
        classifierIds: new List<string>()
            {
                "food"
            }
        )
    );

    while (classifyResponse == null)
        yield return null;
    ```
    {: unity}
    {: codeblock}

    The service returns the following results. You can see that the `classifier_id` is identified as `food`. The classes that the service identified are also different from the first response.

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "food",
              "name": "food",
              "classes": [
                {
                  "class": "apple",
                  "score": 0.572,
                  "type_hierarchy": "/fruit/accessory fruit/apple"
                },
                {
                  "class": "accessory fruit",
                  "score": 0.572
                },
                {
                  "class": "fruit",
                  "score": 0.805
                },
                {
                  "class": "banana",
                  "score": 0.5,
                  "type_hierarchy": "/fruit/banana"
                }
              ]
            }
          ],
          "source_url": "https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg",
          "resolved_url": "https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 0
    }
    ```

## Next steps
{: #gs-next-steps}

You have a basic understanding of how to use built-in classifiers for image recognition with {{site.data.keyword.visualrecognitionshort}}. Now dive deeper:

- Try these calls with your own images. Keep the image size under 10 MB.
- Learn more about how to [build a custom model](/docs/visual-recognition?topic=visual-recognition-tutorial-custom-classifier#tutorial-custom-classifier).
- {: curl} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=dotnet-standard){: external}.
- {: dotnet-standard} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=dotnet-standard){: external}.
- {: go} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=go){: external}.
- {: java} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=java){: external}.
- {: javascript} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=node){: external}.
- {: python} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=python){: external}.
- {: ruby} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=ruby){: external}.
- {: unity} Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition/visual-recognition-v3?code=unity){: external}.

### Attributions
{: #attributions}

- [IBM VGA 90X8941 on PS55.jpg](https://commons.wikimedia.org/wiki/File:IBM_VGA_90X8941_on_PS55.jpg){: external} by [Darklanlan](https://commons.wikimedia.org/wiki/User:Darklanlan){: external} used under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode "Creative Commons Attribution 4.0"){: external}. No changes were made to this image.
- [Fruit basket](https://flic.kr/p/JPHES){: external} by Flikr user [Ryan Edwards-Crewe](https://www.flickr.com/photos/ryanec/){: external} used under [Creative Commons Attribution 2.0 license](https://creativecommons.org/licenses/by/2.0/deed.en){: external}. No changes were made to this image.
- [Ginni Rometty at the Fortune MPW Summit in 2011](https://commons.wikimedia.org/wiki/File:Ginni_Rometty_at_the_Fortune_MPW_Summit_in_2011.jpg){: external} by Asa Mathat / Fortune Live Media used under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/legalcode){: external}. No changes were made to this image.
