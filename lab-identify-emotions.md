# Hands-on Lab: Identify emotions

**Step 1- Create DynamoDB table**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Dynamo

- Click on **Create Table**
- Name of the table: `recognize-emotions-`_your-name_
- Primary key: `s3key`
- Click on **Create**. This will create a table in your DynamoDB.

**Step 2- Create a role for the Lambda function**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for IAM

- Choose **Create Role**
- Select **AWS Service**
- Select **Lambda** and choose **Next: Permissions**

Attach the following policies: 

* ``AmazonDynamoDBFullAcces``
* ``AmazonS3FullAccess``
* ``AmazonRekognitionFullAccess``
* ``CloudWatchFullAccess``

Click **Next**

- Provide a name for the role: ``rekognizeEmotions``
- Choose **Create role**


**Step 3- Create a Lambda function that runs in the cloud**

The inference Lambda function that you deployed earlier will upload the cropped faces to your S3 bucket. On S3 upload, this new Lambda function gets triggered and runs the Rekognize Emotions API by integrating with Amazon Rekognition. 

- Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Lambda
- Click **Create function**
- Choose **Author from scratch**
- Name the function: `recognize-emotion-`_your-name_
- Runtime: Choose Python 2.7
- Role: Choose an existing role
- Existing role: `rekognizeEmotions`
- Choose **Create function**

Replace the default script with the script in [recognize-emotions.py](https://github.com/fibbonnaci/DeepLens-workshops/blob/master/Integrate%20with%20Rekognition/rekognize-emotions.py). You can select the script by selecting Raw in the Github page and choosing the script using Ctrl+A/Cmd+A. Copy the script and paste it into the Lambda function (make sure you delete the default code).

Make sure you enter the table name you created earlier in the section highlighted below:

![dynamodb](https://user-images.githubusercontent.com/11222214/38838790-b8b72116-418c-11e8-9a77-9444fc03bba6.JPG)


Next, we need to add the event that triggers this Lambda function. This will be an “S3:ObjectCreated” event that happens every time a face is uploaded to the face S3 bucket. Add an S3 trigger from the left side of the Designer section in the Lambda console.

Configure with the following:

- Bucket name: `face-detection-`_your-name_ (you created this bucket earlier)
- Event type: `Object Created`
- Prefix: `faces/`
- Filter: `.jpg`
- Enable trigger: ON (keep the checkbox on)

Save the Lambda function.

Under Actions tab choose **Publish**.

**Step 4- View the emotions on a dashboard**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Cloudwatch

- Create a dashboard called `sentiment-dashboard-`_your-name_
- Choose Line in the widget
- Under Custom Namespaces, select “string”, “Metrics with no dimensions”, and then select all metrics.
- Next, set “Auto-refresh” to the smallest interval possible (1h), and change the “Period” to whatever works best for you (1 second or 5 seconds)

NOTE: These metrics will only appear once they have been sent to Cloudwatch via the Rekognition Lambda. It may take some time for them to appear after your model is deployed and running locally. If they do not appear, then there is a problem somewhere in the pipeline.


### With this we have come to the end of the session. As part of building this project, you learnt the following:

1.	How to build and train a face detection model in SageMaker
2.	Modify the DeepLens inference Lambda function to upload cropped faces to S3
3.	Deploy the inference Lambda function and face detection model to DeepLens
4.	Create a Lambda function to trigger Rekognition to identify emotions
5.	Create a DynamoDB table to store the recognized emotions
6.	Analyze the collected data using CloudWatch
