---
title : "Create IAM Role for ECR"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

### 1.5. Create IAM Role for ECR

1. **Access IAM Console**: 
- Open: [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/).
![image](../../../static/images/tao_role/screenshot_1752390613.png)
2. **Create an ECR Reading Policy**: 
- Select **Policies** > **Create Policy**. 
- Select the **Elastic Container Registry** service. 
![image](../../../static/images/tao_role/Screenshot%202025-07-13%20141451.png)
- **Permissions**: 
- **List**: `DescribeImages`, `ListImages`. 
- **Read**: `BatchGetImage`, `DescribeRepositories`, `GetAuthorizationToken`, `GetAccountSetting`.
![image](../../../static/images/tao_role/screenshot_1752391075.png)
- **Resources**: Select **Any in this account**.
![image](../../../static/images/tao_role/screenshot_1752391123.png)
- **Policy name**: `ReadECRRepositoryContent`.
- **Description**: "Allow pulling images and viewing repository information".
![image](../../../static/images/tao_role/screenshot_1752391177.png)
- Click **Create policy**.
![image](../../../static/images/tao_role/screenshot_1752391191.png)
3. **Create ECR Record Policy**:
- Similarly, select **Elastic Container Registry**.
- **Permissions**:
- **Read**: `BatchCheckLayerAvailability`, `GetAuthorizationToken`.
- **Write**: `CompleteLayerUpload`, `InitiateLayerUpload`, `PutImage`, `UploadLayerPart`.
- **Resources**: Select **Any in this account**.
- **Policy name**: `WriteECRRepositoryContent`.
![image](../../../static/images/tao_role/screenshot_1752391466.png)
- **Description**: "Allow pushing and deleting images".
- Click **Create policy**.
![image](../../../static/images/tao_role/screenshot_1752391531.png)
![image](../../../static/images/tao_role/screenshot_1752391573.png)
4. **Create IAM Role**:

- Select **Roles** > **Create role** > **AWS service** > **EC2**.
![image](../../../static/images/tao_role/screenshot_1752391638.png)
![image](../../../static/images/tao_role/screenshot_1752391696.png)
- Attach 2 policies: `ReadECRRepositoryContent`, `WriteECRRepositoryContent`.
![image](../../../static/images/tao_role/screenshot_1752391715.png)
- **Role name**: `CustomRWECRRole`.
- **Description**: "Role allows reading and writing ECR".
![image](../../../static/images/tao_role/screenshot_1752391754.png)
- Click **Create role**.
![image](../../../static/images/tao_role/screenshot_1752391780.png)
5. **Verify**:

- Check in **IAM Console** to make sure the `CustomRWECRRole` role has been created and the correct policies have been attached.