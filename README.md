## Description.

Here we are going to create a IAM user with custom policy to start, stop and restart aws instances based on name tags.

### prerequisite for this project

- IAM user with custom policy
- AWS instances

## IAM POLICY

```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:Describe*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:StartInstances",
                "ec2:StopInstances",
                "ec2:RebootInstances"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/Project": "zomato",
                    "aws:ResourceTag/Env": "dev"
                }
            }
        }
    ]
}
```
