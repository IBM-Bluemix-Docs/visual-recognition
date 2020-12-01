---

copyright:
  years: 2015, 2020
lastupdated: "2020-12-01"

keywords: custom model,custom classifier,samples,train classifier,train mode,train custom model,update model,retrain model

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
{:curl: .ph data-hd-programlang='curl'}
{:go: .ph data-hd-programlang='go'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}

# Creating a custom model
{: #tutorial-custom-classifier}

{{site.data.keyword.visualrecognitionfull}} is discontinued. Existing instances are supported until 1 December 2021, but as of 7 January 2021, you can't create instances. Any instance that is provisioned on 1 December 2021 will be deleted.
{: deprecated}

After you analyze an image in the "Getting started tutorial," you are ready to train and create a custom model. With a custom model, you can train the {{site.data.keyword.visualrecognitionshort}} service to classify and recognize images to suit your business needs.
{: shortdesc}

## Step 1:  Copy your credentials
{: #copy-credentials}

Use the credentials that you copied in "Getting started tutorial." If you didn't create a service instance, run through those steps in the [Before you begin](/docs/visual-recognition?topic=visual-recognition-getting-started-tutorial#prerequisites) section.

{{site.data.keyword.Bluemix_dedicated_notm}} plans authenticate by using `-u "{username}:{password}"` instead of `-u "apikey:{apikey}"`. Use the username and password values for your instance in the examples in this tutorial.
{: note}

## Step 2: Creating a custom model
{: #create}

{{site.data.keyword.visualrecognitionshort}} can learn from example images you upload to create a new, multi-faceted model. Each example file is trained against the other files in that call, and positive examples are stored as classes. These classes are grouped to define a single model, and return their own scores. Negative example files are not stored as classes.

1.  Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/beagle.zip" download="beagle.zip">beagle.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/husky.zip" download="husky.zip">husky.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/golden-retriever.zip" download="golden-retriever.zip">golden-retriever.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>, and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/cats.zip" download="cats.zip">cats.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> example training files.
1.  Call the `POST /v3/classifiers` method with the following command, which uploads the training data and creates a `dogs` custom model:
    - Replace `{apikey}` and `{url}` with the service credentials you copied in the first step.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --form "beagle_positive_examples=@beagle.zip" \
    --form "husky_positive_examples=@husky.zip" \
    --form "goldenretriever_positive_examples=@golden-retriever.zip" \
    --form "negative_examples=@cats.zip" \
    --form "name=dogs" \
    "{url}/v3/classifiers?version=2018-03-19"
    ```
    {: pre}

    Windows users: Replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure that there are no trailing spaces.
    {: tip}

    Positive example file names require the suffix `_positive_examples`. In this example, the file names are `beagle_positive_examples`, `goldenretriever_positive_examples`, and `husky_positive_examples`. The prefix (beagle, goldenretriever, and husky) is returned as the name of class.

    The response includes a new classifier ID and status, for example:

    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "status": "training",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "created": "2018-03-17T19:01:30.536Z",
      "updated": "2018-03-17T19:01:30.536Z",
      "classes": [
        {
          "class": "husky"
        },
        {
          "class": "goldenretriever"
        },
        {
          "class": "beagle"
        }
      ],
      "core_ml_enabled": true
    }
    ```
    {: codeblock}

1.  Check the training status periodically until you see a status of `ready`. Training begins immediately and must finish before you can query the model. Replace `{apikey}`, `{url}`, and `{classifier_id}` with your information:

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    "{url}/v3/classifiers/{classifier_id}?version=2018-03-19"
    ```
    {: pre}

## Step 3: Updating an existing custom model
{: #tutorial-custom-classifier-update}

You can update a custom model either by adding classes to the model or by adding images to an existing class. Here, you improve the model that you created in Step 2 by adding a *Dalmatian* class to the types of dogs that can be classified. You also add images of cats to the negative example set for the "dogs" custom model.

1.  Download the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/dalmatian.zip" download="dalmatian.zip">dalmatian.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> and <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/more-cats.zip" download="more-cats.zip">more-cats.zip <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> sample training files.
1.  Call the `POST /v3/classifiers/{classifier_id}` method with the following curl command, which uploads the training data and updates the custom model "dogs\_1941945966":
    - Replace `{apikey}` and `{url}` with the service credentials you copied in the first step.
    - Replace `{classifier_id}` with the ID of the custom model you want to update.
    - Modify the location of the `{class}_positive_examples` to point to where you saved the .zip files.

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --form "dalmatian_positive_examples=@dalmatian.zip" \
    --form "negative_examples=@more-cats.zip" \
    "{url}/v3/classifiers/{classifier_id}?version=2018-03-19"
    ```
    {: pre}

    The existing "dogs" custom model is replaced by the retrained one with the same classifier_id. The response lists the new set of classes and the status. For example:

    ```json
    {
      "classifier_id": "dogs_1941945966",
      "name": "dogs",
      "status": "retraining",
      "owner": "xxxx-xxxxx-xxx-xxxx",
      "created": "2018-03-17T19:01:30.536Z",
      "updated": "2018-03-17T19:01:30.536Z",
      "classes": [
        {
          "class": "husky"
        },
        {
          "class": "goldenretriever"
        },
        {
          "class": "beagle"
        },
        {
          "class": "dalmatian"
        }
      ],
      "core_ml_enabled": true
    }
    ```
    {: codeblock}

    Training begins immediately. When the new one is available, the status changes to `ready`.

    Don't issue another retraining request until the status is `ready`. Multiple requests to retrain a model result in a single retraining taking effect. A time stamp that is called `updated` shows the time that the model was most recently updated. If you call the **Classify** methods while the model is retraining, the old definition of the model is used.
    {: tip}
1.  Check the training status periodically until you see a status of `ready`. Replace `{apikey}`, `{url}`, and `{classifier_id}` with your information:

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    "{url}/v3/classifiers/{classifier_id}?version=2018-03-19"
    ```
    {: pre}

## Step 4: Classifying an image with a custom model
{: #tutorial-custom-classifier-classify}

When the new model is ready, call it to see how it performs.

1.  Download the <a target="_blank" href="https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/visual-recognition/dogs.jpg" download>dogs.jpg <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Use the `POST /v3/classify` method to test your custom model. The following example classifies the `dogs.jpg` image against both the "dogs\_1941945966" custom model and the built-in `default` General model:
    - Replace `{apikey}` and `{url}` with the service credentials you copied in the first step.

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --form "images_file=@dogs.jpg" \
    --form "classifier_ids=dogs__1941945966,default" \
    "{url}/v3/classify?version=2018-03-19"
    ```
    {: pre}

    To classify against only the built-in General model, omit the `classifier_ids` parameter.
    {: tip}

    The response includes classifiers (models), their classes, and a score for each class. Scores are in the range 0 - 1, and a higher score indicates greater correlation. The **Classify** methods omit low-scoring classes by default if high-scoring classes are identified. You can set a minimum score to display by specifying a floating point value for the `threshold` parameter in your call.

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "dogs_1941945966",
              "name": "dogs",
              "classes": [
                {
                  "class": "goldenretriever",
                  "score": 0.513638
                }
              ]
            },
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "guide dog",
                  "score": 0.86,
                  "type_hierarchy": "/animal/domestic animal/dog/guide dog"
                },
                {
                  "class": "dog",
                  "score": 0.927
                },
                {
                  "class": "domestic animal",
                  "score": 0.927
                },
                {
                  "class": "animal",
                  "score": 0.927
                },
                {
                  "class": "beagling (dog)",
                  "score": 0.508,
                  "type_hierarchy": "/animal/domestic animal/dog/beagling (dog)"
                },
                {
                  "class": "golden retriever dog",
                  "score": 0.5,
                  "type_hierarchy": "/animal/domestic animal/dog/retriever dog/golden retriever dog"
                },
                {
                  "class": "retriever dog",
                  "score": 0.572
                },
                {
                  "class": "light brown color",
                  "score": 0.982
                }
              ]
            }
          ],
          "image": "dogs.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 1
    }
    ```
    {: codeblock}

1.  Review your results.

You're done! You created, trained, and queried a custom model with {{site.data.keyword.visualrecognitionshort}}.

### Deleting your custom model
{: #tutorial-custom-classifier-delete}

You might want to delete your custom model to begin developing your application with a clean instance.

To delete the model, call the `DELETE /v3/classifiers/{classifier_id}` method. Replace `{apikey)`, `{url}`, and `classifier_id` with your information:

```bash
curl -X DELETE -u "apikey:{apikey}" \
"{url}/v3/classifiers/{classifier_id}?version=2018-03-19"
```
{: pre}

## Next steps
{: #tutorial-custom-classifier-next-steps}

Now that you have a basic understanding of how to use custom models, you can dive deeper:

- Learn more about [Best practices for custom classifiers](https://www.ibm.com/cloud/blog/watson-visual-recognition-training-best-practices){: external}.
- Read about the API in the [API reference](https://{DomainName}/apidocs/visual-recognition){: external}.

### Attributions
{: #tutorial-custom-classifier-attributions}

All images that are used on this page are from Flikr and used under [Creative Commons Attribution 2.0 license](https://creativecommons.org/licenses/by/2.0/deed.en){: external}. No changes were made to these images.
