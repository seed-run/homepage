# How to debug DynamoDB timeouts for Serverless application?

## Our issue
- Not single type of call timed out. Timeouts were observed across BatchGet, Get, Query, Update apis.
- DynamoDB call timeout rate was around 0.00002%
- We confirmed it with Mike Apted @mikeapted that the 0.00002% timeout rate we observed is normal.

## Cause 1: HTTP connections are timing out
- AWS NodeJS SDK has 2 settings:
  - HTTP Connect Timeout - Sets the socket to timeout after failing to establish a connection with the server after connectTimeout milliseconds. This timeout has no effect once a socket connection has been established.
  - HTTP Timeout - Sets the socket to timeout after timeout milliseconds of inactivity on the socket. Defaults to two minutes.
- Note the default HTTP timeout is 120 seconds.
- In Lambda + API Gateway setting:
  - API Gateway has a maximum timeout setting of 29s.
  - Lambda shoould have a timeout lesser than 29s
  - And it only makes sense for DynamoDB's connection timeout to be lesser than that of Lambda.
- In fact, we want to keep it short. If DynamoDB times out, we want it to fail quick and retry again. We want the DynamoDB calls to timeout before Lambda and API Gateway timeout.
- Change connection timeout for DynamoDB client
```
import AWS from 'aws-sdk';
const dynamoDb = new AWS.DynamoDB.DocumentClient({
  httpOptions: {
    timeout: 5000,
  }
});
```


## Cause 2: Retries take long
- When an AWS API call fails, the response specifies if the error is retryable.
- By default, AWS NodeJS client auto-retries retryable errors. And it uses an exponential backoff strategy for operation retries.
- For API calls to most services, by default, the client auto-retries up to 3 times, with 100ms wait before the first retry, 200ms before the second, and 400ms before the third retry.
- For API calls to DynamoDb, by default, the client auto-retries up to 10 times, with 50ms wait before the first retry, then 100ms, 200ms, 400ms ... 25600ms before the last retry.
- The worst case scenario for a failed DynamoDB call could take over 50 seconds to return the failure.
- We need to make the DynamoDB call fail before the Lambda times out so we can catch the failure.
- Change the retry count for DynamoDB client
```
import AWS from 'aws-sdk';
const dynamoDb = new AWS.DynamoDB.DocumentClient({
  maxRetries: 3,
});
```

## Special shoutout to Mike Apted (@mikeapted), Adriano Raiano (@adrirai), and Carl Nordenfelt (@carl_nordenfelt) in helping us pinning down the issue.
