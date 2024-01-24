Push AWS notification to Microsoft Teams

## 1. Create a connector for the Teams channel.

> - Teams -> Channel -> Settings -> Connectors -> Edit: Open the dialog "Connectors for "Your Channel Name" channel in "Your Team Name" team.
> - Search "Incoming Webhook", click "Add", open the Incoming Webhook dialog, and click "Add".
> - Provide a name, e.g., "aws-sns-notification", and select "Create".
> - Copy and save the URL. This will be utilized in the AWS lambda function.
> - Click "Done". 

## 2. Create an AWS SNS topic.

> - AWS > Console > SNS > Topics.
> - Click "Create topic".
> - Select the "Standard" type and input the topic name.
> - "Access policy" should allow the S3 bucket to publish events related to this topic; change access policy by "aws/sns/sns_topic_access_policy.json", change "Resource" and "aws:SourceArn" to the current topic and your S3 bucket ARN.
> - Click "Create topic".

## 1.3 Enabling event notification for S3 deletions

> - AWS > Console > S3 > Bucket.
> - Click on your bucket name, select Properties, and scroll down to "Event notifications" and click "Create Event Notification".
> - Input the name for the event; select event type as "All object removal events".
> - Select the destination as "SNS topic" and select the topic created in the previous step.
> - Click "Save changes".

## 1.4 Send messages in SNS to Microsoft Teams by the AWS Lambda function

> - AWS console > lambda > Functions.
> - Click "Create function".
> - Select "Author from scratch", input the name for the function, and select "Python ${version}" for the runtime.
> - Click "Create function".
> - Open the function and change the code to "aws/lambda/lambda_function.py".
> - Deploy as latest.
> - Configure the trigger as an SNS notification and select the topic name created in the previous step.


