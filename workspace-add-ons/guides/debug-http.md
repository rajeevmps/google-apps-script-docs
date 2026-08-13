# Test and debug HTTP Google Workspace add-ons

As a Google Workspace add-on developer you might need to debug code to test changes or troubleshoot complex issues. Debugging Google Workspace add-ons can be done in many different ways depending on your app's architecture, what the app does, how your app is deployed, and your preferences.

This page explains how to debug an HTTP Google Workspace add-on using `ngrok`, which is a unified ingress platform that you can use to test local development environments. In this guide, you test code changes in a local environment and troubleshoot issues in a remote environment.

## Debug from local development environment

In this section, you interact with your Google Workspace add-on that executes in your local environment.

**Figure 1.** Debug in a local development environment.

### Prerequisites

### Node.js

*   Latest versions of `node` and `npm` installed in your local environment.
*   Latest version of `nodemon` installed in your local environment. It's used for auto-reload purposes:

        npm install -g nodemon

*   A Google Cloud project. You can follow the sections Prerequisites, and Set up the environment of the Quickstart guide.

*   The code of the Google Workspace add-on to debug in your local environment. We use the preview link features from the code example `3p-resources` from the GitHub repository `googleworkspace/add-ons-samples` in this guide for illustration purposes.

*   An IDE set up in your local environment that can debug. We use the `Visual Studio Code` IDE and its default debugging features in this guide for illustration purposes.

*   A `ngrok` account.

*   Latest version of `gcloud` installed and initialized in your local environment.

### Python

*   Latest version of `python3` installed in your local environment.
*   Latest version of `pip` and `virtualenv` installed in your local environment. They're used to manage Python packages and virtual environments respectively.
*   A Google Cloud project. You can follow the sections Prerequisites, and Set up the environment of the Quickstart guide.
*   The code of the Google Workspace add-on to debug in your local environment. We use the preview link features from the code example `3p-resources` from the GitHub repository `googleworkspace/add-ons-samples` in this guide for illustration purposes.
*   An IDE set up in your local environment that can debug. We use the `Visual Studio Code` IDE and its default debugging features in this guide for illustration purposes.
*   A `ngrok` account.
*   Latest version of `gcloud` installed and initialized in your local environment.

### Java

*   Latest stable version of the `Java SE 11's JDK` installed in your local environment.
*   Latest version of `Apache Maven` installed in your local environment. It's used to manage Java projects.
*   A Google Cloud project. You can follow the sections Prerequisites, and Set up the environment of the Quickstart guide.
*   The code of the Google Workspace add-on to debug in your local environment. We use the preview link features from the code example `3p-resources` from the GitHub repository `googleworkspace/add-ons-samples` in this guide for illustration purposes.
*   An IDE set up in your local environment that can debug. We use the `Visual Studio Code` IDE and its default debugging features in this guide for illustration purposes.
*   A `ngrok` account.
*   Latest version of `gcloud` installed and initialized in your local environment.

### Make the localhost service available publicly

You need to connect your local environment to the internet so that the Google Workspace add-on can access it. The `ngrok` application is used to redirect HTTP requests made to a public URL to your local environment.

1.  In a browser in your local environment, sign in to your `ngrok` account.
2.  Install the application and set up your `authtoken` in your local environment.
3.  Create a static domain in your `ngrok` account, it's referenced as `NGROK_STATIC_DOMAIN` in the instructions of this guide.

### Create and install the add-on deployment

1.  Configure the Google Workspace add-on to send all its HTTP requests to your static domain. Your deployment file should look like the following:

    ```json
    {
          "oauthScopes": [
            "https://www.googleapis.com/auth/workspace.linkpreview",
            "https://www.googleapis.com/auth/workspace.linkcreate"
          ],
          "addOns": {
            "common": {
              "name": "Manage support cases",
              "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png",
              "layoutProperties": {
                "primaryColor": "#dd4b39"
              }
            },
            "docs": {
              "linkPreviewTriggers": [
                {
                  "runFunction": "NGROK_STATIC_DOMAIN",
                  "patterns": [
                    {
                      "hostPattern": "example.com",
                      "pathPrefix": "support/cases"
                    },
                    {
                      "hostPattern": "*.example.com",
                      "pathPrefix": "cases"
                    },
                    {
                      "hostPattern": "cases.example.com"
                    }
                  ],
                  "labelText": "Support case",
                  "localizedLabelText": {
                    "es": "Caso de soporte"
                  },
                  "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
                }
              ],
              "createActionTriggers": [
                {
                  "id": "createCase",
                  "labelText": "Create support case",
                  "localizedLabelText": {
                    "es": "Crear caso de soporte"
                  },
                  "runFunction": "$URL2",
                  "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
                }
              ]
            },
            "httpOptions": {
              "granularOauthPermissionSupport": "OPT_IN"
            }
          }
        }
    ```

    Replace `NGROK_STATIC_DOMAIN` with the static domain in your `ngrok` account.

2.  Set the Google Cloud project to use:

        gcloud config set project PROJECT_ID

3.  Acquire new user credentials to use for Application Default Credentials:

        gcloud auth application-default login

    Replace `PROJECT_ID` with the project ID for the Google Cloud project of the app.

4.  Create the deployment:

        gcloud workspace-add-ons deployments create manageSupportCases \
            --deployment-file=DEPLOYMENT_FILE_PATH

    Replace `DEPLOYMENT_FILE_PATH` with the path of your deployment file.

5.  Install the deployment:

        gcloud workspace-add-ons deployments install manageSupportCases

    **Figure 2.** The Google Workspace add-on sends all its HTTP requests to the static domain. The `ngrok` public service acts as a bridge between the Google Workspace add-on and the application code that executes locally.

### Test the Google Workspace add-on

You can locally deploy, test, debug, and auto-reload your Google Workspace add-on.

**Note:** The Google Workspace add-on executes with the Cloud Run Functions Framework in the examples.

### Node.js

1.  From the `Visual Studio Code` IDE installed in your local environment, do the following:

    1.  In a new window, open the folder `add-ons-samples/node/3p-resources`.
    2.  Configure the application for local run and auto-reload debug by adding one dependency and two scripts in the `package.json` file:

        ```json
        {
                ...
                "dependencies": {
                  ...
                  "@google-cloud/functions-framework": "^3.3.0"
                },
                "scripts": {
                    ...
                    "start": "npx functions-framework --target=createLinkPreview --port=9000",
                    "debug-watch": "nodemon --watch ./ --exec npm start"
                }
                ...
            }
        ```

    3.  From the root directory, install the application:

            npm install

    4.  Create and configure a launch named `Debug Watch` that triggers the script `debug-watch` by creating the file `.vscode/launch.json` in the root directory:

        ```json
        {
                "version": "0.2.0",
                "configurations": [{
                    "type": "node",
                    "request": "launch",
                    "name": "Debug Watch",
                    "cwd": "${workspaceRoot}",
                    "runtimeExecutable": "npm",
                    "runtimeArgs": ["run-script", "debug-watch"]
                }]
            }
        ```

    5.  Add a breakpoint that pauses the HTTP request processing in the `index.js` file, and start running and debugging with the `Debug Watch` configuration added before. The application is now running and listening for HTTP requests on port `9000`.

        **Figure 3.** The application is running and listening for HTTP requests on port `9000`.

2.  Launch the `ngrok` application in your local environment:

        ngrok http --domain=NGROK_STATIC_DOMAIN 9000

    Replace `NGROK_STATIC_DOMAIN` with the static domain in your `ngrok` account. All requests are now redirected to your local environment and the port used by the application.

    **Figure 4.** The terminal with `ngrok` server running and redirecting.

3.  A web interface is also started on your localhost by the `ngrok` application. You can monitor all activities by opening it in a browser.

    **Figure 5.** The web interface hosted by the `ngrok` application showing no HTTP requests.

4.  Test your Google Workspace add-on by previewing a case URL in a new Google Doc with a tester account:

    *   Create a Google Doc.

        Create a Google Doc

    *   Type the following link and press `enter`:

        https://example.com/support/case/?name=Name1&description=Description1&priority=P1

    *   Click the link.

5.  In the `Visual Studio Code` in your local environment, you can see that the execution is paused at the breakpoint that was set.

    **Figure 6.** The execution is paused at the breakpoint that was set.

6.  When you resume the execution from the `Visual Studio Code` debugger before Google Workspace add-ons times out, the Google Workspace add-on displays the link preview in the Google Doc from the cache.

7.  You can check the HTTP request and response logs from the web interface hosted by the `ngrok` application in your local environment.

    **Figure 7.** The HTTP request from the web interface hosted by the `ngrok` application.

8.  To change the application behavior, replace `Case` with `Case:` on line `51` of the `index.js`. When you save the file, `nodemon` automatically reloads the application with the updated source code and `Visual Studio Code` remains in debug mode.

    **Figure 8.** The application is running and listening for HTTP requests on port `9000` with the code change loaded.

9.  This time, instead of clicking the link and waiting for a few seconds in a new Google Doc, you can select the last HTTP request logged on the web interface hosted by the `ngrok` application in your local environment and click `Replay`. Same as last time, your Google Workspace add-on doesn't reply because it's being actively debugged.

10.  When you resume the execution from the `Visual Studio Code` debugger, you can see from the web interface hosted by the `ngrok` application in your local environment that the application generates a response with the updated version of the preview card.

### Python

1.  From the `Visual Studio Code` IDE installed in your local environment, do the following:

    1.  In a new window, open the folder `add-ons-samples/python/3p-resources/create_link_preview`.
    2.  Create a virtual environment for Python `env` and activate it:

            virtualenv env

    3.  Install all project dependencies using `pip` in the virtual environment:

            pip install -r requirements.txt

    4.  Create the file `.vscode/launch.json` in the root directory and configure a launch named `Debug Watch` that triggers the application from the module `functions-framework` on port `9000` in debug mode on the virtual environment `env`:

        ```json
        {
                "version": "0.2.0",
                "configurations": [{
                    "type": "python",
                    "request": "launch",
                    "name": "Debug Watch",
                    "python": "${workspaceFolder}/env/bin/python3",
                    "module": "functions_framework",
                    "args": [
                        "--target", "create_link_preview",
                        "--port", "9000",
                        "--debug"
                    ]
                }]
            }
        ```

    5.  Add a breakpoint that pauses the HTTP request processing in the `main.py` file, and start running and debugging with the `Debug Watch` configuration added before. The application is now running and listening for HTTP requests on port `9000`.

        **Figure 3.** The application is running and listening for HTTP requests on port `9000`.

2.  Launch the `ngrok` application in your local environment:

        ngrok http --domain=NGROK_STATIC_DOMAIN 9000

    Replace `NGROK_STATIC_DOMAIN` with the static domain in your `ngrok` account. All requests are now redirected to your local environment and the port used by the application.

    **Figure 4.** The terminal with `ngrok` server running and redirecting.

3.  A web interface is also started on your localhost by the `ngrok` application. Monitor all activities by opening it in a browser.

    **Figure 5.** The web interface hosted by the `ngrok` application showing no HTTP requests.

4.  Test your Google Workspace add-on by previewing a case URL in a new Google Doc with a tester account:

    *   Create a Google Doc.

        Create a Google Doc

    *   Type the following link and press `enter`:

        https://example.com/support/case/?name=Name1&description=Description1&priority=P1

    *   Click the link.

5.  In the `Visual Studio Code` in your local environment, you can see that the execution is paused at the breakpoint that was set.

    **Figure 6.** The execution is paused at the breakpoint that was set.

6.  When you resume the execution from the `Visual Studio Code` debugger before Google Workspace add-ons times out, the Google Workspace add-on displays the link preview in the Google Doc from the cache.

7.  You can check the HTTP request and response logs from the web interface hosted by the `ngrok` application in your local environment.

    **Figure 7.** The HTTP request from the web interface hosted by the `ngrok` application.

8.  To change the application behavior, replace `Case` with `Case:` on line `56` of the `main.py` file. When you save the file, `Visual Studio Code` automatically reloads the application with the updated source code and remains in debug mode.

    **Figure 8.** The application is running and listening for HTTP requests on port `9000` with the code change loaded.

9.  This time, instead of clicking the link and waiting for a few seconds in a new Google Doc, you can select the last HTTP request logged on the web interface hosted by the `ngrok` application in your local environment and click `Replay`. Same as last time, your Google Workspace add-on doesn't reply because it's being actively debugged.

10.  When you resume the execution from the `Visual Studio Code` debugger, you can see from the web interface hosted by the `ngrok` application in your local environment that the application generates a response with the updated version of the preview card.

### Java

1.  From the `Visual Studio Code` IDE installed in your local environment, do the following:

    1.  In a new window, open the folder `add-ons-samples/java/3p-resources`.
    2.  Configure the Maven project to run the application `CreateLinkPreview` on port `9000` locally by adding the Cloud Functions Framework build plugin `function-maven-plugin` to the `pom.xml` file:

        ```xml
        ...
            <plugin>
                <groupId>com.google.cloud.functions</groupId>
                <artifactId>function-maven-plugin</artifactId>
                <version>0.11.0</version>
                <configuration>
                    <functionTarget>CreateLinkPreview</functionTarget>
                    <port>9000</port>
                </configuration>
            </plugin>
            ...
        ```

    3.  You can now launch it locally in debug mode:

            mvnDebug function:run
            Preparing to execute Maven in debug mode
            Listening for transport dt_socket at address: 8000

    4.  Create the file `.vscode/launch.json` in the root directory and configure a launch named `Remote Debug Watch` that attaches to the application previously launched on port `8000`:

        ```json
        {
                "version": "0.2.0",
                "configurations": [{
                    "type": "java",
                    "request": "attach",
                    "name": "Remote Debug Watch",
                    "projectName": "http-function",
                    "hostName": "localhost",
                    "port": 8000
                }]
            }
        ```

    5.  Add a breakpoint that pauses the HTTP request processing in the `CreateLinkPreview.java` file, and start attaching and debugging with the `Remote Debug Watch` configuration added before. The application is now running and listening for HTTP requests on port `9000`.

        **Figure 3.** The application is running and listening for HTTP requests on port `9000`.

2.  Launch the `ngrok` application in your local environment:

        ngrok http --domain=NGROK_STATIC_DOMAIN 9000

    Replace `NGROK_STATIC_DOMAIN` with the static domain in your `ngrok` account. All requests are now redirected to your local environment and the port used by the application.

    **Figure 4.** The terminal with `ngrok` server running and redirecting.

3.  A web interface is also started on your localhost by the `ngrok` application. Monitor all activities by opening it in a browser.

    **Figure 5.** The web interface hosted by the `ngrok` application showing no HTTP requests.

4.  Test your Google Workspace add-on by previewing a case URL in a new Google Doc with a tester account:

    *   Create a Google Doc.

        Create a Google Doc

    *   Type the following link and press `enter`:

        https://example.com/support/case/?name=Name1&description=Description1&priority=P1

    *   Click the link.

5.  In the `Visual Studio Code` in your local environment, you can see that the execution is paused at the breakpoint that was set.

    **Figure 6.** The execution is paused at the breakpoint that was set.

6.  When you resume the execution from the `Visual Studio Code` debugger before Google Workspace add-ons times out, the Google Workspace add-on displays the link preview in the Google Doc from the cache.

7.  You can check the HTTP request and response logs from the web interface hosted by the `ngrok` application in your local environment.

    **Figure 7.** The HTTP request from the web interface hosted by the `ngrok` application.

8.  To change the application behavior, replace `Case` with `Case:` on line `78` of the `CreateLinkPreview.java` file, restart the `mvnDebug` process, and relaunch `Remote Debug Watch` to reattach and restart debugging.

9.  This time, instead of clicking the link and waiting for a few seconds in a new Google Doc, you can select the last HTTP request logged on the web interface hosted by the `ngrok` application in your local environment and click `Replay`. Same as last time, your Google Workspace add-on doesn't reply because it's being actively debugged.

10.  When you resume the execution from the `Visual Studio Code` debugger, you can see from the web interface hosted by the `ngrok` application in your local environment that the application generates a response with the updated version of the preview card.

## Debug from remote environment

In this section, you interact with your Google Workspace add-on that executes on a remote environment.

**Figure 9.** Debug from the remote environment.

### Prerequisites

*   Your Google Workspace add-on is deployed and installed.
*   Your application is running in your remote environment with the debugger enabled on a given port, and it's referenced as `REMOTE_DEBUG_PORT` in the instructions of this guide.
*   Your local environment can `ssh` to your remote environment.
*   An IDE is set up in your local environment that can debug. We use the `Visual Studio Code` IDE and its default debugging features in this guide for illustration purposes.

### Connect your local and remote environments

In your local environment from where you want to initiate a debug client connection, set up an SSH tunnel:

    ssh -L LOCAL_DEBUG_PORT:localhost:REMOTE_DEBUG_PORT REMOTE_USERNAME@REMOTE_ADDRESS

Replace the following:

*   `LOCAL_DEBUG_PORT`: The debug port in your local environment.
*   `REMOTE_USERNAME`: The username in your remote environment.
*   `REMOTE_ADDRESS`: The address of your remote environment.
*   `REMOTE_DEBUG_PORT`: The debug port in your remote environment.

The debug port in your local environment is now linked to the debug port in your remote environment.

### Start debugging

From the `Visual Studio Code` IDE installed in your local environment, do the following:

1.  In a new window, open the source code of your app.
2.  Create the file `.vscode/launch.json` in the root directory and configure a launch named `Debug Remote` that attaches to the debug port in your local environment:

    ### Node.js

    ```json
    {
            "version": "0.2.0",
            "configurations": [{
                "type": "node",
                "request": "attach",
                "name": "Debug Remote",
                "address": "127.0.0.1",
                "port": LOCAL_DEBUG_PORT
            }]
        }
    ```

    ### Python

    ```json
    {
            "version": "0.2.0",
            "configurations": [{
                "type": "python",
                "request": "attach",
                "name": "Debug Remote",
                "connect": {
                    "host": "127.0.0.1",
                    "port": LOCAL_DEBUG_PORT
                }
            }]
        }
    ```

    ### Java

    ```json
    {
            "version": "0.2.0",
            "configurations": [{
                "type": "java",
                "request": "attach",
                "name": "Debug Remote",
                "hostName": "127.0.0.1",
                "port": LOCAL_DEBUG_PORT
            }]
        }
    ```

    Replace `LOCAL_DEBUG_PORT` with the debug port in your local environment.

3.  Add a breakpoint in the source code of your app that pauses the HTTP request processing, and start running and debugging with the `Debug Remote` configuration added before.

    Interact with your installed Google Workspace add-on. Your Google Workspace add-on doesn't reply because it's being actively debugged in the `Visual Studio Code` IDE.

## Related topics

*   Learn how to query error logs.
