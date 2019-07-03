# How to enable access logs for API Gateway?

Just a quick recap, there are two ways of API logging:
- execution logs: logs detailed information as API Gateway goes through each step of processing the request. Useful for tracing individual requests.
- access logs: logs who has accessed your API. Each request generates a single entry in the logs similar to NGINX logs. Useful for sending to analytics tool to gather metrics.

### For Seed users
You can enable with 1 click. Here is the doc..

### Enable API Gateway Access logs
This is a two step process. First, we need to create an IAM role that allows API Gateway to write logs in CloudWatch. Then we need to turn on logging for our API project.

First, log in to your [AWS Console](https://console.aws.amazon.com/) and select IAM from the list of services.

![](https://d33wubrfki0l68.cloudfront.net/07bc0503a7d837f6f3c284b498d225b58dac783f/aa9a2/assets/logging/select-iam-service.png)

Select Roles on the left menu.
![](https://d33wubrfki0l68.cloudfront.net/fbc6e501d1350a7177a00cf593d0749d14c6e326/b3770/assets/logging/select-iam-roles.png)


Select Create Role.
![](https://d33wubrfki0l68.cloudfront.net/8857bba78f8b2c909a80d8989788fc254d433c3f/267bd/assets/logging/select-create-iam-role.png)


Under AWS service, select API Gateway.
![](https://d33wubrfki0l68.cloudfront.net/6f777a1046a80b7b200b64b1e971330191e7f3fe/49e68/assets/logging/select-api-gateway-iam-role.png)


Click Next: Permissions.
![](https://d33wubrfki0l68.cloudfront.net/f29c9b06f7b09832dd25f788fac7cebcfc94a866/164f3/assets/logging/select-iam-role-attach-permissions.png)


Click Next: Review.
![](https://d33wubrfki0l68.cloudfront.net/ebbba71519556778ac91a19fcc0c40421084c7d8/a8471/assets/logging/select-review-iam-role.png)


Enter a Role name and select Create role. In our case, we called our role ```APIGatewayCloudWatchLogs```.
![](https://d33wubrfki0l68.cloudfront.net/d7cee9dcd3dc60673426940c059c9f1fe1ff6698/a7390/assets/logging/fill-in-iam-role-info.png)


Click on the role we just created.
![](https://d33wubrfki0l68.cloudfront.net/8c66c2eeacb2a0e946276671988746a0f1ad23e8/66076/assets/logging/select-created-api-gateway-iam-role.png)


Take a note of the Role ARN. We will be needing this soon.
![](https://d33wubrfki0l68.cloudfront.net/f308acfc467e0e31b2543785e62ee37170289bb9/1d8c5/assets/logging/iam-role-arn.png)

Now that we have created our IAM role, let’s turn on logging for our API Gateway project.

Go back to your [AWS Console](https://console.aws.amazon.com/) and select API Gateway from the list of services.

![](https://d33wubrfki0l68.cloudfront.net/43d4ff3647df55040a6b5e34df09aa3bdd45a059/9bc20/assets/logging/select-api-gateway-service.png)


Select Settings from the left panel.
![](https://d33wubrfki0l68.cloudfront.net/e6fc71499ce75b914437ee6cba01b236c32569c8/2bc8b/assets/logging/select-api-gateway-settings.png)


Enter the ARN of the IAM role we just created in the CloudWatch log role ARN field and hit Save.
![](https://d33wubrfki0l68.cloudfront.net/9915ca6535e00478ea77b6bce1c8a136b9ddb4b0/af784/assets/logging/fill-in-api-gateway-cloudwatch-info.png)


Select your API project from the left panel, select Stages, then pick the stage you want to enable logging for. For the case of our Notes App API, we deployed to the prod stage.

![](https://i.imgur.com/SaMWPQT.png)

In the Logs tab:

- Check Enable Access Logging.
- Enter a CloudWatch Group name with the API Gateway id and stage name to ensure uniqueness
```
API-Gateway-Access-Logs_{API_GATEWAT_ID}/{STAGE}
```
- Enter Log Format or pick one of the predefined log format in CLF, JSON, XML or CSV
```
{ "requestId":"$context.requestId",
  "ip": "$context.identity.sourceIp",
  "caller":"$context.identity.caller",
  "user":"$context.identity.user",
  "requestTime":"$context.requestTime",
  "httpMethod":"$context.httpMethod",
  "resourcePath":"$context.resourcePath",
  "status":"$context.status",
  "protocol":"$context.protocol",
  "responseLength":"$context.responseLength"
}
```

![](https://i.imgur.com/sFuNC6U.png)


Scroll to the bottom of the page and click Save Changes. Now our API Gateway requests should be logged via CloudWatch.


### Enable API Gateway Access logs

CloudWatch groups log entries into Log Groups and then further into Log Streams. Log Groups and Log Streams can mean different things for different AWS services. For API Gateway, when logging is first enabled in an API project’s stage, API Gateway creates 1 log group for the stage, and 300 log streams in the group ready to store log entries. API Gateway picks one of these streams when there is an incoming request.

To view API Gateway logs, log in to your AWS Console and select CloudWatch from the list of services.

![](https://d33wubrfki0l68.cloudfront.net/eff00ffdc2b2680ebeeac8c09db64c1db8431d29/e69b0/assets/logging/select-cloudwatch-service.png)

Select Logs from the left panel.

![](https://d33wubrfki0l68.cloudfront.net/93be646196ce32a9e020f95e53a2a5d62c4a4df9/bfcbc/assets/logging/select-cloudwatch-logs.png)

Select the log group prefixed with API-Gateway-Access-Logs_ followed by the API Gateway id.

![](https://i.imgur.com/MRzcT9g.png)


You should see 300 log streams ordered by the last event time. This is the last time a request was recorded. Select the first stream.

![](https://i.imgur.com/HRUk6pD.png)


This shows you one log entry for each API request. Expand a row, the log data should reflect the format you previously defined.

![](https://i.imgur.com/T3I2Kfv.png)

Note that two consecutive groups of logs are not necessarily two consecutive requests in real time. This is because there might be other requests that are processed in between these two that were picked up by one of the other log streams.
