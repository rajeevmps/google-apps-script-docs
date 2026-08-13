# Execute functions with the Google Apps Script API

## Page Summary

- The `scripts.run` method of the Google Apps Script API allows calling applications to remotely execute specified Apps Script functions and receive responses.
- To use the `scripts.run` method, the script project must be deployed as an API executable, the calling application must provide a properly scoped OAuth token, and both must share a common standard Google Cloud project with the Apps Script API enabled.
- The `scripts.run` method requires the script project ID, the name of the function to execute, and any required parameters.
- The API can only pass and return basic data types (strings, arrays, objects, numbers, booleans), not complex Apps Script objects.
- There are several limitations to the API, including the requirement for a common standard Cloud project, restriction to basic data types, inability to call scripts without scopes, and the lack of trigger creation functionality.

The Apps Script API provides a [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method that remotely executes a specified Google Apps Script function. You can use this method in a calling application to run a function in one of your script projects remotely and receive a response.

**Warning:** The Apps Script API doesn't work with [service accounts](https://developers.google.com/identity/protocols/OAuth2ServiceAccount).

## Requirements

Before a calling application can use the [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method, you must:

- **Deploy the script project as an API executable.** You can deploy, undeploy, and redeploy projects as needed.

- **Provide a properly scoped OAuth token for the execution.** This OAuth token must cover all the [scopes](https://developers.google.com/apps-script/concepts/scopes) used by the script, not just the ones used by the called function. See the full list of [authorization scopes](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#authorization-scopes) in the method reference.

- **Ensure that the script and the calling application's [OAuth2 client](#step_3_configure_the_calling_application) share a common Google Cloud project.** The Cloud project must be a [standard Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects); default projects created for Apps Script projects are insufficient. You can use a new standard Cloud project or an existing one.

- [**Enable the Google Apps Script API**](https://developers.google.com/apps-script/api/quickstart/go#step_1_turn_on_the) in the Cloud project.

**Note:** API executables cease responding to `scripts.run` requests if their script project changes ownership to either a [shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives) or to an outside domain account. To fix this, redeploy the script in the new domain or shared drive, or move the script back to its original domain.

**Warning:** Script projects that use sensitive scopes are subject to review by Google. Users attempting to authorize apps that call such scripts with the Apps Script API might see a warning screen saying the app is unverified by Google. For more details, see the [OAuth client verification guide](https://developers.google.com/apps-script/guides/client-verification).

## The `scripts.run` method

The [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method requires the following information:

- The [deployment ID](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#path-parameters) of the script deployment to execute.
- The [name of the function](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) to execute.
- The [list of parameters](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) the function requires, if any.

You can optionally configure your script to execute in _development mode_. This mode executes with the most recently _saved_ version of the script project rather than the most recently deployed version. To do this, set the `devMode` boolean in the [request body](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) to `true`. Only the owner of the script can execute it in development mode.

### Handle parameter data types

Using the Apps Script API [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) method usually involves sending data to Apps Script as function parameters and getting data back as function return values. The API can only take and return values with basic types: strings, arrays, objects, numbers, and booleans. More complex Apps Script objects like [Document](https://developers.google.com/apps-script/reference/document/document) or [Sheet](https://developers.google.com/apps-script/reference/spreadsheet/sheet) cannot be passed into or from the script project by the API.

When your calling application is written in a strongly typed language such as Java, it passes in parameters as a list or array of generic objects corresponding to these basic types. In many cases, you can apply type conversions automatically. For example, a function that takes a number parameter can be given a Java `Double`, `Integer`, or `Long` object as a parameter without extra handling.

When the API returns the function response, you often need to cast the returned value to the correct type before it can be used. Here are some Java-based examples:

- Numbers returned by the API to a Java application arrive as `java.math.BigDecimal` objects and may need to be converted to `Double` or `int` types.
- If the Apps Script function returns an array of strings, a Java application casts the response into a `List<String>` object:

```java
List<String> mylist = (List<String>)(op.getResponse().get("result"));
```

- If you want to return an array of `Bytes`, encode the array as a base64 string within the Apps Script function and return that string instead:

```java
return Utilities.base64Encode(myByteArray); // returns a string.
```

## General procedure

To use the Apps Script API to execute Apps Script functions, follow these steps:

### Step 1: Set up the common Cloud project

Both your script and the calling application need to share the same Cloud project. This Cloud project can be an existing project or a new project created for this purpose. Once you have a Cloud project, you must [switch your script project to use it](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

### Step 2: Deploy the script as an API executable

1. Open the Apps Script project with the functions you want to use.
2. At the top right, click **Deploy** > **New Deployment**.
3. In the dialog that opens, click **Enable deployment types** > **API Executable**.
4. In the "Who has access" drop-down menu, select the users who are allowed to call the script's functions using the Apps Script API.
5. Click **Deploy**.

### Step 3: Configure the calling application

The calling application must enable the Apps Script API and establish OAuth credentials before use. You must have access to the Cloud project to do this.

1. Configure the Cloud project that your calling application and script are using:
   1. [Enable the **Apps Script API** in the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#enabling_an_api_in_a_standard_gcp_project).
   2. [Configure the OAuth consent screen](https://developers.google.com/apps-script/guides/cloud-platform-projects#completing_the_oauth_consent_screen).
   3. [Create OAuth credentials](https://developers.google.com/apps-script/guides/cloud-platform-projects#creating_oauth_credentials).
2. Open the script project and at the left, click **Overview**.
3. Under **Project OAuth scopes**, record all the scopes that the script requires.
4. In the calling application code, generate a script OAuth access token for the API call. This is not a token the API itself uses, but rather one the script requires when executing. It should be built using the Cloud project client ID and the script scopes you recorded.

   The [Google client libraries](https://developers.google.com/api-client-library) can assist in building this token and handling OAuth for the application, usually allowing you to build a higher-level "credentials" object using the script scopes. See the [Apps Script API quickstarts](https://developers.google.com/apps-script/api/quickstart/java) for examples of building a credentials object from a list of scopes.

### Step 4: Make the `scripts.run` request

Once the calling application is configured, you can make [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) calls:

1. Build an [API request](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run#request-body) using the deployment ID, function name, and any required parameters.
2. Make the [`scripts.run`](https://developers.google.com/apps-script/api/reference/rest/v1/scripts/run) call and include the script OAuth token you built in the header (if using a basic `POST` request) or use a credentials object you built with the script scopes.
3. Allow the script to finish executing. Scripts can take up to six minutes of execution time, so your application should allow for this.
4. Upon finishing, the script function may return a value, which the API delivers back to the application if the value is a supported type.

You can find examples of `scripts.run` API calls in the following section.

**Warning:** If your access token expires while the `scripts.run` API request is executing a script function, it can result in an `Authorization is required to perform that action` error. To avoid this, refresh your access token prior to making the API call if its `expires_in` time is less than the maximum [script runtime](https://developers.google.com/apps-script/guides/services/quotas#current_limitations) for your account (6 minutes in most cases).

To refresh your access token, add the following snippet before your `scripts.run` API request:

```java
if (credential.getExpiresInSeconds() <= 360) {
  credential.refreshToken();
}
```

## API request examples

The following examples show how to make an Apps Script API execution request in various languages, calling an Apps Script function to print out a list of folders in the user's root directory. The deployment ID of the Apps Script project containing the executed function must be specified where indicated with `ENTER_YOUR_DEPLOYMENT_ID_HERE`. The examples rely on the [Google API Client libraries](https://developers.google.com/api-client-library).

### Target Script

The function in this script uses the Drive API.

You must [enable the Drive API](https://developers.google.com/drive/api/v3/enable-drive-api) in the project hosting the script.

Additionally, calling applications must send OAuth credentials which include the following Drive scope:

- `https://www.googleapis.com/auth/drive`

The example applications here use the Google client libraries to build credential objects for OAuth using this scope.

```javascript
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
}
```

### Java

```java
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
}
```

### JavaScript

```javascript
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
```

### Node.js

```javascript
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
}
```

### Python

```python
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
  main()
```

## Limitations

The Apps Script API has the following limitations:

1. **A common Cloud project**. The script being called and the calling application must share a Cloud project. The Cloud project must be a [standard Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects); default projects created for Apps Script projects are insufficient.

2. **Basic parameter and return types**. The API cannot pass or return Apps Script-specific objects (such as [Documents](https://developers.google.com/apps-script/reference/document/document), [Blobs](https://developers.google.com/apps-script/reference/base/blob), [Calendars](https://developers.google.com/apps-script/reference/calendar), [Drive Files](https://developers.google.com/apps-script/reference/drive/file), etc.) to the application. Only basic types such as strings, arrays, objects, numbers, and booleans can be passed and returned.

3. **OAuth scopes**. The API can only execute scripts that have at least one required scope. This means you cannot use the API to call a script that doesn't require authorization of one or more services.

4. **No triggers**. The API cannot create Apps Script [triggers](https://developers.google.com/apps-script/guides/triggers/installable).

Source: https://developers.google.com/apps-script/api/how-tos/execute
