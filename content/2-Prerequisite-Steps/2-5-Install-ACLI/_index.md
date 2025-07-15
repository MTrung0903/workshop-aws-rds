---
title : "Install AWS CLI on Local Machine"
date: 2025-07-01
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

### 1.6. Install AWS CLI on Local Machine

1. **Download the installation file**:

- Go to: [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi).

- Download the `AWSCLIV2.msi` file (for Windows) to the default folder (eg: `C:\Users\<YourUser>\Downloads`).

2. **Run the installer**:

- Find the `AWSCLIV2.msi` file, double-click to run.

- Follow the instructions:

- Click **Next** to continue.

- Accept the **License Agreement** and click **Next**.

- Keep the default installation directory (`C:\Program Files\Amazon\AWSCLIV2`) and click **Next**.

- Click **Install**, grant Administrator rights if requested.

- Click **Finish** to complete.

3. **Test the installation**:

- Open **Command Prompt** or **PowerShell** (Win + R, type `cmd` or `powershell`).

- Run:

```bash
aws --version
```
- Example output: `aws-cli/2.27.50 Python/3.13.4 Windows/11 exe/AMD64`.
![image](../../../static/images/tao_aws_cli_local/Screenshot%202025-07-13%20144159.png)
- If the error `aws is not recognized` appears, check the PATH variable:

- Press Win + R, type `sysdm.cpl`, go to the **Advanced** tab > **Environment Variables**.

- In **System Variables**, find **Path**, add `C:\Program Files\Amazon\AWSCLIV2` if it is not there.

- Reopen Command Prompt/PowerShell and try again.

4. **AWS CLI Configuration**:

- Run:
```bash
aws configure
```
- Enter information:

- **AWS Access Key ID**: Get from AWS Management Console:

- Log in: [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/).
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392631.png)
- Go to **Users** > Select IAM user > **Security credentials** > **Create access key**.
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392649.png)
- Select **Command Line Interface (CLI)**, load the CSV file containing the **Access Key ID** and **Secret Access Key**.
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392694.png)
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392743.png)
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392760.png)
- **AWS Secret Access Key**: Import from CSV file.
![image](../../../static/images/tao_aws_cli_local/screenshot_1752392995.png)
- **Default region name**: Enter `us-east-1` (or the region of your choice).

- **Default output format**: Enter `json` or press Enter to use the default.

- The information is saved to:

- `C:\Users\<YourUser>\.aws\credentials`
- `C:\Users\<YourUser>\.aws\config`