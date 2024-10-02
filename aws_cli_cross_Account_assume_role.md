# aws_cli_cross_Account_assume_role
The steps below desribes the procedure to allow access to a user in Account A to access an S3 bucket in Account B using AWS CLI.

## Use case diagram
![crossaccount_access_diagram](crossaccount_access_diagram.png)

## Steps
1) Create a trust role in Account B to provide access to any user in Account A
* Use the below trust policy to create the IAM Role
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::12312321231232:root"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```
* You can follow the UI in the link for steps to create an IAM role: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html#roles-creatingrole-user-console
2) Create an IAM policy and attach it to the trust IAM role
* Use the below policy to provide full access to S3.
```
{
  "Version": "2012-10-17",
  "Statement": [
      {
          "Effect": "Allow",
          "Action": [
              "ec2:*",
              "s3:*"
          ],
          "Resource": "*"
      }
  ]
}
```
