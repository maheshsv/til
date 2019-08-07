# Cross AWS account access with IAM role

Depending on the AWS resources you are working with, there are different ways to grant access to user or role in a different AWS account. But IAM role is a universal and recommended way to fulfill these type of requirements. 

Assuming we need to grant S3 access of AWS account A to a developer user/role/group in AWS account B. The essential steps to implement it are as follows:

1. In AWS account A, create an IAM role with:
    - S3 access permission policy
    - trust AWS account B, usually by adding account id to the trusty accounts
2. In AWS account B, create an IAM policy that can assume the role created in AWS account A.
3. In AWS account B, attach the IAM policy to the developer user/role/group.

References:
- [Tutorial: Delegate Access Across AWS Accounts Using IAM Roles
](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)
- [How do I allow users from another account to access resources in my account through IAM?](https://aws.amazon.com/premiumsupport/knowledge-center/cross-account-access-iam/)
