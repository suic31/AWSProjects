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

### Step 1: Setup Amplify Auth
The app uses email as the default login mechanism. When the users sign up, they receive a verification email.

1. By default, your auth resource is configured as shown inside the notesapp/amplify/auth/resource.ts file. For this tutorial, keep the default auth set up as is.

### Step 2: Setup Amplify Data
The app you will be building is a Notes app that will allow users to create, delete, and list notes. This example app will help you learn how to build many popular types of CRUD+L (create, read, update, delete, and list) applications.

1. On your local machine, navigate to the notesapp/amplify/data/resource.ts file and update it with the following code. Then, save the file.

The following updated code uses a per-owner authorization rule allow.owner() to restrict the note record’s access to the owner of the record. 
Amplify will automatically add an owner: a.string() field to each note which contains the note owner's identity information upon record creation.

import { type ClientSchema, a, defineData } from '@aws-amplify/backend';

const schema = a.schema({
  Note: a
    .model({
      name:a.string(),
      description: a.string(),
      image: a.string(),
    })
    .authorization((allow) => [allow.owner()]),
});

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: 'userPool',
  },
});

### Step 3: Set up Amplify Storage

1. On your local machine, navigate to the notesapp/amplify folder, and create a new folder named storage, and then create a file named resource.ts inside of the new storage folder.

2. Update the amplify/storage/resource.ts file with the following code to configure a storage resource for your app. Then, save the file.

The updated code will set up the access so that only the person who uploads the image can access. The code will use the entity_id as a reserved token that will be replaced with the users' identifier when the file is being uploaded. 
import { defineStorage } from "@aws-amplify/backend";

export const storage = defineStorage({
  name: "amplifyNotesDrive",
  access: (allow) => ({
    "media/{entity_id}/*": [
      allow.entity("identity").to(["read", "write", "delete"]),
    ],
  }),
});

### Step 4: Deploy Amplify Cloud Sandbox

1. On your local machine, navigate to the amplify/backend.ts file, and update it with the following code. Then, save the file.

The following code will import the auth, data, and storage backend definitions:
import { defineBackend } from '@aws-amplify/backend';
import { auth } from './auth/resource';
import { data } from './data/resource';
import { storage } from './storage/resource';

/**
 * @see https://docs.amplify.aws/react/build-a-backend/ to add storage, functions, and more
 */
defineBackend({
  auth,
  data,
  storage
}); 

2. To start your own personal cloud sandbox environment that provides an isolated development space, in a new terminal window, run the following command in your apps root folder:

npx ampx sandbox

3. Once the cloud sandbox has been fully deployed, your terminal will display a confirmation message and the amplify_outputs.json file will be generated and added to your project.


## Task 3: Build the Frontend

Step 1 - You will need two Amplify libraries for your project. The main aws-amplify library contains all of the client-side APIs for connecting your app's frontend to your backend and the @aws-amplify/ui-react library contains framework-specific UI components.

1. Open a new terminal window, navigate to you projects folder (notesapp), and run the following command to install these libraries in the root of the project.

npm install aws-amplify @aws-amplify/ui-react 

Step 2 - Style the App UI

1. On your local machine, navigate to the notesapp/src/index.css file, and update it with the following code to set the style of the Notes UI. Then, save the file.

:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color: rgba(255, 255, 255, 0.87);

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

}

.card {
  padding: 2em;
}

.read-the-docs {
  color: #888;
}

.box:nth-child(3n + 1) {
  grid-column: 1;
}
.box:nth-child(3n + 2) {
  grid-column: 2;
}
.box:nth-child(3n + 3) {
  grid-column: 3;
}

Step 3: Implement the UI Flow for Notes Feature
In this step, you will update the src/App.jsx to configure the Amplify library with the client configuration file (amplify_outputs.json). Then, it will generate a data client using the generateClient() function.

The code uses the Amplify Authenticator component to scaffold out an entire user authentication flow allowing users to sign up, sign in, reset their password, and confirm sign-in for multifactor authentication (MFA).

Additionally, the code contains the following:
 fetchNotes - Use the data client to list the items in the Notes model.
createNote - Get the data from the form and use the data client to create a new note if the user selects an image. Then, the function will upload this image to Amplify storage and associate it with the new note.
deleteNote - Use the data client to delete the selected note.
1. On your local machine, navigate to the notesapp/src/App.jsx file, and update it with the following code.

import { useState, useEffect } from "react";
import {
  Authenticator,
  Button,
  Text,
  TextField,
  Heading,
  Flex,
  View,
  Image,
  Grid,
  Divider,
} from "@aws-amplify/ui-react";
import { Amplify } from "aws-amplify";
import "@aws-amplify/ui-react/styles.css";
import { getUrl } from "aws-amplify/storage";
import { uploadData } from "aws-amplify/storage";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";
/**
 * @type {import('aws-amplify/data').Client<import('../amplify/data/resource').Schema>}
 */

Amplify.configure(outputs);
const client = generateClient({
  authMode: "userPool",
});

export default function App() {
  const [notes, setNotes] = useState([]);

  useEffect(() => {
    fetchNotes();
  }, []);

  async function fetchNotes() {
    const { data: notes } = await client.models.Note.list();
    await Promise.all(
      notes.map(async (note) => {
        if (note.image) {
          const linkToStorageFile = await getUrl({
            path: ({ identityId }) => `media/${identityId}/${note.image}`,
          });
          console.log(linkToStorageFile.url);
          note.image = linkToStorageFile.url;
        }
        return note;
      })
    );
    console.log(notes);
    setNotes(notes);
  }

  async function createNote(event) {
    event.preventDefault();
    const form = new FormData(event.target);
    console.log(form.get("image").name);

    const { data: newNote } = await client.models.Note.create({
      name: form.get("name"),
      description: form.get("description"),
      image: form.get("image").name,
    });

    console.log(newNote);
    if (newNote.image)
      if (newNote.image)
        await uploadData({
          path: ({ identityId }) => `media/${identityId}/${newNote.image}`,

          data: form.get("image"),
        }).result;

    fetchNotes();
    event.target.reset();
  }

  async function deleteNote({ id }) {
    const toBeDeletedNote = {
      id: id,
    };

    const { data: deletedNote } = await client.models.Note.delete(
      toBeDeletedNote
    );
    console.log(deletedNote);

    fetchNotes();
  }

  return (
    <Authenticator>
      {({ signOut }) => (
        <Flex
          className="App"
          justifyContent="center"
          alignItems="center"
          direction="column"
          width="70%"
          margin="0 auto"
        >
          <Heading level={1}>My Notes App</Heading>
          <View as="form" margin="3rem 0" onSubmit={createNote}>
            <Flex
              direction="column"
              justifyContent="center"
              gap="2rem"
              padding="2rem"
            >
              <TextField
                name="name"
                placeholder="Note Name"
                label="Note Name"
                labelHidden
                variation="quiet"
                required
              />
              <TextField
                name="description"
                placeholder="Note Description"
                label="Note Description"
                labelHidden
                variation="quiet"
                required
              />
              <View
                name="image"
                as="input"
                type="file"
                alignSelf={"end"}
                accept="image/png, image/jpeg"
              />

              <Button type="submit" variation="primary">
                Create Note
              </Button>
            </Flex>
          </View>
          <Divider />
          <Heading level={2}>Current Notes</Heading>
          <Grid
            margin="3rem 0"
            autoFlow="column"
            justifyContent="center"
            gap="2rem"
            alignContent="center"
          >
            {notes.map((note) => (
              <Flex
                key={note.id || note.name}
                direction="column"
                justifyContent="center"
                alignItems="center"
                gap="2rem"
                border="1px solid #ccc"
                padding="2rem"
                borderRadius="5%"
                className="box"
              >
                <View>
                  <Heading level="3">{note.name}</Heading>
                </View>
                <Text fontStyle="italic">{note.description}</Text>
                {note.image && (
                  <Image
                    src={note.image}
                    alt={`visual aid for ${notes.name}`}
                    style={{ width: 400 }}
                  />
                )}
                <Button
                  variation="destructive"
                  onClick={() => deleteNote(note)}
                >
                  Delete note
                </Button>
              </Flex>
            ))}
          </Grid>
          <Button onClick={signOut}>Sign Out</Button>
        </Flex>
      )}
    </Authenticator>
  );
}

2. Open a new terminal window, navigate to your app's root folder (notesapp), and run the following command to launch the app:

npm run dev

3. Select the Local host link to open the application.

4. Choose the Create Account tab, and use the authentication flow to create a new user by entering your email address and a password. Then, choose Create Account.

5. You will get a verification code sent to your email. Enter the verification code to log in to the app. When signed in, you can start creating notes and delete them.

6. Open a new terminal window, navigate to your app's root folder (notesapp), and run the following command to push the changes to GitHub: 

git add .
git commit -m 'the notes app'
git push origin main

7. Sign in to the AWS Management console in a new browser window, and open the AWS Amplify console at https://console.aws.amazon.com/amplify/apps.

8. AWS Amplify automatically builds your source code and deployed your app at https://...amplifyapp.com, and on every git push your deployment instance will update. Select the Visit deployed URL button to see your web app up and running live.


## Clean up the resources

In the Amplify console, in the left-hand navigation for the notesapp app, choose App settings, and select General settings.

In the General settings section, choose Delete app.

Kindly find the below sample screenshots of the project:
![Screenshot from 2024-09-04 15-33-21](https://github.com/user-attachments/assets/03cbb252-0ebd-4f32-bdf7-57b942d3947a)

![Screenshot from 2024-09-04 15-33-38](https://github.com/user-attachments/assets/f4111e3b-c394-4ee3-a046-dd3acea570a6)

![Screenshot from 2024-09-04 15-33-45](https://github.com/user-attachments/assets/e2b42411-8e03-4556-a8e8-0d0481ee6b55)

![Screenshot from 2024-09-04 15-33-56](https://github.com/user-attachments/assets/345d3b2b-780a-48c3-866b-620bb3fe8fc5)

![Screenshot from 2024-09-04 15-34-33](https://github.com/user-attachments/assets/95debbc6-afe3-484f-8cf5-0778b02de929)

![Screenshot from 2024-09-04 15-34-40](https://github.com/user-attachments/assets/c0caa048-14d1-415a-8ff8-37aacce18177)

![Screenshot from 2024-09-04 15-34-50](https://github.com/user-attachments/assets/5bfd78a7-a3de-4024-84d3-b9c07a845953)

![Screenshot from 2024-09-04 15-35-43](https://github.com/user-attachments/assets/dc57b3a6-d3e8-449e-a71d-72aed2729cca)

![Screenshot from 2024-09-04 15-50-28](https://github.com/user-attachments/assets/d9e931a4-7916-45fe-89d4-b5088abb99a3)

![Screenshot from 2024-09-04 15-52-42](https://github.com/user-attachments/assets/0ba415c2-b7f5-43bd-8749-e6a92cca0a13)

![Screenshot from 2024-09-04 15-52-51](https://github.com/user-attachments/assets/3bea17c2-cd4c-4c34-bcda-0574a39b681d)

![Screenshot from 2024-09-04 16-16-01](https://github.com/user-attachments/assets/9885f648-2bc8-458d-adf3-7db1eaa7ef38)
