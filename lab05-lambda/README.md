# Lab 05 - Lambda

First serverless lab, and my first real taste of event-driven architecture instead of always-on servers.

## What I did

Created a basic Lambda function in Python that returns a hello message with the current time, deployed it, and ran a manual test to confirm it executes correctly. Then wired it up to actually respond to something real: added an S3 trigger pointing at my Lab 02 bucket, so the function fires automatically whenever a new file gets uploaded there. Updated the code to pull the bucket name and file name out of the event data and log them.

Uploaded a test file into the bucket and checked CloudWatch Logs afterward - the function had run on its own and logged the exact file name, with no manual invocation needed. That is the core idea of serverless: the code just sits there doing nothing (and costing nothing) until something actually happens.

## The interesting problem

After updating the code for the S3 event structure, I still had the old generic test event saved from earlier. Running that old test threw a KeyError because it does not have the same shape as a real S3 event (no Records key). Good reminder that a Lambda function's code is written for a specific event source, and a manual test event has to actually match that shape to be useful - the real proof came from letting the actual S3 upload trigger it, not from the fake test.

## Commands / actions used

Fully GUI-based - Lambda function creation, code editor, S3 trigger configuration, and CloudWatch Logs all done through the AWS Console.

## Screenshots

lambda-code.jpg: Deployed function code reading the S3 event data

s3-trigger-configured.jpg: Function diagram showing the S3 trigger wired in

trigger-logs.jpg: CloudWatch logs proving the real S3 upload triggered the function automatically
