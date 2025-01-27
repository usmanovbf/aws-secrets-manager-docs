# Create an AWS Secrets Manager secret<a name="create_secret"></a>

To store API keys, access tokens, credentials that aren't for databases, and other secrets in Secrets Manager, follow these steps\. For an Amazon ElastiCache secret, if you want to turn on rotation, you must store the secret in the [expected JSON structure](reference_secret_json_structure.md#reference_secret_json_structure_ELC)\.

To create a secret, you need the permissions granted by the **SecretsManagerReadWrite** [AWS managed policy](reference_available-policies.md)\.

**To create a secret \(console\)**

1. Open the Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. Choose **Store a new secret**\.

1. On the **Choose secret type** page, do the following:

   1. For **Secret type**, choose **Other type of secret**\.

   1. In **Key/value pairs**, either enter your secret in **Key/value** pairs, or choose the **Plaintext** tab and enter the secret in any format\. We recommend JSON\. You can store up to 65536 bytes in the secret\.

   1. For **Encryption key**, choose the AWS KMS key that Secrets Manager uses to encrypt the secret value:
      + For most cases, choose **aws/secretsmanager** to use the AWS managed key for Secrets Manager\. There is no cost for using this key\.
      + If you need to access the secret from another AWS account, or if you want to use your own KMS key so that you can rotate it or apply a key policy to it, choose a customer managed key from the list or choose **Add new key** to create one\. For information about the costs of using a customer managed key, see [Pricing](intro.md#asm_pricing)\.

        You must have the following permissions to the key: `kms:Encrypt`, `kms:Decrypt`, and `kms:GenerateDataKey`\. For more information about cross\-account access, see [Permissions to AWS Secrets Manager secrets for users in a different account](auth-and-access_examples_cross.md)\. 

   1. Choose **Next**\.

1. On the **Configure secret** page, do the following:

   1. Enter a descriptive **Secret name** and **Description**\. Secret names must contain 1\-512 Unicode characters\.

   1. \(Optional\) In the **Tags** section, add tags to your secret\. For tagging strategies, see [Tag AWS Secrets Manager secrets](managing-secrets_tagging.md)\. Don't store sensitive information in tags because they aren't encrypted\.

   1. \(Optional\) In **Resource permissions**, to add a resource policy to your secret, choose **Edit permissions**\. For more information, see [Attach a permissions policy to an AWS Secrets Manager secret](auth-and-access_resource-policies.md)\.

   1. \(Optional\) In **Replicate secret**, to replicate your secret to another AWS Region, choose **Replicate secret**\. You can replicate your secret now or come back and replicate it later\. For more information, see [Replicate a secret to other Regions](create-manage-multi-region-secrets.md)\.

   1. Choose **Next**\.

1. \(Optional\) On the **Configure rotation** page, you can turn on automatic rotation\. You can also keep rotation off for now and then turn it on later\. For more information, see [Rotate secrets](rotating-secrets.md)\. Choose **Next**\.

1. On the **Review** page, review your secret details, and then choose **Store**\.

   Secrets Manager returns to the list of secrets\. If your new secret doesn't appear, choose the refresh button\.

## AWS CLI<a name="create_secret_cli"></a>

When you enter commands in a command shell, there is a risk of the command history being accessed or utilities having access to your command parameters\. See [Mitigate the risks of using the AWS CLI to store your AWS Secrets Manager secrets](security_cli-exposure-risks.md)\.

**Example Create a secret**  
The following [https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/create-secret.html](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/create-secret.html) example creates a secret with two key\-value pairs\.  

```
aws secretsmanager create-secret \
    --name MyTestSecret \
    --description "My test secret created with the CLI." \
    --secret-string "{\"user\":\"diegor\",\"password\":\"EXAMPLE-PASSWORD\"}"
```

**Example Create a secret from credentials in a JSON file**  
The following [https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/create-secret.html](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/create-secret.html) example creates a secret from credentials in a file\. For more information, see [Loading AWS CLI parameters from a file](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-parameters-file.html) in the AWS CLI User Guide\.  

```
aws secretsmanager create-secret \
    --name MyTestSecret \
    --secret-string file://mycreds.json
```
Contents of mycreds\.json:  

```
{
    "username": "diegor",
    "password": "EXAMPLE-PASSWORD"
}
```

## AWS SDK<a name="create_secret_sdk"></a>

To create a secret by using one of the AWS SDKs, use the [https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_CreateSecret.html](https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_CreateSecret.html) action\. For more information, see [AWS SDKs](asm_access.md#asm-sdks)\.