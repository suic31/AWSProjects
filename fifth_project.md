# [Cloud Security with AWS IAM] #

## Step 1: Launch an EC2 Instance
![Screenshot from 2024-08-29 19-55-32](https://github.com/user-attachments/assets/64aed1e5-ff59-4b23-8233-6f7768d00e80)

Give a name and Enter the default settings i.e Select AMI as Amazon Linux and keep instance type default and rest all the default and click on Launch Instance
![Screenshot from 2024-08-29 19-55-32](https://github.com/user-attachments/assets/aada076c-f725-4696-ac97-26908c8da3b9)

![Screenshot from 2024-08-29 19-59-47](https://github.com/user-attachments/assets/42791104-77ac-4346-b652-7672128202be)


## Step 2: Launch another EC2 Instance the same way as you launched in Step 1 and give a unique name in my case i kept the first 1 as production and 2nd one as development

## Step 3: Need to search for IAM and click on Policy from left side and need to paste the below code

{    
  "Version": "2012-10-17",    
  "Statement": [        
    {            
      "Effect": "Allow",            
      "Action": "ec2:*",            
      "Resource": "*",            
      "Condition": {                
        "StringEquals": {                    
          "ec2:ResourceTag/Env": "development"                
        }            
      }        
    },        
    {            
      "Effect": "Allow",            
      "Action": "ec2:Describe*",            
      "Resource": "*"        
    },        
    {            
      "Effect": "Deny",            
      "Action": [                
        "ec2:DeleteTags",                
        "ec2:CreateTags"            
      ],            
      "Resource": "*"        
    }    
  ] 
}

(To Learn policy kindly go to AWS Policy Documentation and Learn)
![Screenshot from 2024-08-29 20-37-13](https://github.com/user-attachments/assets/6be43216-bfbd-4b94-b821-71d470b66878)


## Step 4: 

Click on Next and enter a policyName
![Screenshot from 2024-08-29 20-42-03](https://github.com/user-attachments/assets/981f66f4-6f81-4088-8940-130568a6596b)

Also create a Account Alias under the AWS Account details kindly see the below details
![Screenshot from 2024-08-29 20-52-07](https://github.com/user-attachments/assets/a630994e-b1ff-4cc6-bbaa-d4a23e013180)

## Step 5: Need to create a IAM User Group
Under IAM there is a option as User groups click on it and Create a User Group, provide a name and attach the policy which we created early and click on create
![Screenshot from 2024-08-29 21-09-17](https://github.com/user-attachments/assets/8af759a5-98bb-45cf-9652-90dff7c64c3c)

Now need to add user to User Group [Best is to create a new user and add it to the group]
![Screenshot from 2024-08-29 21-10-04](https://github.com/user-attachments/assets/aed681b0-dc97-4898-a6c0-81c9131bef1f)

## Step 5: Now login with the user you had added previously [Or else add the new user] [ALSO DO THIS IN INGONITO MODE ELSE YOUR CURRENT SESSION WILL BE LOGGED OUT]
![Screenshot from 2024-08-29 21-17-40](https://github.com/user-attachments/assets/3fddace1-9798-48ce-8805-124dd6ea52c0)

After logging in you should be able to access the EC2 options and should be able to see the running instances
![Screenshot from 2024-08-29 21-24-16](https://github.com/user-attachments/assets/80d8450b-be0b-4a27-b005-974ee1a16daa)

Try to stop the Production Instance you will get a message saying you cannot do that as there is no access to do that
![Screenshot from 2024-08-29 21-21-12](https://github.com/user-attachments/assets/a237a914-ccca-4270-bc07-40472512c47b)

# *[Now Try to Stop the Development Instances you should be able to as we have given all access to development related tags in policies]*

