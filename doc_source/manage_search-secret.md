# Find secrets in AWS Secrets Manager<a name="manage_search-secret"></a>

When you search for secrets without a filter, Secrets Manager matches keywords in the secret name, description, tag key, and tag value\. Searching without filters is not case\-sensitive and ignores special characters, such as space, /, \_, =, \#, and only uses numbers and letters\. When you search without a filter, Secrets Manager analyzes the search string to convert it to separate words\. The words are separated by any change from uppercase to lowercase, from letter to number, or from number/letter to punctuation\. For example, entering the search term `credsDatabase#892` searches for `creds`, `Database`, and `892` in name, description, and tag key and value\.

You can apply the following filters to your search:

**Name**  
Matches the beginning of secret names; case\-sensitive\. For example, **Name:** **Data** returns a secret named DatabaseSecret, but not databaseSecret or MyData\. 

**Description**  
Matches the words in secret descriptions, not case\-sensitive\. For example, **Description**: **My Description** matches secrets with the following descriptions:   
+ My Description
+ my description
+ My basic description
+ Description of my secret

**Owning service**  
Matches the beginning of the managing service ID prefix, not case\-sensitive\. For example, **my\-ser** matches secrets managed by services with the prefix my\-serv and my\-service\. For more information, see [Secrets managed by other services](service-linked-secrets.md)\. 

**Replicated secrets**  
You can filter for primary secrets, replica secrets, or secrets that aren't replicated\.

**Tag keys**  
Matches the beginning of tag keys; case\-sensitive\. For example, **Tag key:** **Prod** returns secrets with the tag Production and Prod1, but not secrets with the tag prod or 1 Prod\.

**Tag values**  
Matches the beginning of tag values; case\-sensitive\. For example, **Tag value:** **Prod** returns secrets with the tag Production and Prod1, but not secrets with the tag value prod or 1 Prod\. 

Secrets Manager is a regional service and only secrets within the selected region are returned\.

## AWS CLI<a name="manage_search-secret_cli"></a>

**Example List the secrets in your account**  
The following [https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/list-secrets.html](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/list-secrets.html) example gets a list of the secrets in your account\.  

```
aws secretsmanager list-secrets
```

**Example Filter the list of secrets in your account**  
The following [https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/list-secrets.html](https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/list-secrets.html) example gets a list of the secrets in your account that have **Test** in the name\. Filtering by name is case sensitive\.  

```
aws secretsmanager list-secrets \
    --filter Key="name",Values="Test"
```
Filter keys you can use:  
+ `description`
+ `name`
+ `tag-key`
+ `tag-value`
+ `owning-service`
+ `primary-region`
+ `all` \(searches all of the above keys\)

## AWS SDK<a name="manage_search-secret_sdk"></a>

To find secrets by using one of the AWS SDKs, use [https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_ListSecrets.html](https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_ListSecrets.html)\. For more information, see [AWS SDKs](asm_access.md#asm-sdks)\.

