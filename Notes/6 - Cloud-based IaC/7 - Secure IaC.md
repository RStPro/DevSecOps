## Secure Cloud IaC Best Practices

### For Both CloudFormation and Terraform

- **Version Control:** store IaC code in version control systems like Git to track changes, facilitate collaboration, and maintain a version history.
- **Least Privilege Principle:** always assign the least permissions and scope for credentials and IaC tools. Only grant the needed permissions for the actions to be performed.
- **Parameterize Sensitive Data:** Use parameterize to handle credentials or API keys and avoid hardcoding secrets directly into the IaC code.
- **Secure Credential Management:** leverage the cloud platform's secure credential management solutions or services to securely handle and store sensitive information, e.g., vaults for secret management.
- **Audit Trails:** enable logging and monitoring features to maintain an audit trail of changes made through IaC tools. Use these logs to conduct reviews periodically.
- **Code Reviews:** implement code reviews to ensure IaC code adheres to best security practices. Collaborative review processes can catch potential security issues early.

Check out the [Source Code Security](https://tryhackme.com/room/sourcecodesecurity) room to learn more about this area.

### For AWS CloudFormation

- **Use IAM Roles:** Assign [Identity and Access Management](https://aws.amazon.com/iam/?gclid=Cj0KCQiAm4WsBhCiARIsAEJIEzXouhhd93RvbhqE9xDx8UN65Y44Gq19qsHQf_D5yk9QkScSLgQwvDgaAtOWEALw_wcB&trk=35b38fd8-ca20-4fe2-b46d-16f845a47e34&sc_channel=ps&ef_id=Cj0KCQiAm4WsBhCiARIsAEJIEzXouhhd93RvbhqE9xDx8UN65Y44Gq19qsHQf_D5yk9QkScSLgQwvDgaAtOWEALw_wcB:G:s&s_kwcid=AL!4422!3!651612449969!e!!g!!amazon%20iam!19836376240!155574317508) (IAM) roles with the minimum required permissions to CloudFormation stacks. Avoid using long-term access keys when possible.
- **Secure Template Storage:** store CloudFormation templates in an encrypted [S3 bucket](https://aws.amazon.com/s3/) and restrict access to only authorized users or roles.
- **Stack Policies:** implement stack policies to control updates to stack resources and enforce specific conditions during updates.

### For Terraform

- **Backend State Encryption:** enable backend state encryption to protect sensitive information stored in the Terraform state file.
- **Use Remote Backends:** store the Terraform state remotely using backends like Amazon S3 or Azure Storage. This enhances collaboration and provides better security.
- **Variable Encryption:** consider encrypting sensitive values using tools like HashiCorp Vault or other secure key management solutions when using variables.
- **Provider Configuration:** Securely configure provider credentials using environment variables, variable files, or other secure methods.