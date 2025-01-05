
# Using Amazon Bedrock API: AWS Command Line Interface Request Examples

This guide provides a step-by-step approach to using the Amazon Bedrock API via the AWS Command Line Interface (CLI). It includes examples to help you test your permissions and authentication setup. Before proceeding, ensure you have met the following prerequisites:

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Prerequisites

1. **AWS Account and Permissions**  
   Ensure you have an AWS account with access to a role containing the necessary permissions for Amazon Bedrock. If not, follow the steps in [Getting Started with Amazon Bedrock Roles](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html#getting-started-bedrock-role).

2. **Model Access**  
   Request access to the Amazon Titan Text G1 - Express model. Refer to the [Model Access Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html#getting-started-model-access).

3. **IAM User Credentials**  
   Obtain access keys for an IAM user and configure your AWS CLI profile with these credentials. Refer to the [Guide to Granting Programmatic Access](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started-api.html#grant-program-access).

## Testing Permissions and Access Keys

Use the Amazon Bedrock role to test your setup. These examples assume you have configured the default profile with your access keys.

### Configuration Notes:
- **Minimum Requirements**: A profile with an AWS Access Key ID and AWS Secret Access Key.
- **Temporary Credentials**: If using temporary credentials, ensure you include the AWS Session Token.

---

## Listing Foundation Models Available in Amazon Bedrock

The following example demonstrates how to list the foundation models available in your region using the `ListFoundationModels` operation. Run the following command:

```bash
aws bedrock list-foundation-models --region us-east-1
```

If successful, the response will include a list of foundation models available in Amazon Bedrock for your region.

---

## Submitting Text Prompts with `InvokeModel`

Use the `InvokeModel` operation to submit a text prompt and generate a response from a model. Run the following command:

```bash
aws bedrock-runtime invoke-model \
--model-id amazon.titan-text-express-v1 \
--body '{"inputText": "Describe the purpose of a \"hello world\" program in one line.", "textGenerationConfig" : {"maxTokenCount": 512, "temperature": 0.5, "topP": 0.9}}' \
--cli-binary-format raw-in-base64-out \
invoke-model-output-text.txt
```

### Expected Result:
If the command succeeds, the model-generated response will be written to the file `invoke-model-output-text.txt`. The text response will be included in the `outputText` field.

---

## Submitting Text Prompts with `Converse`

The `Converse` operation allows you to submit prompts and generate responses for multi-turn conversations. We recommend using `Converse` over `InvokeModel` for a unified inference approach. Run the following command:

```bash
aws bedrock-runtime converse \
--model-id amazon.titan-text-express-v1 \
--messages '[{"role": "user", "content": [{"text": "Describe the purpose of a \"hello world\" program in one line."}]}]' \
--inference-config '{"maxTokens": 512, "temperature": 0.5, "topP": 0.9}'
```

### Expected Result:
If the command succeeds, the model-generated response will be returned in the `text` field, along with additional information.

---

By following these steps, you can effectively interact with Amazon Bedrock APIs using the AWS CLI. For additional configurations or troubleshooting, refer to the [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/).

---
