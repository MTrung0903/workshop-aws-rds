---
title : "Tạo IAM Role cho ECR"
date: 2025-07-01
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

### 1.5. Tạo IAM Role cho ECR

1. **Truy cập IAM Console**:
   - Mở: [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/).
   ![image](/images/tao_role/screenshot_1752390613.png)
2. **Tạo Policy đọc ECR**:
   - Chọn **Policies** > **Create Policy**.
   - Chọn dịch vụ **Elastic Container Registry**.
   ![image](/images/tao_role/Screenshot%202025-07-13%20141451.png)
   - **Permissions**:
     - **List**: `DescribeImages`, `ListImages`.
     - **Read**: `BatchGetImage`, `DescribeRepositories`, `GetAuthorizationToken`, `GetAccountSetting`.
     ![image](/images/tao_role/screenshot_1752391075.png)
   - **Resources**: Chọn **Any in this account**.
   ![image](/images/tao_role/screenshot_1752391123.png)
   - **Policy name**: `ReadECRRepositoryContent`.
   - **Description**: "Cho phép kéo images và xem thông tin repository".
   ![image](/images/tao_role/screenshot_1752391177.png)
   - Nhấn **Create policy**.
   ![image](/images/tao_role/screenshot_1752391191.png)
3. **Tạo Policy ghi ECR**:
   - Tương tự, chọn **Elastic Container Registry**.
   - **Permissions**:
     - **Read**: `BatchCheckLayerAvailability`, `GetAuthorizationToken`.
     - **Write**: `CompleteLayerUpload`, `InitiateLayerUpload`, `PutImage`, `UploadLayerPart`.
   - **Resources**: Chọn **Any in this account**.
   - **Policy name**: `WriteECRRepositoryContent`.
   ![image](/images/tao_role/screenshot_1752391466.png)
   - **Description**: "Cho phép đẩy và xóa images".
   - Nhấn **Create policy**.
   ![image](/images/tao_role/screenshot_1752391531.png)
   ![image](/images/tao_role/screenshot_1752391573.png)
4. **Tạo IAM Role**:
   - Chọn **Roles** > **Create role** > **AWS service** > **EC2**.
   ![image](/images/tao_role/screenshot_1752391638.png)
   ![image](/images/tao_role/screenshot_1752391696.png)
   - Gắn 2 policy: `ReadECRRepositoryContent`, `WriteECRRepositoryContent`.
   ![image](/images/tao_role/screenshot_1752391715.png)
   - **Role name**: `CustomRWECRRole`.
   - **Description**: "Role cho phép đọc và ghi ECR".
   ![image](/images/tao_role/screenshot_1752391754.png)
   - Nhấn **Create role**.
   ![image](/images/tao_role/screenshot_1752391780.png)
5. **Xác minh**:
   - Kiểm tra trong **IAM Console** để đảm bảo role `CustomRWECRRole` đã được tạo và gắn đúng policies.