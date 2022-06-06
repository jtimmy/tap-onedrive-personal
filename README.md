# tap-onedrive-personal
Singer.io tap for accessing Files from OneDrive Personal, based on the SingerSDK

## Getting Started

### Installation

Clone the repo, then navigate to it in a terminal and run pipx intall .

### Configuration


This tap require that you register an app with Graph API in order to obtain an Application ID and Client Secret that will be used by the tap configuration.

#### Application ID

Follow the instructions below to register an app using the Azure App registrations page.

> The follwing guides were referenced when creating the below steps, please consult them if you run into any issues
>
> * [Registering your app for Microsoft Graph](https://docs.microsoft.com/en-us/onedrive/developer/rest-api/getting-started/app-registration?view=odsp-graph-online)
> * [Python Web App demo using Microsoft Intelligent Security Graph - Configuration](https://github.com/microsoftgraph/python-security-rest-sample#configuration)
> * [Quickstart: Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app#register-a-new-application-using-the-azure-portal)
> * [How to authenticate to personal OneDrive with Graph REST API](https://stackoverflow.com/questions/65283220/how-to-authenticate-to-personal-onedrive-with-graph-rest-api)
> * [Microsoft identity platform and OAuth 2.0 authorization code flow](https://docs.microsoft.com/en-au/azure/active-directory/develop/v2-oauth2-auth-code-flow)
> * [Authorization and sign-in for OneDrive in Microsoft Graph](https://docs.microsoft.com/en-us/onedrive/developer/rest-api/getting-started/graph-oauth?view=odsp-graph-online)

1. Go to the [Azure App registrations page](https://aka.ms/AppRegistrations/).
1. When prompted, sign in with your account credentials
1. Below the Heading **App registrations**, click **+ New registration**
1. Enter the following information
    1. **Name**: `tap-onedrive-personal`
    1. **Supported account types**:	Personal Microsoft accounts only
    1. **Redirect URI (optional)**: (leave blank)
1. Click **Register**

On the Next page, make note of the value next to **Application (client) ID**

#### Redirect URI

Next we will create a Client Secret that will be used to authorize the application.

1. Navigate to the App registration page for your application
    1. This is the page where you copied the Applcation ID. If you are no longer on the page from the last section, go to the [App registrations list](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click the app created previously
1. On the left nav, click **Authentication**
1. Under the **Platform configurations** header, click **+ Add a platform**
1. In the popup, click **Mobile and desktop applications**
1. Check the box next to `https://login.microsoftonline.com/common/oauth2/nativeclient`
1. Click **Configure** at the bottom

On the Next page, make note of the value of the checked **Redirect URI**

#### Client Secret

Next we will create a Client Secret that will be used by the tap configuration.

1. Navigate to the App registration page for your application
    1. This is the page where you copied the Applcation ID. If you are no longer on the page from the last section, go to the [App registrations list](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click the app created previously
1. On the left nav, click **Certificates & secrets**
1. Make sure you are in the **Client Secrets** section, then click **+ New client secret**
1. In the right side popup, enter the following values:
    1. **Description**: `tap-onedrive-personal`
    1. **Expires**: 6 months
1. Click Add

In the new row below **+ New client secret**,  make note of the value in the **Value** column, this is Client Secret

> This value will not be shown again once you leave this page, so make sure to record it somewhere safe.  Treat this value like a password.
> If you lose the Client Secret, delete the existing one and create a new one

#### Application Scope

Next we will assign the scopes neede by the application for the tap to be able to perform the work.

1. Navigate to the App registration page for your application
    1. This is the page where you copied the Applcation ID. If you are no longer on the page from the last section, go to the [App registrations list](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click the app created previously
1. On the left nav, click **API permissions**
1. Under the **Configured permissions** header, click **+ Add a permission**
1. In the popup, click **Microsoft Graph** at the top
1. In the next screen , click **Delegated Permissions** at the top
1. Scroll down until you find the **Files** group and click the `>` to expand it
1. Check the box next to the **Files.Read.All** permission
1. Click **Add permission** at the bottom of the page

#### Get Autorization Code

In a web browser, go to the following URL, replacing the values below as follows

https://login.microsoftonline.com/consumers/oauth2/v2.0/authorize?client_id={client_id}&scope={scope}&response_type=code&redirect_uri={redirect_uri}

* **{client_id}** should be replaced with the Application ID noted above
* **{scope}** should be replaced with the Scope added to the application above 
TODO, update this to reference graph.api stuff
* **{redirect_uri}** should be replaced with the URL used when creating the application above

#### Get Refresh Token

In Postman, 

https://login.microsoftonline.com/consumers/oauth2/v2.0/token

Body

* 