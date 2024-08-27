*[Visualizing Netflix Data using Amazon Quicksight]*
====================================================

Step 1: Downloading the Dataset of Netflix
- I have a huge data of csv file and a json document
- CSV File name: netflix_titles.csv and manifest.json

Step 2: Store the Dataset in Amazon S3
- In your S3 console, create a new bucket with a unique Name and rest all option keep as default
- Upload the Dataset which we downloaded in step 2
- Now open the json file and edit the URI and paste your S3 URI url
  ![Screenshot from 2024-08-26 10-05-25](https://github.com/user-attachments/assets/d9cdab10-7f1b-4e3e-b867-08a082fddf98)

- Now we have 2 files in the Bucket csv file and a json file
![Screenshot from 2024-08-26 10-03-48](https://github.com/user-attachments/assets/2426f691-3409-414b-8afa-6b99434c9604)

Step 3: Create your Amazon QuickSight account
- Search for Amazon QuickSight and then create Account
- Give a unique Name and select S3 option and uncheck the AddOns

Step 4: Connect your S3 bucket to Amazon QuickSight
- Open the QuickSight and click the S3 Bucket
- Also upload the json file url from the s3
- Click on Create and then click on Visualise

![Screenshot from 2024-08-26 10-50-49](https://github.com/user-attachments/assets/c957e034-a2e5-4390-ac7a-0ef246fab2a1)

![Screenshot from 2024-08-26 10-52-41](https://github.com/user-attachments/assets/e8d54e70-aca5-406d-b47d-e9dce845a65c)

Step 5: Create Your First QuickSight Visualisation
- As per your convenience input the data as per fields
- Use data and Visuals correspondingly 

![Screenshot from 2024-08-26 10-59-17](https://github.com/user-attachments/assets/9efe52a3-d1b3-413f-8a4c-7a4650818a21)

`You can do more of Visualization and play around it`

!!! NOW DELETE YOUR RESOURCES WHAT ALL YOU HAVE CREATED
Click on your Quicksight profile and then click on Manage Account 
![Screenshot from 2024-08-26 11-07-21](https://github.com/user-attachments/assets/bb9ace33-2f73-45a5-897a-e91f50c45921)
Click on Account Settings --> Account Termination
![Screenshot from 2024-08-26 11-08-45](https://github.com/user-attachments/assets/a14aa8d5-3cde-4924-94d6-50b4a609f0c3)

Now need to delete the S3 Bucket
Empty the Bucket and then delete the Bucket !!!!
