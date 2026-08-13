# Introduction

The Google Apps Script API lets you automate script creation, management, and
execution in Google Apps Script. You can programmatically create, modify, and
deploy Google Apps Script projects, and execute Apps Script
functions remotely---actions that otherwise require using the
Apps Script editor or its UI.

This API is often used to:

- Create and manage Apps Script projects and deployments.
- Add or update functions in script projects.
- Execute Apps Script functions from other applications.
- Monitor script execution logs and statuses.

> [!WARNING]
> **Warning:** The Apps Script API doesn't work with [service accounts](https://developers.google.com/identity/protocols/OAuth2ServiceAccount).

The Apps Script API also replaces and extends the
Apps Script Execution API. You can use the
Apps Script API to execute Apps Script functions
remotely, just as you could with the Execution API.

To use this API in your apps, you must
[enable it for use](https://developers.google.com/apps-script/api/how-tos/enable#use_the_apps_script_api_in_your_app).

To allow other apps to manage your scripts, you must
[grant them access](https://developers.google.com/apps-script/api/how-tos/enable#grant_third-party_applications_access_to_your_script_projects).

## Overview of the API

The Apps Script API is divided into several resources, each with a
specific purpose and set of requests you can make. These resources are as
follows:

- [`projects`](https://developers.google.com/apps-script/api/reference/rest/v1/projects) --- A representation of a script project. The API provides methods to create, read, monitor, and modify projects. Use this resource to manage the script files and metadata of your project.
- [`projects.deployments`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments) --- A representation of a script deployment. The API provides methods to create, list, update, and delete script project deployments. Use deployments to make your script available as a web app, add-on, or executable.
- [`projects.versions`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions) --- A representation of a script project version. The API provides methods to create and read project versions. Use versions to track different iterations of your script project.
- [`processes`](https://developers.google.com/apps-script/api/reference/rest/v1/processes) --- A representation of a script function execution. The API provides methods to list existing processes and gather information about them, such as type and current status. Use this resource to monitor script executions initiated using the `scripts.run` method.
- [`scripts`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts) --- The endpoint that provides methods to remotely execute Apps Script functions. Use this resource to run functions in your script project from your application.


# Python quickstart

Create a Python command-line application that makes requests to the
Google Apps Script API.

Quickstarts explain how to set up and run an app that calls a
Google Workspace API. This quickstart uses a
simplified authentication approach that is appropriate for a testing
environment. For a production environment, we recommend learning about
[authentication and authorization](https://developers.google.com/workspace/guides/auth-overview)
before
[choosing the access credentials](https://developers.google.com/workspace/guides/create-credentials#choose_the_access_credential_that_is_right_for_you)
that are appropriate for your app.

This quickstart uses Google Workspace's recommended API client libraries
to handle some details of the authentication and authorization flow.

## Objectives

- Set up your environment.
- Install the client library.
- Set up the sample.
- Run the sample.

## Prerequisites

To run this quickstart, you need the following prerequisites:

- Python 3.10.7 or greater
- The [pip](https://pypi.python.org/pypi/pip) package management tool
- [A Google Cloud project](https://developers.google.com/workspace/guides/create-project).


- A Google account with Google Drive enabled.

<br />

## Set up your environment

To complete this quickstart, set up your environment.

### Enable the API

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

- In the Google Cloud console, enable the Google Apps Script API.

  [Enable the API](https://console.cloud.google.com/apis/enableflow?apiid=script.googleapis.com)

### Configure the OAuth consent screen

If you're using a new Google Cloud project to complete this quickstart, configure
the OAuth consent screen. If you've already
completed this step for your Cloud project, skip to the next section.

1. In the Google API Console, go to Menu \> **Google Auth platform** \> **Branding** .

   [Go to Branding](https://console.developers.google.com/auth/branding)
2. If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in [Branding](https://console.developers.google.com/auth/branding), [Audience](https://console.developers.google.com/auth/audience), and [Data Access](https://console.developers.google.com/auth/scopes). If you see a message that says **Google Auth platform not configured yet** , click **Get Started**:
   1. Under **App Information** , in **App name**, enter a name for the app.
   2. In **User support email**, choose a support email address where users can contact you if they have questions about their consent.
   3. Click **Next**.
   4. Under **Audience** , select **Internal**.
   5. Click **Next**.
   6. Under **Contact Information** , enter an **Email address** where you can be notified about any changes to your project.
   7. Click **Next**.
   8. Under **Finish** , review the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy) and if you agree, select **I agree to the Google API Services: User Data Policy**.
   9. Click **Continue**.
   10. Click **Create**.
3. For now, you can skip adding scopes. In the future, when you create an app for use outside of your Google Workspace organization, you must change the **User type** to **External** . Then add the authorization scopes that your app requires. To learn more, see the full [Configure OAuth consent](https://developers.google.com/workspace/guides/configure-oauth-consent) guide.

### Authorize credentials for a desktop application

To authenticate end users and access user data in your app, you need to create one or more OAuth 2.0 Client IDs. A client ID is used to identify a single app to Google's OAuth servers. If your app runs on multiple platforms, you must create a separate client ID for each platform.

1. In the Google API Console, go to Menu \> **Google Auth platform** \> **Clients** .

   [Go to Clients](https://console.developers.google.com/auth/clients)
2. Click **Create Client**.
3. Click **Application type** \> **Desktop app**.
4. In the **Name** field, type a name for the credential. This name is only shown in the Google API Console.
5. Click **Create** .


   The newly created credential appears under "OAuth 2.0 Client IDs."
6. Save the downloaded JSON file as `credentials.json`, and move the file to your working directory.

## Install the Google client library

- Install the Google client library for Python:

      python3 -m pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib

## Configure the sample

1. In your working directory, create a file named `quickstart.py`.
2. Include the following code in `quickstart.py`:


   apps_script/quickstart/quickstart.py [View on GitHub](https://github.com/googleworkspace/python-samples/blob/main/apps_script/quickstart/quickstart.py)

   ```python
   """
   Shows basic usage of the Apps Script API.
   Call the Apps Script API to create a new script project, upload a file to the
   project, and log the script's URL to the user.
   """
   import os.path

   from google.auth.transport.requests import Request
   from google.oauth2.credentials import Credentials
   from google_auth_oauthlib.flow import InstalledAppFlow
   from googleapiclient import errors
   from googleapiclient.discovery import build

   # If modifying these scopes, delete the file token.json.
   SCOPES = ["https://www.googleapis.com/auth/script.projects"]

   SAMPLE_CODE = """
   function helloWorld() {
     console.log("Hello, world!");
   }
   """.strip()

   SAMPLE_MANIFEST = """
   {
     "timeZone": "America/New_York",
     "exceptionLogging": "CLOUD"
   }
   """.strip()


   def main():
     """Calls the Apps Script API."""
     creds = None
     # The file token.json stores the user's access and refresh tokens, and is
     # created automatically when the authorization flow completes for the first
     # time.
     if os.path.exists("token.json"):
       creds = Credentials.from_authorized_user_file("token.json", SCOPES)
     # If there are no (valid) credentials available, let the user log in.
     if not creds or not creds.valid:
       if creds and creds.expired and creds.refresh_token:
         creds.refresh(Request())
       else:
         flow = InstalledAppFlow.from_client_secrets_file(
             "credentials.json", SCOPES
         )
         creds = flow.run_local_server(port=0)
       # Save the credentials for the next run
       with open("token.json", "w") as token:
         token.write(creds.to_json())

     try:
       service = build("script", "v1", credentials=creds)

       # Call the Apps Script API
       # Create a new project
       request = {"title": "My Script"}
       response = service.projects().create(body=request).execute()

       # Upload two files to the project
       request = {
           "files": [
               {"name": "hello", "type": "SERVER_JS", "source": SAMPLE_CODE},
               {
                   "name": "appsscript",
                   "type": "JSON",
                   "source": SAMPLE_MANIFEST,
               },
           ]
       }
       response = (
           service.projects()
           .updateContent(body=request, scriptId=response["scriptId"])
           .execute()
       )
       print("https://script.google.com/d/" + response["scriptId"] + "/edit")
     except errors.HttpError as error:
       # The API encountered a problem.
       print(error.content)


   if __name__ == "__main__":
     main()
   ```

   <br />

   <br />

## Run the sample

1. In your working directory, build and run the sample:

       python3 quickstart.py

<!-- -->

2. The first time you run the sample, it prompts you to authorize access:
   1. If you're not already signed in to your Google Account, sign in when prompted. If you're signed in to multiple accounts, select one account to use for authorization.
   2. Click **Accept**.


   Your Python application runs and calls the Google Apps Script API.


   Authorization information is stored in the file system, so the next time you run the sample
   code, you aren't prompted for authorization.

## Next steps

- [Try the Google Workspace APIs in the APIs explorer](https://developers.google.com/workspace/explore)

<!-- -->

- [Apps Script API reference documentation](https://developers.google.com/apps-script/api/reference/rest)
- [Google APIs Client for Python documentation](https://developers.google.com/api-client-library/python)
- [Google Apps Script API PyDoc documentation](https://developers.google.com/resources/api-libraries/documentation/script/v1/python/latest/index%2Ehtml)


Processes are any kind of Google Apps Script function execution that
runs on the Apps Script server. Processes can be started through
the Apps Script editor, a script trigger, an
Google Workspace add-on, a web app, or through the
Google Apps Script API itself.

Processes can be listed and examined by means of the
Apps Script API [`processes`](https://developers.google.com/apps-script/api/reference/rest/v1/processes)
endpoint. The API can provide process information such as script ID, start
time, process duration, executing user, status, and other details.


The Google Apps Script API requires different types of authorizations
depending on your goal:

- Use the Apps Script API in your app.
- Allow other applications to manage your script project data or deployments.

To use the Apps Script API in your application, you must enable the
API in the application's
[Google Cloud project](https://cloud.google.com/apis/docs/enable-disable-apis#enable_an_api).
This lets you create OAuth credentials so that users of the application
can authorize it.

To let third-party applications manage the content or deployment of your script
projects, you must grant access to your script projects.

## Use the Apps Script API in your app

To use the Apps Script API inside your app, you must enable the
Apps Script API in your application's Google Cloud project. After
enabling the Apps Script API, you can create OAuth credentials and
download the client ID and secret to include in your application. You can also
monitor the API usage in the [Google Cloud console](https://console.cloud.google.com/).

You can use [the API enablement wizard](https://console.developers.google.com/start/api?id=script)
to create or select a Google Cloud project in the Google Cloud console and
automatically enable the API. Alternatively, you can
[open the console's **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager),
select a project, then search for and add the Apps Script API manually
using the project's **APIs \& services** dashboard. After you've enabled the API,
you can create OAuth credentials, client IDs, and client secrets for your
applications in the **APIs \& services \> Credentials** panel.

The [Apps Script API quickstarts](https://developers.google.com/apps-script/api/quickstart/python#step_1_turn_on_the_api_name)
provide a step-by-step look at the whole process of enabling the API and
setting up authorization for an application.

## Grant third-party applications access to your script projects

The Apps Script API can allow applications to create and modify your
scripts and their [deployments](https://developers.google.com/apps-script/concepts/deployments). This can
lead to a bad situation if you authorize a malicious third-party application
which then proceeds to create more malicious scripts or modify the behavior of
scripts you already have.

To help reduce this risk, the Apps Script API cannot access your script
projects by default. You must explicitly grant the API access before you can use
any application that creates or modifies scripts or deployments. Once you've
granted the API access to your scripts, applications you authorize can use the
API to manage your script projects.

An error results if you attempt to run an affected application without first
granting the API access. This error occurs after you authorize the application.

> [!NOTE]
> **Note:** Applications can use the Apps Script API to [execute Google Apps Script functions](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run). These API requests don't require granting access to your script projects.

You can grant the Apps Script API access to your script projects using
the [Apps Script dashboard](https://developers.google.com/apps-script/guides/dashboard#settings).
You can also use the dashboard to revoke this access at any time. When you grant
the API access, you are doing so for all applications. Individual applications
still need to be authorized, however.

Before you grant access, ensure you understand the risk involved in allowing
applications to modify your scripts. Never authorize any application that you
suspect is malicious.

# Manage projects

This section provides an overview of the Google Apps Script API methods
you can use to create, read, modify, and monitor your Google Apps Script
projects. The [Project Management](https://developers.google.com/apps-script/api/samples/manage) samples page
shows examples of API management requests. The reference documentation for each
method provides implementation details.

| **API method overview** ||
|---|---|
| **Create projects** | [projects.create](https://developers.google.com/apps-script/api/reference/rest/v1/projects/create) **Results** : Create a basic, empty project with no project files and a default [project manifest](https://developers.google.com/apps-script/concepts/manifests). **Options** : You can provide a project title. You can also create a [bound script](https://developers.google.com/apps-script/guides/bound) by providing the Google Drive ID of a Google Docs, Google Sheets, Google Forms, or Google Slides file to act as the script's parent. |
| **Read project metadata** | [projects.get](https://developers.google.com/apps-script/api/reference/rest/v1/projects/get) **Results** : Retrieves a [`Project`](https://developers.google.com/apps-script/api/reference/rest/v1/projects#Project) object, which represents project metadata. This data includes the project title, script ID, creating user, creation time, and other details. |
| **Read project content** | [projects.getContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent) **Results** : Returns an array of [`File`](https://developers.google.com/apps-script/api/reference/rest/v1/File) objects, one for each code and HTML file in the project. The list also includes the [project manifest](https://developers.google.com/apps-script/concepts/manifests) as a JSON file. File objects contain the source content of the file (`File.source`) and other metadata, such as a list of functions in the file (`File.functionSet`). **Options** : You can specify which [version](https://developers.google.com/apps-script/guides/versions) of the content to retrieve with a query parameter. |
| **Update project content** | [projects.updateContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/updateContent) **Results** : Changes the file content in a script project. You provide the new content as an array of [`File`](https://developers.google.com/apps-script/api/reference/rest/v1/File) objects. One of these `File` objects must have JSON type and represent the script project's new [project manifest](https://developers.google.com/apps-script/concepts/manifests). The new content is stored as the HEAD version of the project. It is used when the script executes as a trigger, in the script editor, in Google Workspace add-on preview mode, or as a web app or Apps Script API in development mode. **Note** : To update script project content, first issue a [projects.getContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent) request to retrieve an array of the existing `File`s, make the intended changes to those objects, then use the `File`s as input for a [projects.updateContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/updateContent) request. **Warning:** The new content replaces all existing files in the script project. Files not updated by the request are removed. |
| **Read project metrics** | [projects.getMetrics](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics) **Results** : Read certain metrics about a project. These metrics include the number of users, the total number of executions, the total number of execution errors, and other details. Use a [MetricType](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics#metrictype) to specify the information you are requesting. **Options** : Restrict the results to specific deployments or script functions using a [MetricsFilter](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics#MetricsFilter). You can also define a specific metric interval using a [MetricsIntervalConfig](https://developers.google.com/api/reference/rest/v1/projects/getMetrics#metricsintervalconfig). |


# Manage deployments

This section provides an overview of the Google Apps Script API methods you
can use to create, list, read, modify, and delete a script project's
[deployments](https://developers.google.com/apps-script/concepts/deployments).

| **API method overview** ||
|---|---|
| **Create a deployment** | [projects.deployments.create](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments/create) **Results** : Create a new deployment for a script project. You specify the code [version](https://developers.google.com/apps-script/guides/versions), the [manifest](https://developers.google.com/apps-script/concepts/manifests) file, and deployment description to use. Returns a [`Deployment`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments#resource-deployment) object, containing the deployment configuration details. |
| **List a project's deployments** | [projects.deployments.list](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments/list) **Results** : Returns an array of [`Deployment`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments#resource-deployment) objects, each representing one of the deployments of the script project. |
| **Read a deployment** | [projects.deployments.get](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments/get) **Results** : Returns a [`Deployment`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments#resource-deployment) that represents a specific deployment in a specific script project. |
| **Update a deployment** | [projects.deployments.update](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments/update) **Results** : Changes a deployment's description, code [version](https://developers.google.com/apps-script/guides/versions), or the [manifest](https://developers.google.com/apps-script/concepts/manifests) where the deployment is defined. |
| **Delete a deployment** | [projects.deployments.delete](https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments/delete) **Results**: Removes a deployment. **Warning:** Deleting a deployment causes any Google Workspace add-on, web app, or other application that makes use of that deployment to lose access to the Google Apps Script project. This usually causes them to fail. Don't delete a deployment without first updating any apps that depend on it. |


# Manage versions

This section provides an overview of the Google Apps Script API methods you
can use to create a new project code [version](https://developers.google.com/apps-script/guides/versions),
read version information, or list all existing versions.

> [!NOTE]
> **Note:** These methods return one or more [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) objects which contain version configuration information such as the version number and description. You can read the code attached to a specific version using a [`projects.getContent`](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent) request.

| **API method overview** ||
|---|---|
| **Create a version** | [projects.versions.create](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/create) **Results** : Create a new, immutable version of a script project's code. The project's current saved code is used for the version. This creates a code "snapshot" you can read later or use in a specific [deployment](https://developers.google.com/apps-script/concepts/deployments). Returns a [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) object, containing the version configuration details. |
| **List a project's versions** | [projects.versions.list](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/list) **Results** : Returns an array of [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) objects, each representing one of the versions of the script project. |
| **Read a version** | [projects.versions.get](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/get) **Results** : Returns a [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) that represents a specific version of a script project. |


# View process information

This section provides an overview of the Google Apps Script API methods you
can use to list your script [processes](https://developers.google.com/apps-script/api/concepts/processes).

| **API method overview** ||
|---|---|
| **List your processes** | [processes.list](https://developers.google.com/apps-script/api/reference/rest/v1/processes/list) **Results** : Returns an array of [`Process`](https://developers.google.com/apps-script/api/reference/rest/v1/processes#Process) objects, each containing the metadata for a process you have run. This information includes the process type, status, start time, and duration. **Options** : You can define and provide a [`ListUserProcessFilter`](https://developers.google.com/apps-script/api/reference/rest/v1/processes/list#ListUserProcessesFilter) object to filter the process list. Only processes that match \*\*all\*\* of the filter conditions are returned. |
| **List a project's processes** | [processes.listScriptProcesses](https://developers.google.com/apps-script/api/reference/rest/v1/processes/listScriptProcesses) **Results** : Returns an array of [`Process`](https://developers.google.com/apps-script/api/reference/rest/v1/processes#Process) objects, each containing the metadata for a process run from a specifed script project. This information includes the process type, status, start time, and duration. **Options** : You can define and provide a [`ListScriptProcessesFilter`](https://developers.google.com/apps-script/api/reference/rest/v1/processes/listScriptProcesses#ListScriptProcessesFilter) object to filter the process list. Only processes that match \*\*all\*\* of the filter conditions are returned. |


The Apps Script API provides a
[`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method that
remotely executes a specified Google Apps Script function. You can use
this method in a calling application to run a function in one of your script
projects remotely and receive a response.

> [!WARNING]
> **Warning:** The Apps Script API doesn't work with [service accounts](https://developers.google.com/identity/protocols/OAuth2ServiceAccount).

## Requirements

Before a calling application can use the
[`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method, you
must:

- **Deploy the script project as an API executable.** You can deploy, undeploy,
  and redeploy projects as needed.

- **Provide a properly scoped OAuth token for the execution.** This OAuth token
  must cover all the [scopes](https://developers.google.com/apps-script/concepts/scopes) used by the script,
  not just the ones used by the called function. See the full list of
  [authorization scopes](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#authorization-scopes)
  in the method reference.

- **Ensure that the script and the calling application's
  [OAuth2 client](https://developers.google.com/apps-script/api/how-tos/execute#step_3_configure_the_calling_application) share a common
  Google Cloud project.** The Cloud project must be a
  [standard Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects);
  default projects created for Apps Script projects are
  insufficient. You can use a new standard Cloud project or an existing
  one.

- [**Enable the Google Apps Script API**](https://developers.google.com/apps-script/api/quickstart/go#step_1_turn_on_the)
  in the Cloud project.

> [!NOTE]
> **Note:** API executables cease responding to `scripts.run` requests if their script project changes ownership to either a [shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives) or to an outside domain account. To fix this, redeploy the script in the new domain or shared drive, or move the script back to its original domain.

> [!WARNING]
> **Warning:** Script projects that use sensitive scopes are subject to review by Google. Users attempting to authorize apps that call such scripts with the Apps Script API might see a warning screen saying the app is unverified by Google. For more details, see the [OAuth client verification guide](https://developers.google.com/apps-script/guides/client-verification).

## The `scripts.run` method

The [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method
requires the following information:

- The [deployment ID](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#path-parameters) of the script deployment to execute.
- The [name of the function](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) to execute.
- The [list of parameters](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) the function requires, if any.

You can optionally configure your script to execute in *development mode* .
This mode executes with the most recently *saved* version of the script project
rather than the most recently deployed version. To do this, set the
`devMode` boolean in the
[request body](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body)
to `true`. Only the owner of the script can execute it in development mode.

### Handle parameter data types

Using the Apps Script API
[`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method
usually involves sending data to Apps Script as function
parameters and getting data back as function return values. The API can only
take and return values with basic types: strings, arrays, objects, numbers, and
booleans. More complex Apps Script objects like
[Document](https://developers.google.com/apps-script/reference/document/document) or
[Sheet](https://developers.google.com/apps-script/reference/spreadsheet/sheet) cannot be passed into or
from the script project by the API.

When your calling application is written in a strongly typed language such as
Java, it passes in parameters as a list or array of generic objects
corresponding to these basic types. In many cases, you can apply type
conversions automatically. For example, a function that takes a number parameter
can be given a Java `Double`, `Integer`, or `Long` object as a parameter without
extra handling.

When the API returns the function response, you often need to cast the
returned value to the correct type before it can be used. Here are some
Java-based examples:

- Numbers returned by the API to a Java application arrive as `java.math.BigDecimal` objects and may need to be converted to `Double` or `int` types.
- If the Apps Script function returns an array of strings, a
  Java application casts the response into a `List<String>` object:

      List<String> mylist = (List<String>)(op.getResponse().get("result"));

- If you want to return an array of `Bytes`, encode the array as a base64
  string within the Apps Script function and return that
  string instead:

      return Utilities.base64Encode(myByteArray); // returns a string.

The [example code samples](https://developers.google.com/apps-script/api/how-tos/execute#api_request_examples) below illustrate ways of
interpreting the API response.

## General procedure

To use the Apps Script API to execute Apps Script
functions, follow these steps:

### Step 1: Set up the common Cloud project

Both your script and the calling application need to share the same
Cloud project. This Cloud project can be an existing project or
a new project created for this purpose. Once you have a Cloud project, you
must [switch your script project to use it](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

### Step 2: Deploy the script as an API executable

1. Open the Apps Script project with the functions you want to use.
2. At the top right, click **Deploy** \> **New Deployment**.
3. In the dialog that opens, click **Enable deployment types** ![](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg) \> **API Executable**.
4. In the "Who has access" drop-down menu, select the users who are allowed to call the script's functions using the Apps Script API.
5. Click **Deploy**.

### Step 3: Configure the calling application

The calling application must enable the Apps Script API and establish
OAuth credentials before use. You must have access to the
Cloud project to do this.

1. Configure the Cloud project that your calling application and script are using:
   1. [Enable the **Apps Script API** in the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#enabling_an_api_in_a_standard_gcp_project).
   2. [Configure the OAuth consent screen](https://developers.google.com/apps-script/guides/cloud-platform-projects#completing_the_oauth_consent_screen).
   3. [Create OAuth credentials](https://developers.google.com/apps-script/guides/cloud-platform-projects#creating_oauth_credentials).
2. Open the script project and at the left, click **Overview** ![](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/info/default/24px.svg).
3. Under **Project OAuth scopes**, record all the scopes that the script requires.
4. In the calling application code, generate a script OAuth access token
   for the API call. This is not a token the API itself uses, but rather one
   the script requires when executing. It should be built using the
   Cloud project client ID and the script scopes you recorded.

   The [Google client libraries](https://developers.google.com/api-client-library) can assist in
   building this token and handling OAuth for the application, usually
   allowing you to build a higher-level "credentials" object using the script
   scopes. See the [Apps Script API quickstarts](https://developers.google.com/apps-script/api/quickstart/java)
   for examples of building a credentials object from a list of scopes.

### Step 4: Make the `scripts.run` request

Once the calling application is configured, you can make
[`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) calls:

1. Build an [API request](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) using the deployment ID, function name, and any required parameters.
2. Make the [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) call and include the script OAuth token you built in the header (if using a basic `POST` request) or use a credentials object you built with the script scopes.
3. Allow the script to finish executing. Scripts can take up to six minutes of execution time, so your application should allow for this.
4. Upon finishing, the script function may return a value, which the API delivers back to the application if the value is a supported type.

You can find [examples of `scripts.run` API calls](https://developers.google.com/apps-script/api/how-tos/execute#api_request_examples) in the
following section.

> [!WARNING]
> **Warning:** If your access token expires while the `scripts.run` API request is executing a script function, it can result in an `Authorization is required to perform that action` error. To avoid this, refresh your access token prior to making the API call if its `expires_in` time is less than the maximum [script runtime](https://developers.google.com/apps-script/guides/services/quotas#current_limitations) for your account (6 minutes in most cases).

To refresh your access token, add the following snippet before your
`scripts.run` API request:

    if (credential.getExpiresInSeconds() <= 360) {
      credential.refreshToken();
    }

## API request examples

The following examples show how to make an Apps Script API execution
request in various languages, calling an Apps Script function to
print out a list of folders in the user's root directory. The deployment ID of
the Apps Script project containing the executed function must be
specified where indicated with `ENTER_YOUR_DEPLOYMENT_ID_HERE`. The examples
rely on the [Google API Client libraries](https://developers.google.com/api-client-library).

### Target Script


The function in this script uses the Drive API.

You must [enable the Drive API](https://developers.google.com/drive/api/v3/enable-drive-api) in the
project hosting the script.

Additionally, calling applications must send OAuth credentials which include
the following Drive scope:

- `https://www.googleapis.com/auth/drive`

The example applications here use the Google client libraries to build
credential objects for OAuth using this scope.

    /**
     * Return the set of folder names contained in the user's root folder as an
     * object (with folder IDs as keys).
     * @return {Object} A set of folder names keyed by folder ID.
     */
    function getFoldersUnderRoot() {
      const root = DriveApp.getRootFolder();
      const folders = root.getFolders();
      const folderSet = {};
      while (folders.hasNext()) {
        const folder = folders.next();
        folderSet[folder.getId()] = folder.getName();
      }
      return folderSet;
    }https://github.com/googleworkspace/apps-script-samples/blob/8a31678d1d7e7eb9ab5e937adcc12b216ad9d4cb/apps-script/execute/target.js#L17-L31

### Java


    /**
     * Create a HttpRequestInitializer from the given one, except set
     * the HTTP read timeout to be longer than the default (to allow
     * called scripts time to execute).
     *
     * @param {HttpRequestInitializer} requestInitializer the initializer
     *                                 to copy and adjust; typically a Credential object.
     * @return an initializer with an extended read timeout.
     */
    private static HttpRequestInitializer setHttpTimeout(
        final HttpRequestInitializer requestInitializer) {
      return new HttpRequestInitializer() {
        @Override
        public void initialize(HttpRequest httpRequest) throws IOException {
          requestInitializer.initialize(httpRequest);
          // This allows the API to call (and avoid timing out on)
          // functions that take up to 6 minutes to complete (the maximum
          // allowed script run time), plus a little overhead.
          httpRequest.setReadTimeout(380000);
        }
      };
    }

    /**
     * Build and return an authorized Script client service.
     *
     * @param {Credential} credential an authorized Credential object
     * @return an authorized Script client service
     */
    public static Script getScriptService() throws IOException {
      Credential credential = authorize();
      return new Script.Builder(
          HTTP_TRANSPORT, JSON_FACTORY, setHttpTimeout(credential))
          .setApplicationName(APPLICATION_NAME)
          .build();
    }

    /**
     * Interpret an error response returned by the API and return a String
     * summary.
     *
     * @param {Operation} op the Operation returning an error response
     * @return summary of error response, or null if Operation returned no
     * error
     */
    public static String getScriptError(Operation op) {
      if (op.getError() == null) {
        return null;
      }

      // Extract the first (and only) set of error details and cast as a Map.
      // The values of this map are the script's 'errorMessage' and
      // 'errorType', and an array of stack trace elements (which also need to
      // be cast as Maps).
      Map<String, Object> detail = op.getError().getDetails().get(0);
      List<Map<String, Object>> stacktrace =
          (List<Map<String, Object>>) detail.get("scriptStackTraceElements");

      java.lang.StringBuilder sb =
          new StringBuilder("\nScript error message: ");
      sb.append(detail.get("errorMessage"));
      sb.append("\nScript error type: ");
      sb.append(detail.get("errorType"));

      if (stacktrace != null) {
        // There may not be a stacktrace if the script didn't start
        // executing.
        sb.append("\nScript error stacktrace:");
        for (Map<String, Object> elem : stacktrace) {
          sb.append("\n  ");
          sb.append(elem.get("function"));
          sb.append(":");
          sb.append(elem.get("lineNumber"));
        }
      }
      sb.append("\n");
      return sb.toString();
    }

    public static void main(String[] args) throws IOException {
      // ID of the script to call. Acquire this from the Apps Script editor,
      // under Publish > Deploy as API executable.
      String scriptId = "ENTER_YOUR_SCRIPT_ID_HERE";
      Script service = getScriptService();

      // Create an execution request object.
      ExecutionRequest request = new ExecutionRequest()
          .setFunction("getFoldersUnderRoot");

      try {
        // Make the API request.
        Operation op =
            service.scripts().run(scriptId, request).execute();

        // Print results of request.
        if (op.getError() != null) {
          // The API executed, but the script returned an error.
          System.out.println(getScriptError(op));
        } else {
          // The result provided by the API needs to be cast into
          // the correct type, based upon what types the Apps
          // Script function returns. Here, the function returns
          // an Apps Script Object with String keys and values,
          // so must be cast into a Java Map (folderSet).
          Map<String, String> folderSet =
              (Map<String, String>) (op.getResponse().get("result"));
          if (folderSet.size() == 0) {
            System.out.println("No folders returned!");
          } else {
            System.out.println("Folders under your root folder:");
            for (String id : folderSet.keySet()) {
              System.out.printf(
                  "\t%s (%s)\n", folderSet.get(id), id);
            }
          }
        }
      } catch (GoogleJsonResponseException e) {
        // The API encountered a problem before the script was called.
        e.printStackTrace(System.out);
      }
    }https://github.com/googleworkspace/java-samples/blob/19db17de8d3d018de067c5c8bbe50753b9f2055c/appsScript/execute/src/main/java/Execute.java#L18-L139

### JavaScript

    /**
     * Load the API and make an API call.  Display the results on the screen.
     */
    function callScriptFunction() {
      const scriptId = '<ENTER_YOUR_SCRIPT_ID_HERE>';

      // Call the Apps Script API run method
      //   'scriptId' is the URL parameter that states what script to run
      //   'resource' describes the run request body (with the function name
      //              to execute)
      try {
        gapi.client.script.scripts.run({
          'scriptId': scriptId,
          'resource': {
            'function': 'getFoldersUnderRoot',
          },
        }).then(function(resp) {
          const result = resp.result;
          if (result.error && result.error.status) {
            // The API encountered a problem before the script
            // started executing.
            appendPre('Error calling API:');
            appendPre(JSON.stringify(result, null, 2));
          } else if (result.error) {
            // The API executed, but the script returned an error.

            // Extract the first (and only) set of error details.
            // The values of this object are the script's 'errorMessage' and
            // 'errorType', and an array of stack trace elements.
            const error = result.error.details[0];
            appendPre('Script error message: ' + error.errorMessage);

            if (error.scriptStackTraceElements) {
              // There may not be a stacktrace if the script didn't start
              // executing.
              appendPre('Script error stacktrace:');
              for (let i = 0; i < error.scriptStackTraceElements.length; i++) {
                const trace = error.scriptStackTraceElements[i];
                appendPre('\t' + trace.function + ':' + trace.lineNumber);
              }
            }
          } else {
            // The structure of the result will depend upon what the Apps
            // Script function returns. Here, the function returns an Apps
            // Script Object with String keys and values, and so the result
            // is treated as a JavaScript object (folderSet).

            const folderSet = result.response.result;
            if (Object.keys(folderSet).length == 0) {
              appendPre('No folders returned!');
            } else {
              appendPre('Folders under your root folder:');
              Object.keys(folderSet).forEach(function(id) {
                appendPre('\t' + folderSet[id] + ' (' + id + ')');
              });
            }
          }
        });
      } catch (err) {
        document.getElementById('content').innerText = err.message;
        return;
      }
    }
    https://github.com/googleworkspace/browser-samples/blob/e365a5428ccbbe1ac231fcbe2f0ae48803ac4be7/apps-script/execute/index.js#L18-L81

### Node.js


    import {GoogleAuth} from 'google-auth-library';
    import {google} from 'googleapis';

    /**
     * Calls an Apps Script function to list the folders in the user's root Drive folder.
     */
    async function callAppsScript() {
      // The ID of the Apps Script project to call.
      const scriptId = '1xGOh6wCm7hlIVSVPKm0y_dL-YqetspS5DEVmMzaxd_6AAvI-_u8DSgBT';

      // Authenticate with Google and get an authorized client.
      // TODO (developer): Use an appropriate auth mechanism for your app.
      const auth = new GoogleAuth({
        scopes: 'https://www.googleapis.com/auth/drive',
      });

      // Create a new Apps Script API client.
      const script = google.script({version: 'v1', auth});

      const resp = await script.scripts.run({
        auth,
        requestBody: {
          // The name of the function to call in the Apps Script project.
          function: 'getFoldersUnderRoot',
        },
        scriptId,
      });

      if (resp.data.error?.details?.[0]) {
        // The API executed, but the script returned an error.
        // Extract the error details.
        const error = resp.data.error.details[0];
        console.log(`Script error message: ${error.errorMessage}`);
        console.log('Script error stacktrace:');

        if (error.scriptStackTraceElements) {
          // Log the stack trace.
          for (let i = 0; i < error.scriptStackTraceElements.length; i++) {
            const trace = error.scriptStackTraceElements[i];
            console.log('\t%s: %s', trace.function, trace.lineNumber);
          }
        }
      } else {
        // The script executed successfully.
        // The structure of the response depends on the Apps Script function's return value.
        const folderSet = resp.data.response ?? {};
        if (Object.keys(folderSet).length === 0) {
          console.log('No folders returned!');
        } else {
          console.log('Folders under your root folder:');
          Object.keys(folderSet).forEach((id) => {
            console.log('\t%s (%s)', folderSet[id], id);
          });
        }
      }
    }https://github.com/googleworkspace/node-samples/blob/dc39b4f4dca7af02bbec94c10a125ff643cc1820/apps-script/execute/index.js#L18-L74

### Python

    import google.auth
    from googleapiclient.discovery import build
    from googleapiclient.errors import HttpError


    def main():
      """Runs the sample."""
      # pylint: disable=maybe-no-member
      script_id = "1VFBDoJFy6yb9z7-luOwRv3fCmeNOzILPnR4QVmR0bGJ7gQ3QMPpCW-yt"

      creds, _ = google.auth.default()
      service = build("script", "v1", credentials=creds)

      # Create an execution request object.
      request = {"function": "getFoldersUnderRoot"}

      try:
        # Make the API request.
        response = service.scripts().run(scriptId=script_id, body=request).execute()
        if "error" in response:
          # The API executed, but the script returned an error.
          # Extract the first (and only) set of error details. The values of
          # this object are the script's 'errorMessage' and 'errorType', and
          # a list of stack trace elements.
          error = response["error"]["details"][0]
          print(f"Script error message: {0}.{format(error['errorMessage'])}")

          if "scriptStackTraceElements" in error:
            # There may not be a stacktrace if the script didn't start
            # executing.
            print("Script error stacktrace:")
            for trace in error["scriptStackTraceElements"]:
              print(f"\t{0}: {1}.{format(trace['function'], trace['lineNumber'])}")
        else:
          # The structure of the result depends upon what the Apps Script
          # function returns. Here, the function returns an Apps Script
          # Object with String keys and values, and so the result is
          # treated as a Python dictionary (folder_set).
          folder_set = response["response"].get("result", {})
          if not folder_set:
            print("No folders returned!")
          else:
            print("Folders under your root folder:")
            for folder_id, folder in folder_set.items():
              print(f"\t{0} ({1}).{format(folder, folder_id)}")

      except HttpError as error:
        # The API encountered a problem before the script started executing.
        print(f"An error occurred: {error}")
        print(error.content)


    if __name__ == "__main__":
      main()https://github.com/googleworkspace/python-samples/blob/def0f3ea49b648b36e0443f61143987e719c80b9/apps_script/execute/execute.py#L18-L71

## Limitations

The Apps Script API has the following limitations:

1. **A common Cloud project** . The script being called and the
   calling application must share a Cloud project. The
   Cloud project must be a
   [standard Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects);
   default projects created for Apps Script projects are
   insufficient.

2. **Basic parameter and return types** . The API cannot pass or return
   Apps Script-specific objects (such as
   [Documents](https://developers.google.com/apps-script/reference/document/document),
   [Blobs](https://developers.google.com/apps-script/reference/base/blob),
   [Calendars](https://developers.google.com/apps-script/reference/calendar),
   [Drive Files](https://developers.google.com/apps-script/reference/drive/file), etc.) to the
   application. Only basic types such as strings, arrays, objects, numbers, and
   booleans can be passed and returned.

3. **OAuth scopes**. The API can only execute scripts that have at least
   one required scope. This means you cannot use the API to call a script
   that doesn't require authorization of one or more services.

4. **No triggers** . The API cannot create Apps Script
   [triggers](https://developers.google.com/apps-script/guides/triggers/installable).


   