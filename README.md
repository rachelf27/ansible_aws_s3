# AWS Cloud Storage Provisioning

This document is created for provisioning cloud storage buckets in multiple environments using Ansible.

## Prerequisites and Environment Setup

- Valid AWS IAM User account with Access Key and Secret Key 

- Have the following installed on your machine
    ```
    Python
    pip
    ```
- Install Ansible, AWS CLI and AWS SDKs <br>
    `pip install ansible awscli boto boto3`

- Check AWS CLI and Ansible is installed correctly <br>
    `aws --version` <br>
    `ansible --version` 

- Configure the AWS CLI profile as shown below: <br>
    `aws configure`
    ```
    AWS Access Key ID [None]: <AWS_ACCESS_KEY>

    AWS Secret Access Key [None]: <AWS_SECRET_KEY>

    Default region name [None]: <AWS_REGION>

    Default output format [None]: json
    ```
- Set Environment variables
    ```
    export AWS_ACCESS_KEY_ID=<AWS_ACCESS_KEY>
    export AWS_SECRET_ACCESS_KEY=<AWS_SECRET_KEY>
    export AWS_DEFAULT_REGION=<AWS_REGION>
    ```
- Change/Navigate to the Cloud Provisioning Directory

## Creating AWS S3 Buckets

To create new buckets use `create_s3_buckets.yml` playbook with variables.<br>
Substitute the desired bucket name for `bucketNameValue`.<br>
Choose the environment from `hosts` file and pass in the desired environment variable. <br>
Verify the bucket is created.
```
AWS_ACCESS_KEY=$AWS_ACCESS_KEY_ID AWS_SECRET_KEY=$AWS_SECRET_ACCESS_KEY AWS_EC2_REGION=$AWS_DEFAULT_REGION ansible-playbook -i hosts -l local create_s3_buckets.yml -e bucket_name="bucketNameValue" -vvv

aws s3 ls
```

## Deleting S3 Buckets

To delete buckets use `delete_s3_buckets.yml` playbook with variables.<br>
Substitute the desired bucket name for `bucketNameValue`.<br>
Choose the environment from `hosts` file and pass in the desired environment variable. <br>
Verify the bucket is deleted.
```
AWS_ACCESS_KEY=$AWS_ACCESS_KEY_ID AWS_SECRET_KEY=$AWS_SECRET_ACCESS_KEY AWS_EC2_REGION=$AWS_DEFAULT_REGION ansible-playbook -i hosts -l local delete_s3_buckets.yml -e bucket_name="bucketNameValue" -vvv

aws s3 ls
```