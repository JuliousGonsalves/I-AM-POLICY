## Description

Here we are going to create a IAM user with custom policy to start, stop and restart aws instances based on name tags.

## Scenario

In a live project enviroment, If you require to provide a dev to start , stop and restart only dev instances. So that we can limit the action a dev can do in the EC2
So we are going to create 3 Instance with custom tags as follows. You can add tags to match your requirement and tweak the policies based on your tags.

# 1. Name = webserver, Env = dev,  Project = zomato

![webserver1](https://user-images.githubusercontent.com/98936958/157377116-a1d5aaa2-7318-468e-9f8c-5f424fa331e4.PNG)

# 2. Name = webserver, Env = prod,  Project = zomato

![webserver2](https://user-images.githubusercontent.com/98936958/157377122-7a01d75d-e9ff-4247-8ef6-26058d149488.PNG)

# 3. Name = webserver, Env = prod,  Project = uber

![webserver3](https://user-images.githubusercontent.com/98936958/157377124-ebeb2e18-7167-4cfe-b9ba-51a4338daf5c.PNG)

## prerequisite for this project

-  Create a IAM user and add the below policy for that user
-  3 AWS Instances. (See screenshots, I have added policy to match my tags) 

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

## Outcome

As per the above IAM policy, The IAM user can only start, stop and restart instances with tags Env = dev,  Project = zomato. The user will not be able to edit tags also.
See screenshots below.

# Unable to perform start, stop and restart.

![image1](https://user-images.githubusercontent.com/98936958/157377217-8325a77e-4014-4663-baf9-6c4b443e928e.PNG)

# Able to start, stop and restart Instance with matching tags

![image2](https://user-images.githubusercontent.com/98936958/157377224-5016070e-26a2-4a60-a602-df7917584430.PNG)
