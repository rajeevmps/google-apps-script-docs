# Build a Google Workspace add-on with Node.js

- Develop Google Workspace add-ons using Cloud Functions and Node.js for basic functionalities, ideal for simple integrations.
- This quickstart provides a step-by-step guide to set up, deploy, and install a sample add-on within your Google Workspace environment.
- For advanced add-ons with richer features, it is recommended to leverage Cloud Run instead of Cloud Functions for a more robust solution.
- The process involves configuring OAuth consent, deploying a Cloud Function, creating the add-on deployment, and installing it for testing.

## Objectives

- Set up your environment.
- Create and deploy a Cloud Run function.
- Create and deploy the add-on.
- Install the add-on.

## Prerequisites

- A Google Cloud project.
- Enable billing for your Cloud project. Learn how to verify the billing status of your projects.
- The Cloud SDK is configured with the Cloud project.

## Set up your environment

### Open your Cloud project in the Google Cloud console

1. In the Google Cloud console, go to the **Select a project** page.
2. Select the Google Cloud project you want to use. Or, click **Create project** and follow the on-screen instructions. If you create a Google Cloud project, you might need to turn on billing for the project.

### Configure the OAuth consent screen

1. In the Google API Console, go to Menu > **Google Auth platform** > **Branding**.
2. If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in Branding, Audience, and Data Access. If you see a message that says **Google Auth platform not configured yet**, click **Get Started**:
   - Under **App Information**, in **App name**, enter a name for the app.
   - In **User support email**, choose a support email address where users can contact you if they have questions about their consent.
   - Click **Next**.
   - Under **Audience**, select **Internal**.
   - Click **Next**.
   - Under **Contact Information**, enter an **Email address** where you can be notified about any changes to your project.
   - Click **Next**.
   - Under **Finish**, review the Google API Services User Data Policy and if you agree, select **I agree to the Google API Services: User Data Policy**.
   - Click **Continue**.
   - Click **Create**.
3. For now, you can skip adding scopes. In the future, when you create an app for use outside of your Google Workspace organization, you must change the **User type** to **External**. Then add the authorization scopes that your app requires.

## Create and deploy a Cloud Run function

1. Click **Authorize** to provision and connect to Cloud Shell.

2. In the Cloud Shell Terminal, turn on the Cloud Run functions API, the Cloud Build API, the Google Workspace add-ons API, the Compute Engine API, and the Cloud Run API:

```
gcloud services enable cloudfunctions.googleapis.com  \
                        cloudbuild.googleapis.com  \
                        gsuiteaddons.googleapis.com  \
                        compute.googleapis.com  \
                        run.googleapis.com
```

3. Launch the Cloud Shell Editor by clicking **Open Editor** on the toolbar of the Cloud Shell window. This built-in code editor provides the convenience of viewing and editing files in the same environment where projects are built and deployed.

4. In the empty directory, create the file `function.js` with the following sample code:

```javascript
/**
 * Cloud Run function that loads the homepage for a
 * Google Workspace add-on.
 *
 * @param {Object} req Request sent from Google
 * @param {Object} res Response to send back
 */
exports.loadHomePage = function addonsHomePage (req, res) {
  res.send(createAction());
};

/** Creates a card with two widgets. */
function createAction() {
  return {
    "action": {
      "navigations": [
        {
          "pushCard": {
            "header": {
              "title": "Cats!"
            },
            "sections": [
              {
                "widgets": [
                  {
                    "textParagraph": {
                      "text": "Your random cat:"
                    }
                  },
                  {
                    "image": {
                      "imageUrl": "https://cataas.com/cat"
                     }
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  };
}
```

5. In the same directory, create the file `package.json` with the following sample code:

```json
{
  "dependencies": {
    "@google-cloud/functions-framework": "^3.0.0"
  }
}
```

6. Return to the Cloud Shell Terminal by clicking **Open Terminal**.

7. Add the `Cloud Build Service Account` role (`roles/cloudbuild.builds.builder`) to the Compute Engine default service account.

First, setup the service account permission:

```
export PROJECT_ID=$(gcloud config get project)
export SERVICE_ACCOUNT_NAME=$(gcloud compute project-info describe \
  --format="value(defaultServiceAccount)")
```

Next, grant the missing service account permission:

```
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:$SERVICE_ACCOUNT_NAME" \
  --role="roles/cloudbuild.builds.builder"
```

8. Run the following command to deploy the function:

```
gcloud run deploy loadHomePage --runtime nodejs22 --trigger-http
```

If prompted, specify that you don't allow unauthenticated invocations of the function. It might take a couple minutes for the function to deploy.

## Create an add-on deployment

1. Find the service account email for the add-on:

```
gcloud workspace-add-ons get-authorization
```

2. Grant the service account the `cloudfunctions.invoker` role. Replace SERVICE_ACCOUNT_EMAIL with the `serviceAccountEmail` field from the previous step.

```
gcloud run services add-iam-policy-binding loadHomePage \
  --role roles/roles/run.invoker \
  --member serviceAccount:SERVICE_ACCOUNT_EMAIL
```

3. Get the URL of the deployed function. To get the URL, run the following command and look for the `url` field under the `httpsTrigger` section:

```
gcloud run services describe loadHomePage
```

4. Return to the Cloud Shell Editor by clicking **Open Editor**.

5. In the same directory as `package.json`, create the file `deployment.json` with the following sample code. Replace URL with the `url` of the deployed function from the previous step.

```json
{
  "oauthScopes": ["https://www.googleapis.com/auth/gmail.addons.execute"],
  "addOns": {
    "common": {
      "name": "My HTTP Add-on",
      "logoUrl": "https://raw.githubusercontent.com/webdog/octicons-png/main/black/beaker.png",
      "homepageTrigger": {
        "runFunction": "URL"
      }
    },
    "gmail": {},
    "drive": {},
    "calendar": {},
    "docs": {},
    "sheets": {},
    "slides": {},
    "httpOptions": {
      "granularOauthPermissionSupport": "OPT_IN"
    }
  }
}
```

6. Return to the Cloud Shell Terminal to create the deployment:

```
gcloud workspace-add-ons deployments create quickstart \
  --deployment-file=deployment.json
```

## Install the add-on

1. Install the deployment in development mode:

```
gcloud workspace-add-ons deployments install quickstart
```

2. Open or reload Gmail to view the add-on. In the toolbar on the right, look for a beaker icon.

3. Click the icon to open the add-on. If prompted, authorize the add-on.

## Optional: Clean up

To avoid charges, delete the resources you created:

1. Uninstall the add-on from your Google Account:

```
gcloud workspace-add-ons deployments uninstall quickstart
```

2. To avoid charges for the resources used in this quickstart, delete the Cloud project:

```
gcloud projects delete PROJECT_ID
```

Replace PROJECT_ID with the ID of the Cloud project that you used for the quickstart. You can find the Cloud project ID in the Google API Console on the Dashboard page.

## Related topics

To add more features to your Google Workspace add-on, refer to the following:

- Build a Google Workspace add-on using HTTP endpoints
- Codelab: Build a Google Workspace add-on with Node.js and Cloud Run
- Preview links with smart chips
