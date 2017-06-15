# AWS Lambda + Serverless
- Lambda Doc: http://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html
- Serverless Doc: https://serverless.com/framework/docs/providers/aws/cli-reference/deploy/

Workflow:

```
// first time
sls deploy

// update just code
sls deploy function -f FUNCTION_NAME

// tail log
sls logs -f FUNCTION_NAME -t
```
