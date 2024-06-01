#AWS #AWSAmplify #AmplifyGen2 #FullStack #WebDevelopment 

Cloned from [NextJS React Amplify Template](https://github.com/new?template_name=amplify-next-template&template_owner=aws-samples&name=amplify-next-template&description=My%20Amplify%20Gen%202%20starter%20application)

#### Project Structure
├── amplify/ # Folder containing your Amplify backend configuration
│ ├── auth/ # Definition for your auth backend
│ │ └── resource.tsx
│ ├── data/ # Definition for your data backend
│ │ └── resource.ts
| ├── backend.ts
│ └── tsconfig.json
├── src/ # React UI code
│ ├── App.tsx # UI code to sync todos in real-time
│ ├── index.css # Styling for your app
│ └── main.tsx # Entrypoint of the Amplify client library
├── package.json
└── tsconfig.json

*amplify_outputs.json* contains backend endpoint information, publicly-viewable API keys, auth flow information, etc. Amplify uses this to connect to Amplify Backend. 

##### resource.ts
They define the model generated for its respective folder. 