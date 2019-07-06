# How to trace Serverless apps with AWS X-Ray?

AWS X-Ray is a service that records and visualize requests made by your application. It provides an end-to-end view of requests as they travel through your application, and shows a map of your application's underlying components.

To understand how X-Ray works, read [What is AWS X-Ray?]()

This posts will show you how to set up AWS X-Ray to trace API requests and Lambda invocations for your Serverless Framework application.

### Enable X-Ray tracing for API Gateway and Lambda

Open your `serverless.yml` and add a **tracing** configuration inside the **provider** section:
```yaml=
provider:
  ...
  tracing:
    apiGateway: true
    lambda: true
```

Then add the IAM permissions required for Lambda to write to X-Ray under **iamRoleStatements** inside the **provider** section:
```yaml=
provider:
  ...
  iamRoleStatements:
    - Effect: Allow
      Action:
        ...
        - xray:PutTraceSegments
        - xray:PutTelemetryRecords
      Resource: "*"
```

And just for reference, here is my Lambda function:
```javascript=
const AWS = require('aws-sdk');
const dynamodb = new AWS.DynamoDB.DocumentClient();
const sns = new AWS.SNS();

exports.main = async function(event) {

  await dynamodb.get({
    TableName: 'notes',
    Key: { noteId: 'note1' },
  }).promise();

  await sns.publish({
    Message           : 'test',
    TopicArn          : 'arn:aws:sns:us-east-1:113345762000:test-topic',
  }).promise();


  return { statusCode: 200, body: 'successful' };
}
```

Now run `sls deploy` to deploy your service. Do **not** deploy an individual function since you made changes to your **serverless.yml**.

Note: If you are trying to enable AWS X-Ray Tracing on existing Serverless projects, make sure your Serverless cli version is later than 1.44.

After you deploy, invoke your API Gateway endpoint:
```bash=
$ curl https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/xxx
```

Go to your AWS X-Ray console, and select **Traces** from the left menu.
![](https://i.imgur.com/uXA92Qm.png)

The **Trace overview** section at the top show all the URL that initiated the trace. And the **Trace list** section at the bottom shows each individual traces. By default, it shows all the traces within the last 5 minutes. You can pick a different time range.

Click on a trace in the **Trace list**. Note: it might take up to 30 seconds before a trace shows up.
![](https://i.imgur.com/RXnEhYZ.png)

A couple of things you can see here:
- The API request was a GET request and succeeded with 200 status
- Entire request took API Gateway 597ms to process
- Out of 597ms, 594ms was spent by Lambda function. Meaning API Gateway added 3ms of overhead.
- Out of 594ms, it took 387ms for Lambda to initialize. That's **Cold Start** time.
- The actual process took 107ms.

But I want two questions:
- How long did the DyanmoDB query and the SNS each took?
- If a API request fails, how do I know if it failed at the DynamoDB step or the SNS step? 

### Enable X-Ray tracing for other AWS services invoked by AWS Lambda

Install AWS X-Ray sdk. In your project directory, run:
```bash=
$ npm install -s aws-xray-sdk
```

Update your Lambda code and wrap AWS sdk with X-Ray sdk. Change:
```javascript=
const AWS = require('aws-sdk');
...
```
To:
```javascript=
const AWSXRay = require('aws-xray-sdk-core');
const AWS = AWSXRay.captureAWS(require('aws-sdk'));
...
```

Now run `sls deploy` again to deploy the code change. This time you can deploy a single function using `sls deploy -f FUNCTION_NAME`, since we only changed the source code, not our **serverless.yml**.

After you deploy, invoke your API Gateway endpoint again:
```bash=
$ curl https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/xxx
```

Go back to your AWS X-Ray console, wait till the new trace to show up. You can tell if a trace is recent by looking at its **Age**:
![](https://i.imgur.com/84WtKO6.png)

Select the new trace.
![](https://i.imgur.com/WOT0RJW.png)

This time:
- Lambda cold start took 461ms, and 185ms to process the request
- Out of the 185ms, DynamoDB query took 73ms and SNS publish call took 98ms


The full version of the example code can be found here - [serverless-example-with-xray](https://github.com/seed-run/serverless-example-with-xray)
