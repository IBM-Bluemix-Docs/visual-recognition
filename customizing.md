---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-02"

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

# Guidelines for training classifiers

After you classify an image and create, train, and query a custom classifier with the example data in the [Creating a custom classifier tutorial](/docs/services/visual-recognition/tutorial-custom-classifier.html), you can classify your own data or create your own custom classifier.
{: shortdesc}

## General classifier categories
{: #general-model}

The General classifier returns classes from thousands of possible tags organized into categories and subcategories. The following list shows the top-level categories:

- Animals (including birds, reptiles, amphibians, etc.)
- Person and people-oriented information and activities
- Food (including cooked food and beverages)
- Plants (including trees, shrubs, aquatic plants, vegetables)
- Sports
- Nature (including many types of natural formations, geological structures)
- Transportation (land, water, air)
- And many more, including furnishings, fruits, musical instruments, tools, colors, gadgets, devices, instruments, weapons, buildings, structures and man-made objects, clothing and garments, and flowers, among others.

### Classify response hierarchy

The `/v3/classify` method classifies images within a hierarchy of related classes. For example, a picture of a Beagle might be classified as "animal" as well as the related "dog" and "beagle". A positive match with the related classes, in this case "dog" and "beagle", boosts the score of the parent response. In this example, the response includes all three classes: "animal", "dog", and "beagle". The score of the parent class ("animal") is boosted because it matches the related classes ("dog" and "beagle"). The parent is also a "type\_hierarchy" to show that it is a parent of the hierarchy.
### Estimate the cost involved

**Important:** When creating the classifier, each image used is counted as a training event. Each training event is billed at the rate of $0.10. Plan the total cost involved before creating the custom classifier. 

For example if 200 images are ued for a classifier, the cost incurred will be 200 * $0.10 = $20.

## Structure of the training data
{: #structure}

A custom classifier is a group of classes that are trained against each other. This allows you to create a multi-faceted classifier that can identify highly specialized subjects, while also providing a score for each individual class.

During training, classes are created when you upload separate compressed (.zip) files of positive examples for each class. For example, to create a classifier called "fruit", you might upload a .zip file of images of pears, a .zip file of images of apples, and a .zip file of images of bananas in a single training call.

You can also provide a .zip file of negative examples in the same training call to further hone your classifier. Negative example files are not used to create a class. For the custom classifier "fruit", you might provide a .zip file with images of various vegetables.

![Fruits classifier with positive and negative examples](images/classifier.png)

After training completes, when the service identifies fruit in an image, it will return the classifier "fruit" as an array containing the classes "pears", "apples", and "bananas" with their respective confidence scores.

**Important:** The **Create a classifier** call requires that you provide at least two example .zip files: two positive examples files or one positive and one negative file.

Custom classifiers are accessible only to the specific service instance where they were created and cannot be shared with other {{site.data.keyword.Bluemix_notm}} users who do not have access to your instance of the service.

## Updating custom classifiers

You can update an existing classifier by adding new classes or by adding new images to existing classes. To update the existing classifier, use several compressed (.zip) files, including files containing positive or negative images (.jpg, or .png). You must supply at least one compressed file, with additional positive or negative examples.

Compressed files containing positive examples are used to create and update "classes" to impact all of the classes in that classifier. The prefix that you specify for each positive example parameter is used as the class name within the new classifier. The "\_positive\_examples" suffix is required. There is no limit on the number of positive example files you can upload in a single call.

The compressed file containing negative examples is not used to create a class within the created classifier, but does define what the updated classifier is not. Negative example files should contain images that do not depict the subject of any of the positive examples. You can only specify one negative example file in a single call.

![Fruits classifier retrained with new positive class for oranges and negative class for cheese](images/retrain.png)

### How retraining works

If you train a classifier with three sets of positive class pictures - Apples, Bananas, and Pears - the system trains three models internally. For the Apples model, the group of pictures in "Apples" is trained as a positive example, and the group of pictures uploaded in "Bananas" and "Pears" are trained as negative examples. The system then knows that bananas and pears are not apples. The other classes are used as negative examples for the Bananas, and Pears models as well.

Next, say you want to retrain your classifier with new positive classes: YellowPears and GreenPears. In order to do this, you'll need to manually look through your old pears.zip folder, and split the images out into two new folders: YellowPears.zip and GreenPears.zip.

**Important:** Splitting a class definition via retraining is possible, but it calls for great care in organizing the data. You must submit the **exact** same image files to the new folders - no resizing or anything - that you used during the original training. For example, when creating YellowPears or GreenPears, every single yellow pear image from the original pears.zip training set should be exactly copied into the YellowPears.zip folder; otherwise, any image that is not copied exactly will be in the Pears training set, and used as a negative when YellowPears is trained.

Now, you simply retrain the system with YellowPears.zip and GreenPears.zip as positive examples. When you do this, the system recognizes the exact duplicate images in the YellowPears and GreenPears folders from the original pears.zip folder, and those images are retrained as positive examples for their new classes. The rule is that a duplicate image is kept in the positive set, if it is also found in both the negative and positive set for a class.

The end result is that the YellowPears and GreenPears classes will have Apples and Bananas as negative examples, but will not have any exact duplicate images from the Pears class as negative examples.

## Size limitations

There are size limitations for training calls and data:

- The service accepts a maximum of 10,000 images or 100 MB per .zip file
- The service requires a minimum of 10 images per .zip file.
- The service accepts a maximum of 256 MB per training call.
- Minimum recommended size of an image is 32X32 pixels.

There are also size limitations when classifying images or detecting faces:

- Limitations for the methods to classify images:
    - Maximum image size is 10 MB.
    - Maximum .zip file size is 100 MB with up to 20 images.
- Limitations for the methods to detect faces:
    - Maximum image size is 10 MB.
    - Maximum .zip file size is 100 MB with up to 15 images.

<!-- - The `POST /v3/recognize_text` method accept a maximum of 10 images per batch. -->

## Guidelines for good training

The following guidelines are not enforced by the API. However, the service tends to perform better when the training data adheres to them:

- Make sure that your images are at least 224 x 224 pixels.
- For .png images, make sure that the pixel depth is set to at least 24 bits per pixel:
    - To check the depth on MacOS, run the `file` command. 24-bit depth is displayed as `8-bit/color`.
    - To check on Windows, right-click the file and choose **Properties** > **Details**. Look for **Bit depth**.
- Include at least 50 positive images per class before you assess your training results.
    - Assuming similar quality and content for your training data, more training images generally provide more accurate results than fewer images.
    - 150 - 200 images per .zip file provides the best balance between processing time and accuracy. More than 200 images increases the time and the accuracy, but with diminishing returns for the amount of time it takes.
    - The benefits of training a classifier on more images plateaus at around 5000 images. Although you can train on more than 5000 images, that number might not significantly increase accuracy, and increases processing time.
- Include a negative class to help improve your results.
    - Include approximately the same number of negative images as positive ones. An unequal number of images might reduce the quality of the trained classifier.
- Make sure that the backgrounds in your training images are comparable to what you expect to classify. The accuracy of your classifier can be affected by the kinds of images you provide to train it.
    - For example, if you are training the "tiger" classifier, your classifier might be less accurate if you train only on images of tigers in a zoo that are taken by a mobile phone but analyze images that taken in the wild taken by professional photographers.
- Make sure that the subject matter of the classifier is at least 1/3 of the image's overall size.

For more information about training, see [Best practices for custom classifiers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2016/10/watson-visual-recognition-training-best-practices/){: new_window}.

## Guidelines for high volume classifying

Maximize efficiency and performance of the service in the following ways when you submit many images:

- Crop or resize your images to 224 x 224 pixels. The service is currently optimized for this size although it might change.
    - Crop the image if it has an aspect ratio greater than 2:1 or under 1:2.
    - Consider cropping the image into multiple square images, or include only the center of the image, depending on what is most important to your use.
- Submit up to 20 images in a single .zip file. You don't need to use any compression because JPEG and PNG images are compressed files.
- Use the **classifier_ids** parameter to specify only the classifiers that you want to use.
- Although the service reads EXIF tags and rotates images, for the best throughput, send images that don't need to be rotated by the service (the EXIF **Orientation** tag is set to `1`).

## Custom classifier scores

The `/classify` method produces a score between 0.0 and 1.0 for each image for each class. This section delves into the meaning of those scores for custom classifiers (as opposed to the General classifier).

### Background reading

- The service performs [statistical classification. ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Statistical_classification){: new_window}
- You can [measure statistical classifiers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Category:Information_retrieval_evaluation){: new_window} in several ways.

### How to use the scores

- Think about possible actions to be taken in response to a classification. Specifically, analyze how you will use "true" or "false" positive or negative conditions.  These conditions are described in the Background Reading.
- This cost-benefit balance is crucial to deciding what to do with each class score, and only someone who understands the final application can determine it. The score value needed for the application to take some action is called the "decision threshold." The service does not compute this for you.
- Custom classifiers use binary "one versus the rest" models to train each class against the other classes. The system assumes that two classes within a classifier cannot occur at the same time, so you should create separate classifiers to test for classes that can exist together, like `blue` and `sky`. Alternatively, you could create a distinct classifier for cases where both classes exist at the same time and test for a class like `blueSky`.

### Example

Imagine that you are monitoring an assigned parking space with a webcam. You train a custom classifier to recognize whether your car is in the spot, some other car is in the spot, the spot is empty, or the camera has been blocked. You collect training examples for each of these cases and train a custom classifier with four classes. Your application classifies images from the webcam to report the status of the spot, and the system notifies you with a message if the status is unexpected. Each time the service classifies the image from the camera, it produces four scores: `myCar`, `unknownCar`, `emptySpot`, and `blockedCamera`.

The first action to consider is whether to send a notification.

Suppose you park in your spot and have the service start classifying the images. You see the `myCar` score computed as 0.8 on average over a few hours, while the `unknownCar` score hovers around 0.3, `emptySpot` is around 0.15 and `blockedCamera` is around 0.1. Given this data, you write your code to notify you if the `myCar` score is less than 0.75, or if one of the others is greater than 0.6. During the day, you get about one false alarm every three hours when people walk by and obscure the car. The system sends you the photo along with the notice, so you can see it's nothing to worry about. That seems fine, but then at night those false alarms every three hours get very annoying! Your preferences for day versus night notification reflect the higher cost of a false alarm at night time for your application.

So, the notification logic and threshold will probably vary, depending on the perceived risk of car theft, the accuracy of your classifiers, and the amount of annoyance caused by a false alarm.

Similarly, as a person, you may face the same trade  off. If the system notifies you that the camera has been blocked, the accompanying image will likely simply be all black or gray. Do you go to check on the car in person or ignore it? Again, this depends on your other priorities and the perceived risks.

### Questions

- **What do the scores mean?**

    - The scores are comparable indicators, with a range from 0.0 to 1.0. You can compare the scores of two custom classes (from the same or different classifiers) on the same or different images, and the higher one should be more likely to appear in the image than the lower one. However, they may both be present. It is best to pick a decision threshold for each class individually.
    - The scores for custom classifiers are not comparable to the scores returned by the General classifier (which has `classifier_id: "default"`)
    - The service attempts to normalize the score output so that 0.5 is a good decision threshold. By default, scores below 0.5 are not reported in the results of `/classify`. You can override this behavior by setting the threshold parameter of the `/classify` method. This normalization is only computed on the training data, so with new data or different application contexts, you might find that a different threshold works better.
    - The scores are unitless and are neither percentages nor probabilities. (They do not add up to 100% or 1.0).

- **Why do I get scores between 0.5 and 0.6 for images that I would expect to return a high score, near 1.0?**

    You might get lower scores if there is a significant amount of similarity between your classes, so that in the feature space your examples are not in distinct clusters, and the scores reflect this closeness to the best boundary between positives and negatives that the system could learn.

- **How can I evaluate the accuracy of a custom classifier for my use case?**

    You can do this in multiple ways, one of which is the following:

    1.  Assemble a set of labeled images "L" that was not used in training the classifier.
    1.  Split L into two sets, V and T - validation and testing.
    1.  Run V through your classifier and pick a score threshold "R" which optimizes the correctness metric you value, such as top-5 precision, across all of V.
    1.  From T, select a random subset "Q" and classify it using your classifier and "R". Compute the probability of a correct classification on Q. That's one experiment.
    1.  Repeat step 4 with a different subset Q from T, then compute the average % correct across all experiments.
