### Implementation

In this exercise, you will have to write a Lambda function that sends an HTTP request every minute and records metrics for this request.

You would have to generate two data points:

If a request was successful or not

Time it took to execute a request.

To generate a single data point, you need to use the following code:

await cloudwatch.putMetricData({
  
  MetricData: [ // A list of data points to send
    
    {
      MetricName: 'Success', // Name of a metric
      Dimensions: [ // A list of key-value pairs that can be used to filter metrics from CloudWatch
        {
          Name: 'ServiceName',
          Value: serviceName
        }
      ],
      Unit: 'Count', // Unit of a metric
      Value: value // Value of a metric to store
    }
  ],
  
  Namespace: 'Udacity/Serveless' // An isolated group of metrics
}).promise()

To call a function every minute, you would need to use CloudWatch Events as an event source for your Lambda function just as we did this in this lesson.

### Build the project

Install dependencies by running the following command:

*npm install*

Once the dependencies are installed, you can build a .zip package that can be deployed to AWS Lambda:

*npm run package*

This should create a file called http-metrics.zip.

You would also need to set correct IAM permissions for a Lambda function to send metrics to AWS CloudWatch. You can copy an IAM policy from the iam-policy.json file in this project.

### Deployment

You need to deploy a .zip package to your Lambda function.

To set environment variables for a function, you need to scroll to the "Environment variables" section in the AWS Lambda interface.
