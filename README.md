# tap-onedrive-personal
Singer.io tap for accessing Files from OneDrive Personal, based on the SingerSDK

## Getting Started

### Installation

Clone the repo, then navigate to it in a terminal and run pipx intall .

### Configuration

#### Application ID

This tap require that you register an app with Graph API in order to obtain an Application ID that will be used by the tap configuration.
Follow the instructions below to register an app using the Azure App registrations page.

> The follwing guides were referenced when creating the below steps, please consult them if you run into any issues
> * [Registering your app for Microsoft Graph](https://docs.microsoft.com/en-us/onedrive/developer/rest-api/getting-started/app-registration?view=odsp-graph-online)
> * [Python Web App demo using Microsoft Intelligent Security Graph - Configuration](https://github.com/microsoftgraph/python-security-rest-sample#configuration)

1. Go to the [Azure App registrations page](https://aka.ms/AppRegistrations/).
1. When prompted, sign in with your account credentials
1. Below the Heading **App registrations**, click **+ New registration**
1. Enter the following information
    1. **Name**: `tap-onedrive-personal`
    1. **Supported account types**:	Personal Microsoft accounts only
    1. **Redirect URI (optional)**
        1. **Select a platform**: `Public client/native (mobile & desktop)`
        1. **URL**: `http://localhost:5000/login/authorized`
1. Click **Register**

On the Next page, make note of the value next to **Application (client) ID**

#### Client Secret

Next we will create a Client Secret that will be used by the tap configuration.

1. Navigate to the App registration page for your application
    1. This is the page where you copied the Applcation ID. If you are no longer on the page from the last section, go to the [App registrations list](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click the app created previously
1. On the left nav, click **Certificates & secrets**
1. Make sure you are on the **Client Secrets** section, then click **+ New client secret**
1. In the right side popup, enter the following values:
    1. **Description**: `tap-onedrive-personal`
    1. **Expires**: 6 months
1. Click Add

In the new row below **+ New client secret**,  make note of the value in the **Value** column, this is Client Secret

> This value will not be shown again once you leave this page, so make sure to record it somewhere safe.  Treat this value like a password.
> If you lose the Client Secret, delete the existing one and create a new one

TODO:
