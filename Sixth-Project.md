# [Build a Full-Stack React Application using AWS Amplify]

## Task 1: Deploy and Host a React App

### Step 1 - Create a new React Application

1. In a new terminal window, run the following command to use Vite to create a React application:

npm create vite@latest notesapp -- --template react
cd notesapp
npm install
npm run dev

2. In the terminal window, select and open the Local link to view the Vite + React application.

### Step 2 - Initialize GitHub repository

In this step, you will create a GitHub repository and commit your code to the repository. You will need a GitHub account to complete this step, if you do not have an account, sign up here.

Note: If you have never used GitHub on your computer, follow the steps to generate and add an SSH key to your account before continuing to allow connection to your account.

1. Sign in to GitHub at https://github.com/.


2. In the Start a new repository section, make the following selections:

For Repository name, enter notesapp, and choose the Public radio button.
Then select, Create a new repository.

3. Open a new terminal window, navigate to your app's root folder (notesapp), and run the following commands to initialize a git and push the application to the new GitHub repo: 

Note: Replace the SSH GitHub URL in the command with your SSH GitHub URL.

git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:<your-username>/notesapp.git 
git branch -M main

git push -u origin main

### Step 3 - Install the Amplify packages

1. Open a new terminal window, navigate to your app's root folder (notesapp), and run the following command:

npm create amplify@latest -y

2. Running the previous command will scaffold a lightweight Amplify project in the app’s directory.

3. In your open terminal window, run the following commands to push the changes to GitHub:

git add .
git commit -m 'installing amplify'
git push origin main

### Step 4 - Deploy your app with AWS Amplify
In this step, you will connect the GitHub repository you just created to AWS Amplify. This will enable you to build, deploy, and host your app on AWS.

1. Sign in to the AWS Management console in a new browser window, and open the AWS Amplify console at https://console.aws.amazon.com/amplify/apps.

2. Choose Create new app.

3. On the Start building with Amplify page, for Deploy your app, select GitHub, and select Next.

4. When prompted, authenticate with GitHub. You will be automatically redirected back to the Amplify console. Choose the repository and main branch you created earlier. Then, select Next.

5. Leave the default build settings and select Next.

6. Review the inputs selected, and choose Save and deploy.

AWS Amplify will now build your source code and deploy your app at https://...amplifyapp.com, and on every git push your deployment instance will update. It may take up to 5 minutes to deploy your app.

7. Once the build completes, select the Visit deployed URL button to see your web app up and running live.

### Step 5 - Automatically deploy code changes
In this step, you will make some changes to the code using your text editor and push the changes to the main branch of your app.

1. On your local machine, navigate to the notesapp/src/App.jsx file, and update it with the following code. Then, save the file.

import reactLogo from "./assets/react.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={reactLogo} className="logo react" alt="React logo" />

        <h1>Hello from Amplify</h1>
      </header>
    </div>
  );
}

export default App;

2. In your terminal window, run the following command to push the changes to GitHub:
git add .
git commit -m 'changes for amplify'
git push origin main

3. AWS Amplify will now build your source code and deploy your app.  

4. Navigate back to the Amplify console, and select the Visit deployed URL button to view your updated app.


## Task 2: Initialize a Local Amplify App



