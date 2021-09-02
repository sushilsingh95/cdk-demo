# cdk-demo
In this demo for CDK, we will be creating a CDK stack with following resources:
- A lambda function
- A dynamodb table
- A s3 bucket

although, there would be no real


## Installing the CDK
use the npm to install aws-cdk globally
```bash
npm install -g aws-cdk
```

verify that you cdk is installed and available
```bash
cdk --version
```

## Create a CDK app
Here we are generating a new CDK app
```bash
cdk init app --language typescript 
```

Here we are installing the packages for required for resources that we will be using in our demo
```bash
npm install @aws-cdk/aws-dynamodb @aws-cdk/aws-lambda @aws-cdk/aws-s3
```


## Writing the Code

Below code creates a new lambda function
```typescript
const fn = new lambda.Function(this, 'MyFunction', {
    runtime: lambda.Runtime.NODEJS_12_X,
    handler: 'index.handler',
    code: lambda.Code.fromInline("console.log('Hello from lambda')")
});
```

Following code snippet create a dynamo db table
```typescript
const table = new dynamodb.Table(this, "table", {
    partitionKey: {
        name: "userId",
        type: dynamodb.AttributeType.STRING
    },
    sortKey: {
        name: "noteId",
        type: dynamodb.AttributeType.STRING
    },
    removalPolicy: cdk.RemovalPolicy.DESTROY
});
```

This code creates a new s3 bucket.
```typescript
const bucket = new s3.Bucket(this, 'MyFirstBucket', {
    removalPolicy: cdk.RemovalPolicy.DESTROY
});
```

