# AWS CloudFormation Template for AWS Config, HIPAA/GDPR Rules, and Service Control Policies (SCPs)

This CloudFormation template enables AWS Config, configures compliance rules for HIPAA and GDPR, and sets up Service Control Policies (SCPs) in AWS Organizations. It is designed to help you enforce compliance and security best practices across your AWS accounts.

---

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Template Details](#template-details)
4. [Deployment Instructions](#deployment-instructions)
5. [Resources Created](#resources-created)
6. [Outputs](#outputs)
7. [Customization](#customization)
8. [Troubleshooting](#troubleshooting)
9. [Cleanup](#cleanup)

---

## Overview

This CloudFormation template automates the setup of the following AWS services and features:
1. **AWS Config**:
   - Enables configuration recording for all supported resources.
   - Delivers configuration snapshots to an S3 bucket.
   - Sends notifications to an SNS topic for configuration changes.
2. **AWS Config Rules**:
   - Enables prebuilt rules for HIPAA/GDPR compliance.
3. **Service Control Policies (SCPs)**:
   - Prevents accounts from leaving the organization.
   - Prevents accounts from disabling AWS Config.

---

## Prerequisites

Before deploying this template, ensure the following:
1. **AWS Organizations**:
   - You must have AWS Organizations enabled.
   - This template should be deployed in the **management account** of your organization.
2. **Permissions**:
   - You need sufficient IAM permissions to create the resources defined in the template.
3. **S3 Bucket**:
   - The template creates an S3 bucket for AWS Config logs. Ensure the bucket name is unique.
4. **SNS Topic**:
   - The template creates an SNS topic for notifications. Ensure you subscribe to the topic to receive alerts.

---

## Template Details

### Resources Created
1. **AWS Config Configuration Recorder**:
   - Records configuration changes for all supported resources.
2. **AWS Config Delivery Channel**:
   - Specifies an S3 bucket and SNS topic for storing and notifying about configuration changes.
3. **IAM Role**:
   - Grants AWS Config permissions to write to the S3 bucket and publish to the SNS topic.
4. **S3 Bucket**:
   - Stores AWS Config logs.
5. **SNS Topic**:
   - Sends notifications for AWS Config events.
6. **AWS Config Rules**:
   - Enables prebuilt rules for HIPAA/GDPR compliance.
7. **Service Control Policies (SCPs)**:
   - Prevents accounts from leaving the organization.
   - Prevents accounts from disabling AWS Config.

### Parameters
- The template does not require any input parameters. All resources are created with default names and configurations.

### Outputs
- The template outputs the following:
  - S3 bucket name for AWS Config logs.
  - SNS topic ARN for notifications.
  - IAM role ARN for AWS Config.

---

## Deployment Instructions

### Step 1: Download the Template
Save the CloudFormation template provided in this repository as a `.yaml` file (e.g., `config-hipaa-gdpr-scp.yaml`).

### Step 2: Deploy the Template
1. Open the **AWS Management Console**.
2. Navigate to **CloudFormation**.
3. Click **Create Stack** > **With new resources (standard)**.
4. Upload the template file (`config-hipaa-gdpr-scp.yaml`).
5. Provide a **Stack Name** (e.g., `Config-HIPAA-GDPR-SCP`).
6. Click **Next** and proceed through the wizard.
7. On the **Review** page, acknowledge that the template may create IAM resources.
8. Click **Create Stack**.

### Step 3: Verify Deployment
1. Once the stack creation is complete, check the **Outputs** tab for the S3 bucket name, SNS topic ARN, and IAM role ARN.
2. Verify that AWS Config is enabled in your account.
3. Subscribe to the SNS topic to receive notifications.

---

## Resources Created

### AWS Config
- **Configuration Recorder**: Records configuration changes for all supported resources.
- **Delivery Channel**: Delivers configuration snapshots to the S3 bucket and sends notifications to the SNS topic.
- **IAM Role**: Grants AWS Config the necessary permissions.

### S3 Bucket
- Stores AWS Config logs.
- Versioning is enabled to protect against accidental deletions.

### SNS Topic
- Sends notifications for AWS Config events.

### AWS Config Rules
- **HIPAA Compliance Rule**: Ensures resources comply with HIPAA requirements.
- **GDPR Compliance Rule**: Ensures resources comply with GDPR requirements.

### Service Control Policies (SCPs)
- **DenyLeavingOrganization**: Prevents accounts from leaving the organization.
- **DenyDisablingConfig**: Prevents accounts from disabling AWS Config.

---

## Outputs

The template outputs the following:
1. **ConfigS3BucketName**: Name of the S3 bucket for AWS Config logs.
2. **ConfigSnsTopicArn**: ARN of the SNS topic for AWS Config notifications.
3. **ConfigRoleArn**: ARN of the IAM role for AWS Config.

---

## Customization

### Modify AWS Config Rules
- To customize the AWS Config rules, update the `InputParameters` section in the `HIPAAConfigRule` and `GDPRConfigRule` resources.

### Add Additional SCPs
- To add more SCPs, create additional `AWS::Organizations::Policy` resources in the template.

### Change S3 Bucket Name
- Update the `BucketName` property in the `ConfigS3Bucket` resource to use a custom name.

---

## Troubleshooting

### AWS Config Not Enabled
- Ensure the IAM role has the correct permissions.
- Verify that the S3 bucket and SNS topic were created successfully.

### SCPs Not Applied
- Ensure the template is deployed in the management account of your organization.
- Verify that AWS Organizations is enabled.

### SNS Notifications Not Received
- Subscribe to the SNS topic using your email or other supported protocols.

---

## Cleanup

To delete the resources created by this template:
1. Open the **AWS Management Console**.
2. Navigate to **CloudFormation**.
3. Select the stack you created (e.g., `Config-HIPAA-GDPR-SCP`).
4. Click **Delete**.
5. Confirm the deletion.

**Note**: Deleting the stack will remove all resources created by the template, including the S3 bucket and SNS topic.

---

## References
- [AWS Config Documentation](https://docs.aws.amazon.com/config/)
- [AWS Organizations SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [HIPAA Compliance on AWS](https://aws.amazon.com/compliance/hipaa-compliance/)
- [GDPR Compliance on AWS](https://aws.amazon.com/compliance/gdpr-center/)
