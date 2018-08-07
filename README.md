# AWS SDK for Java Sample Project

This is a modified version of the AWS S3Sample java app. This illustrates accessing
S3 using the AWS Java SDK and also sending traces to the X-ray service.

## Requirements

You have a choice of Maven or Gradle

The only requirement of this application is Maven. All other dependencies can
be installed by building the maven package:
    
    mvn package

Otherwise with gradle you can run the gradlew wrapper and all dependencies will be installed:

    gradlew build

## Basic Configuration

You need to set up your AWS security credentials before the sample code is able
to connect to AWS. You can do this by creating a file named "credentials" at ~/.aws/ 
(C:\Users\USER_NAME\.aws\ for Windows users) and saving the following lines in the file:

    [default]
    aws_access_key_id = <your access key id>
    aws_secret_access_key = <your secret key>

Alternately, do these from the terminal you want to run the sample:
    export AWS_ACCESS_KEY_ID=<your accces key id>
    export AWS_SECRET_ACCESS_KEY=< <your secret key>

See the [Security Credentials](http://aws.amazon.com/security-credentials) page
for more information on getting your keys.

## Running the S3 sample

### Prerequisites
You will need to go to [IAM policies page](https://console.aws.amazon.com/iam/home?#policies), search for the String "S3,"
and "Attach" the "AmazonS3FullAccess" policy to the user whose credentials exist in 
your `~/.aws/credentials` file. Otherwise, you will likely get a `AmazonServiceException`/`Access Denied`/`403` error.

Make sure you have Xray Full access, follow the steps here:
  [X-Ray permissions page](https://docs.aws.amazon.com/xray/latest/devguide/xray-permissions.html)

Run the AWS Xray daemon locally using the steps listed here:
  [Running X-Ray Daemon locally](https://docs.aws.amazon.com/xray/latest/devguide/xray-daemon-local.html)

This sample application connects to Amazon's [Simple Storage Service (S3)](http://aws.amazon.com/s3),
creates a bucket, and uploads a file to that bucket. The code will generate a
bucket name for you, as well as an example file to upload. An AWS Xray trace
is also created to trace the calls.

Run the sample using one of these steps:

Maven:

    mvn clean compile exec:java

Gradle:

    gradlew clean build run

You should see S3 interaction messages on the terminal. On the X-Ray daemon terminal, you
should see messages like "[Info] Successfully sent batch of 1 segments (0.333 seconds)"

You can then view the service map and the traces after going to the X-Ray dashboard on aws.


When you start making your own buckets, the S3 documentation provides a good overview
of the [restrictions for bucket names](http://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html).

## License

This sample application is distributed under the
[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

