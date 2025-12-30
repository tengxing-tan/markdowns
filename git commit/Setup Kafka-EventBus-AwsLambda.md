To define a Lambda function, EventBridge bus, and Kafka event source mapping (ESM), follow this step-by-step guide based on current 2025 AWS standards.

# 1. Define the Lambda Function

- **Create Function:** Navigate to the AWS Lambda Console and select **Create function**. Choose **Author from scratch**, provide a name, and select a runtime such as Python 3.11 or Node.js.
- **Configure IAM Role:** Ensure the function’s execution role has permissions to read from Kafka (e.g., `AWSLambdaMSKExecutionRole`) and manage network interfaces if using a VPC.
- **Network Settings:** If your Kafka cluster is in a VPC, configure the Lambda with the same VPC, private subnets, and appropriate security groups. 

# 2. Define the EventBridge Bus

- **Create Custom Bus:** In the Amazon EventBridge Console, go to **Event buses** and select **Create event bus**. Give it a unique name (e.g., `kafka-sink-bus`).
- **Configure Rules (Optional):** Define rules on this bus to route events to other targets (like SQS or SNS) based on specific patterns.
- **Pipes Integration:** For a streamlined Kafka-to-EventBridge flow, consider using **EventBridge Pipes**, which connects a Kafka source directly to an EventBridge bus target without needing custom polling code. 

# 3. Define the Kafka Event Source Mapping (ESM) 

You can now create this mapping directly from the Amazon MSK console as of November 2025. 

- **Using the MSK Console:** Navigate to your cluster, go to the **Lambda integration** tab, and provide the target Lambda function and topic name.
- **Using the Lambda Console:**
    1. Select **Add trigger** in the function overview.
    2. Select **Apache Kafka** or **MSK**.
    3. Enter the **Bootstrap servers**, **Topic name**, and **Starting position** (e.g., LATEST).
    4. Configure **Authentication** (e.g., SASL/SCRAM or TLS) using secrets from AWS Secrets Manager if required.
- **Using AWS CLI:** Run the following command to create the mapping programmatically:

```bash
aws lambda create-event-source-mapping \
  --function-name YourFunctionName \
  --event-source-arn arn:aws:kafka:region:account:cluster/YourCluster \
  --topics YourTopicName \
  --starting-position LATEST
```

# 4. Verification and Testing

- **Check Status:** Ensure the trigger status in the Lambda console changes from **Creating** to **Enabled**.
- **Test Payload:** Use the [Lambda Test tab](https://docs.aws.amazon.com/lambda/latest/dg/testing-functions.html) to simulate a Kafka record, which is delivered as a base64-encoded string in an array of records.