# What's the difference between access and execution logs for API Gateway?

There are two types of API logging in CloudWatch: execution logging and access logging.

### Execution logging
- logs the API Gateway internal information as the request is processed  
- fully managed by API Gateway
- API Gateway automatically creates a CloudWatch log group with name ```API-Gateway-Execution-Logs_{rest-api-id}/{stage_name}```
- log format is pre-defined, you can only choose the log level (INFO or ERROR) and whether or not to log full api request/response data
- the screenshot shows log data for a single request, it contains:
  - request url
  - request data received by API Gateway
  - request data sent to Lambda function
  - response received from Lambda function
  - response sent by API Gateway
  - details on usage plan and API key used to process the request, etc

- Execution logs are useful when you need to debug a specific request and trace down the issue.
- Execution logs can generate lots of log data, and a large CloudWatch bill.

![](https://i.imgur.com/bQD0wcZ.png)
![](https://i.imgur.com/F37rZ18.png)


### Access logging
- logs who has accessed your API, similar to NGINX logs
- managed by the developer
- you are responsible of creating the CloudWatch log groups
- you define the log format. It can be anything CLF (Common Log Format), JSON, XML, CSV, etc.
- you have access to the data inside the $context variable, including:
  - caller's IP address
  - request time
  - request HTTP method
  - request url
  - response HTTP status code, etc

  An example of the log format in JSON looks like:
```
{ "requestId":"$context.requestId", \
  "ip": "$context.identity.sourceIp", \
  "caller":"$context.identity.caller", \
  "user":"$context.identity.user", \
  "requestTime":"$context.requestTime", \
  "httpMethod":"$context.httpMethod", \
  "resourcePath":"$context.resourcePath", \
  "status":"$context.status", \
  "protocol":"$context.protocol", \
  "responseLength":"$context.responseLength" \
}
```

- Access logs are useful for collecting analytical data about your API. You can feed the logs directly to analytics services.
- With CloudWatch insights, you can directly query against access logs

![](https://i.imgur.com/Qd3AOJe.png)

