# Create a Continuous Delivery Pipeline

### Pre-Requisites:
[AWS account with administrator-level access
GitHub account
Git installed on your computer
Recommended browser: The latest version of Chrome or Firefox]

## Module 1: Set Up Git Repo
Open your Github Account and also in similar tab open the link [https://github.com/suic31/aws-elastic-beanstalk-express-js-sample] --> Fork it --> Open the Forked Repo and then Clone it into your system
![Screenshot from 2024-09-13 21-10-58](https://github.com/user-attachments/assets/74647c5d-5fb9-47a3-a870-3b53c2bc7a38)

Later open the folder which you have cloned --> Open the app.js and change Hello World and enter Something according to you  
![Screenshot from 2024-09-13 21-15-25](https://github.com/user-attachments/assets/c5da08d5-fea0-4459-afb4-ae2f22501de3)

Enter the below command in your terminal
git add app.js
git commit -m "change message"

Need to push the changes done
git push
![Screenshot from 2024-09-13 21-20-28](https://github.com/user-attachments/assets/ba457e01-af12-49b7-bf47-260f228ebe26)

Confirm the changes done in your account by going into the cloned repo in Github and under app.js you should see the content you have pasted
![Screenshot from 2024-09-13 21-21-24](https://github.com/user-attachments/assets/a1e3e11a-7889-4036-b2e2-75952048beea)

## Module 2: Deploy Web App

### Configure an AWS Elastic Beanstalk app

In a new browser tab, open the AWS Elastic Beanstalk console.
Choose the orange Create Application button.
Choose Web server environment under the Configure environment heading.
In the text box under the heading Application name, enter DevOpsGettingStarted.
In the Platform dropdown menu, under the Platform heading, select Node.js . Platform branch and Platform version will automatically populate with default selections.
Confirm that the radio button next to Sample application under the Application code heading is selected.
Confirm that the radio button next to Single instance (free tier eligible) under the Presets heading is selected.
Select Next.



###   Test your Web App

1. To test your sample web app, select the link under the name of your environment.
![Screenshot from 2024-09-13 23-29-06](https://github.com/user-attachments/assets/bdfebf50-6f54-4913-99b9-6b33ed4529f3)

2. Once the test has completed, a new browser tab should open with a webpage congratulating you!
![Screenshot from 2024-09-13 23-29-29](https://github.com/user-attachments/assets/56743ec7-51c6-41a7-b0d5-5be92a2a50f1)

# Module 3: Create Build Project

### Configure the AWS CodeBuild Project

In a new browser tab, open the AWS CodeBuild console.
Choose the orange Create project button.
In the Project name field, enter Build-DevOpsGettingStarted.
Select GitHub from the Source provider dropdown menu.
Confirm that the Connect using OAuth radio button is selected.
Choose the white Connect to GitHub button. A new browser tab will open asking you to give AWS CodeBuild access to your GitHub repo.
Choose the green Authorize aws-codesuite button.
Enter your GitHub password.
Choose the orange Confirm button.
Select Repository in my GitHub account.
Enter aws-elastic-beanstalk-express-js-sample in the search field.
Select the repo you forked in Module 1. After selecting your repo, your screen should look like this
