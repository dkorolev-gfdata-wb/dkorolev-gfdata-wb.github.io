
# WB-Dashboards

The project consists of "Projects", "Resource" and "Team" dashboards that allow to manipulate a large amount of data related to projects within the organization (information about projects, tasks, milestones, phases, terms, etc.).

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project.

### Getting a local version of the project

TFS path:

```
$/WBEngineering/wb-dashboards
```

### Installing all project dependencies

```
npm install
```

### Running locally

Runs the app locally in development mode (http://localhost:3000 ).

```
npm start
```

### Building

Builds the app for production to the build folder.

```
npm run build
```

## Deployment to GitHub Pages (https://dkorolev-gfdata-wb.github.io)

Project is already configured to deploying to GitHub Pages (https://dkorolev-gfdata-wb.github.io). So, everything you need to do to deploy app is:

1. Set origin url

```
git remote set-url origin https://dkorolev-gfdata-wb:<Password>@github.com/dkorolev-gfdata-wb/dkorolev-gfdata-wb.github.io.git/
```

2. Run the following command

```
npm run deploy
```

That's it. If all goes well, you will see "Published" in your console.

## Deployment somewhere else

In view of the fact that project requires Azure AD authentication, before deploying project somewhere we need to configure Azure AD App for the new instance of the application. We have to perform the following steps for this:

1. Go to the Microsoft Azure Portal -> Azure Active Directory -> App registrations.
2. Click "New application registration".
3. Enter the name of the application, select Application Type "Native" and enter the redirect url of the application (url, where you want to host the application).
4. When Azure AD App is created we need to go to its manifest and set the property "oauth2AllowImplicitFlow" to true.
5. Now we need to grant our application the necessary permissions to access the Sharepoint Online. Go to the App Settings -> Required permissions -> Add -> Select API -> Office 365 SharePoint Online. 
6. In the "APPLICATION PERMISSIONS" section select the following items: 
    - "Read and write items and lists in all site collections"
    - "Read and write items in all site collections"
    - "Read items in all site collections"
7. Save changes.
8. Copy "Application ID", go to the project, open adalConfig.ts (src -> adal -> adalConfig.ts) file and update "prodAppId" variable.
9. Rebuid project: 
```
npm run build
```

That's it. If all goes well, after completing this operation you can find fresh version of the app in the build folder.