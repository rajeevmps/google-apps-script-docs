# Build a Google Chat app with an Agent2Agent agent

This page explains how to build a Google Workspace add-on that works in
Google Chat and interfaces with an AI agent that uses the
[Agent2Agent (A2A)](https://a2a-protocol.org/latest/) protocol.
You develop the agent using the
[Agent Development Kit (ADK)](https://google.github.io/adk-docs),
and host it in
[Vertex AI Agent Engine](https://docs.cloud.google.com/agent-builder/agent-engine/overview).

**Note:** In Google Chat, add-ons appear to users as
Google Chat apps. You can also build your Chat app using 
*Google Chat API interaction events*. To learn more, see the
[Extend Google Chat overview](https://developers.google.com/workspace/add-ons/chat).

AI agents autonomously perceive their environment, reason, and execute complex,
multi-step actions to achieve a defined goal. In this tutorial, you deploy the
[LLM Auditor multi-agent sample](https://github.com/google/adk-samples/tree/main/python/agents/llm-auditor)
that critiques and revises facts using Gemini and Google Search grounding.

![LLM Auditor multi-agent sample as Chat app.](https://developers.google.com/static/workspace/add-ons/images/quickstart-adk-agent.png)

The following diagram shows the architecture and messaging pattern:

![Architecture of a Chat app implemented with an A2A AI agent.](https://developers.google.com/static/workspace/add-ons/images/design-patterns/a2a-agent.svg)

In the diagram, a user interacting with a
Chat app implemented with an A2A agent has
the following flow of information:

1. A user sends a message to a Chat app, either in a
direct message or in a Chat space.
2. The Chat app logic that's implemented either in
Apps Script or as a web server with HTTP endpoints receives
and processes the message.
3. The A2A agent hosted with Vertex AI Agent Engine receives and processes
the interaction.
4. Optionally, the Chat app or AI agent can integrate
with Google Workspace services, such as Calendar or
Sheets, or other Google services, such as Google Maps
or YouTube.
5. The Chat app sends responses asynchronously,
using the Google Chat API to communicate the AI agent's progress.
6. The responses are delivered to the user.

## Objectives

- Set up your environment.
- Deploy the A2A agent.
- Deploy the Chat app.
- Configure the Chat app.
- Test the Chat app.

## Prerequisites

- A Business or Enterprise
[Google Workspace](https://support.google.com/a/answer/6043576) account with access to
[Google Chat](https://workspace.google.com/products/chat/).
- A Google Cloud project with billing enabled. To check that an existing project has billing enabled,
see [Verify the
billing status of your projects](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled). To create a project and set up billing, see
[Create a Google Cloud project](https://developers.google.com/workspace/guides/create-project).
- [Prerequisites of the LLM Auditor ADK agent](https://github.com/google/adk-samples/tree/main/python/agents/llm-auditor)
    - Python 3.11+: For installation, follow instructions on the official
  [Python website](https://docs.python.org/3/using/index.html).
    - Python Poetry: For installation, follow instructions on the official
  [Poetry website](https://python-poetry.org/docs/).
    - Google Cloud CLI: For installation, follow instructions on the official
  [Google Cloud website](https://cloud.google.com/sdk/docs/install).

## Set up your environment

### Enable the Google Cloud APIs

- In the Google Cloud console, enable the Google Chat, Vertex AI, and Cloud Resource Manager APIs.
[Enable the APIs](https://console.cloud.google.com/flows/enableapi?apiid=chat.googleapis.com,aiplatform.googleapis.com,cloudresourcemanager.googleapis.com)

### Configure the OAuth consent screen

All apps using OAuth 2.0 require a consent screen configuration. Configuring
your app's OAuth consent screen defines what is displayed to users and app
reviewers, and registers your app so you can publish it later.

1. In the Google API Console, go to Menu menu
> **Google Auth platform**
> **Branding**.
 [Go to Branding](https://console.developers.google.com/auth/branding)
2. If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in [Branding](https://console.developers.google.com/auth/branding), [Audience](https://console.developers.google.com/auth/audience), and [Data Access](https://console.developers.google.com/auth/scopes). If you see a message that says **Google Auth platform not configured yet**, click **Get Started**:
3. For now, you can skip adding scopes.
 In the future, when you create an app for use outside of your
 Google Workspace organization, you must change the **User type** to **External**. Then
 add the authorization scopes that your app requires. To learn more, see the full
 [Configure OAuth consent](https://developers.google.com/workspace/guides/configure-oauth-consent) guide.

### Create a service account in Google Cloud console

Create a new service account with the role `Vertex AI User` by following
these steps:

### Google Cloud Console

1. In the Google Cloud Console, go to Menu menu
> **IAM & Admin**
> **Service Accounts**.
 [Go to Service Accounts](https://console.developers.google.com/iam-admin/serviceaccounts)
The remaining steps appear in the Google Cloud Console.
2. Select a Google Cloud project.
3. Click **Create service account**.
4. Enter a service account name to display in the Google Cloud Console.
 Note: By default, Google creates a unique service account ID based on the service account name.
 You can modify the ID in the service account ID field. You cannot change the ID later.
5. If you don't want to set access controls now, click **Done** to finish creating the service account. To set access controls now, click **Create and continue** and proceed to the next step.
 **Note:** Granting access control here only affects Google Cloud resources. Google Workspace resources (such as Google Sheets
 and Google Drive) are shared and configured separately.
6. Optional: Assign roles to your service account to grant access to your Google Cloud project's resources in addition to Google Workspace resources. For more details, refer to [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access).
7. Click **Continue**.
8. Optional: Enter users or groups that can manage and perform actions with this service account. For more details, refer to [Service account impersonation](https://docs.cloud.google.com/iam/docs/service-account-impersonation).
9. Click **Done** to finish creating the service account.
 Make a note of the email address for the service account.

### gcloud CLI

1. Create the service account:
   ```bash session
   gcloud iam service-accounts create SERVICE_ACCOUNT_NAME \
     --display-name="SERVICE_ACCOUNT_NAME"
   ```
2. Optional: Assign roles to your service account to grant access to your Google Cloud project's resources in addition to Google Workspace resources. For more details, refer to [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access).

The service account appears on the service account page.

### Create a private key

> **Warning:** This example uses an exported
> service account key for simplicity's sake. Exporting a private key is not
> recommended in production because it shouldn't be stored in an insecure
> location, such as source control.
>
> To learn more about secure service
> account implementations and best practices, see
> [Choose
> when to use service accounts](https://cloud.google.com/iam/docs/best-practices-for-using-and-managing-service-accounts#choose-when-to-use).

To create and download a private key for the service account, follow these
steps:

1. In the Google Cloud Console, go to Menu menu
> **IAM & Admin**
> **Service Accounts**.
 [Go to Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts)
The remaining steps appear in the Google Cloud Console.
2. Select a Google Cloud project.
3. Click the email address of the service account that you want to create a key for.
4. Click the **Keys** tab.
5. Click the **Add key** drop-down menu, then select **Create new key**.
6. Select **JSON** as the **Key type** and click **Create**.
 Your new public/private key pair is generated and downloaded to your
 machine as a service account key file. Save the downloaded JSON file as `credentials.json`
 in your working directory. This file is the only copy of this key. After you
 download the key file, you cannot download it again. For information about how to store
 your key securely, see
 [Best practices for managing service account keys](https://docs.cloud.google.com/iam/docs/best-practices-for-managing-service-account-keys).

For more information about service accounts, see
[service accounts in the Google Cloud IAM documentation](https://cloud.google.com/iam/docs/service-accounts).

## Deploy the A2A agent

1. If you haven't done so, authenticate with your Google Cloud account and
configure the Google Cloud CLI to use your Google Cloud project.
Replace `PROJECT_ID` with the ID of your Cloud project.
   ```bash
   gcloud auth application-default login
   ```
2. Download the ADK samples GitHub repository using this button:
[Download adk-samples](https://github.com/google/adk-samples/archive/refs/heads/main.zip)
3. In your preferred local development environment, extract the downloaded
archive file and open the `adk-samples/python/agents/llm-auditor` directory.
   ```bash
   unzip adk-samples-main.zip
   ```
4. Update the implementation to deploy the ADK agent as an A2A remote agent:
   1. **pyproject.toml**: Add ADK and A2A SDK dependencies in deployment group.
    .filepath {
    color: #fff;
    margin: 6px;
    max-width: calc(100% - 160px); /* Give at least 160px for the "View on GitHub" button. */
    text-overflow: ellipsis;
    text-shadow: rgba(0,0,0,0.1) 1px 1px;
    overflow: hidden;
    }
    .github-docwidget-gitinclude-code .prettyprint {
    margin: 0;
    }
    .view-on-github {
    text-shadow: rgba(12,12,12,0.1) 1px 1px;
    }
   apps-script/chat/a2a-ai-agent/llm-auditor/pyproject.toml
   [View on GitHub](https://github.com/googleworkspace/add-ons-samples/blob/main/apps-script/chat/a2a-ai-agent/llm-auditor/pyproject.toml)
    Code
   [project]
   name = "llm-auditor"
   version = "0.1.0"
   description = "The LLM Auditor evaluates LLM-generated answers, verifies actual accuracy using the web, and refines the response to ensure alignment with real-world knowledge."
   authors = [
    { name = "Chun-Sung Ferng", email = "csferng@google.com" },
    { name = "Cyrus Rashtchian", email = "cyroid@google.com" },
    { name = "Da-Cheng Juan", email = "dacheng@google.com" },
    { name = "Ivan Kuznetsov", email = "ivanku@google.com" },
   ]
   license = "Apache License 2.0"
   readme = "README.md"
   [tool.poetry.dependencies]
   python = "^3.10"
   google-adk = "^1.0.0"
   google-cloud-aiplatform = { extras = [
    "adk",
    "agent-engines",
   ], version = "^1.93.0" }
   google-genai = "^1.9.0"
   pydantic = "^2.10.6"
   python-dotenv = "^1.0.1"
   [tool.poetry.group.dev]
   optional = true
   [tool.poetry.group.dev.dependencies]
   google-adk = { version = "^1.0.0", extras = ["eval"] }
   pytest = "^8.3.5"
   pytest-asyncio = "^0.26.0"
   [tool.poetry.group.deployment]
   optional = true
   [tool.poetry.group.deployment.dependencies]
   absl-py = "^2.2.1"
   **google-adk = "^1.0.0"**
   **a2a-sdk = "^0.3.0"**
   [build-system]
   requires = ["poetry-core>=2.0.0,<3.0.0"]
   build-backend = "poetry.core.masonry.api"
   2. **deployment/deploy.py**: Replace the ADK app deployment with an A2A
   agent and card.
    .filepath {
    color: #fff;
    margin: 6px;
    max-width: calc(100% - 160px); /* Give at least 160px for the "View on GitHub" button. */
    text-overflow: ellipsis;
    text-shadow: rgba(0,0,0,0.1) 1px 1px;
    overflow: hidden;
    }
    .github-docwidget-gitinclude-code .prettyprint {
    margin: 0;
    }
    .view-on-github {
    text-shadow: rgba(12,12,12,0.1) 1px 1px;
    }
   apps-script/chat/a2a-ai-agent/llm-auditor/deployment/deploy.py
   [View on GitHub](https://github.com/googleworkspace/add-ons-samples/blob/main/apps-script/chat/a2a-ai-agent/llm-auditor/deployment/deploy.py)
    Code
   # Copyright 2025 Google LLC
   #
   # Licensed under the Apache License, Version 2.0 (the "License");
   # you may not use this file except in compliance with the License.
   # You may obtain a copy of the License at
   #
   # http://www.apache.org/licenses/LICENSE-2.0
   #
   # Unless required by applicable law or agreed to in writing, software
   # distributed under the License is distributed on an "AS IS" BASIS,
   # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   # See the License for the specific language governing permissions and
   # limitations under the License.
   """Deployment script for LLM Auditor."""
   import os
   from absl import app
   from absl import flags
   from dotenv import load_dotenv
   from llm_auditor.agent import root_agent
   import vertexai
   from vertexai import agent_engines
   # A2A wrapping
   from a2a.types import AgentSkill
   from google.adk.a2a.executor.a2a_agent_executor import A2aAgentExecutor
   from google.adk.runners import InMemoryRunner
   from vertexai.preview.reasoning_engines.templates.a2a import create_agent_card
   from vertexai.preview.reasoning_engines import A2aAgent
   FLAGS = flags.FLAGS
   flags.DEFINE_string("project_id", None, "GCP project ID.")
   flags.DEFINE_string("location", None, "GCP location.")
   flags.DEFINE_string("bucket", None, "GCP bucket.")
   flags.DEFINE_string("resource_id", None, "ReasoningEngine resource ID.")
   flags.DEFINE_bool("list", False, "List all agents.")
   flags.DEFINE_bool("create", False, "Creates a new agent.")
   flags.DEFINE_bool("delete", False, "Deletes an existing agent.")
   flags.mark_bool_flags_as_mutual_exclusive(["create", "delete"])
   **def create() -> None:**
   **"""Creates an agent engine for LLM Auditor."""**
   **agent_card = create_agent_card(**
   **agent_name=root_agent.name,**
   **description=root_agent.description,**
   **skills=[AgentSkill(**
   **id='audit_llm_output',**
   **name='Audit LLM Output',**
   **description='Critiques and revises outputs from large language models.',**
   **tags=['LLM', 'Audit', 'Revision'],**
   **examples=[**
   **'The earth is flat.',**
   **'The capital of France is Berlin.',**
   **'The last winner of the Super Bowl was the New England Patriots in 2020.',**
   **],**
   **)]**
   **)**
   **a2a_agent = A2aAgent(**
   **agent_card=agent_card,**
   **agent_executor_builder=lambda: A2aAgentExecutor(**
   **runner=InMemoryRunner(**
   **app_name=root_agent.name,**
   **agent=root_agent,**
   **)**
   **)**
   **)**
   **a2a_agent.set_up()**
   **remote_agent = agent_engines.create(**
   **a2a_agent,**
   **display_name=root_agent.name,**
   **requirements=[**
   **"google-adk (>=0.0.2)",**
   **"google-cloud-aiplatform[agent_engines] (>=1.88.0,<2.0.0)",**
   **"google-genai (>=1.5.0,<2.0.0)",**
   **"pydantic (>=2.10.6,<3.0.0)",**
   **"absl-py (>=2.2.1,<3.0.0)",**
   **"a2a-sdk>=0.3.22",**
   **"uvicorn",**
   **],**
   **# In-memory runner**
   **max_instances=1,**
   **env_vars ={**
   **"NUM_WORKERS": "1"**
   **},**
   **extra_packages=["./llm_auditor"],**
   **)**
   **print(f"Created remote agent: {remote_agent.resource_name}")**
   def delete(resource_id: str) -> None:
    remote_agent = agent_engines.get(resource_id)
    remote_agent.delete(force=True)
    print(f"Deleted remote agent: {resource_id}")
   def list_agents() -> None:
    remote_agents = agent_engines.list()
    TEMPLATE = '''
   {agent.name} ("{agent.display_name}")
   - Create time: {agent.create_time}
   - Update time: {agent.update_time}
   '''
    remote_agents_string = '\n'.join(TEMPLATE.format(agent=agent) for agent in remote_agents)
    print(f"All remote agents:\n{remote_agents_string}")
   def main(argv: list[str]) -> None:
    del argv # unused
    load_dotenv()
    project_id = (
    FLAGS.project_id
    if FLAGS.project_id
    else os.getenv("GOOGLE_CLOUD_PROJECT")
    )
    location = (
    FLAGS.location if FLAGS.location else os.getenv("GOOGLE_CLOUD_LOCATION")
    )
    bucket = (
    FLAGS.bucket if FLAGS.bucket
    else os.getenv("GOOGLE_CLOUD_STORAGE_BUCKET")
    )
    print(f"PROJECT: {project_id}")
    print(f"LOCATION: {location}")
    print(f"BUCKET: {bucket}")
    if not project_id:
    print("Missing required environment variable: GOOGLE_CLOUD_PROJECT")
    return
    elif not location:
    print("Missing required environment variable: GOOGLE_CLOUD_LOCATION")
    return
    elif not bucket:
    print(
    "Missing required environment variable: GOOGLE_CLOUD_STORAGE_BUCKET"
    )
    return
    vertexai.init(
    project=project_id,
    location=location,
    staging_bucket=f"gs://{bucket}",
    )
    if FLAGS.list:
    list_agents()
    elif FLAGS.create:
    create()
    elif FLAGS.delete:
    if not FLAGS.resource_id:
    print("resource_id is required for delete")
    return
    delete(FLAGS.resource_id)
    else:
    print("Unknown command")
   if __name__ == "__main__":
    app.run(main)
5. Create a new Cloud Storage bucket dedicated to the ADK agent.
Replace the following:
   ```bash
   gcloud storage buckets create gs://CLOUD_STORAGE_BUCKET_NAME --project=PROJECT_ID --location=PROJECT_LOCATION
   ```
   1. `CLOUD_STORAGE_BUCKET_NAME` with a unique bucket name you want
   to use.
   2. `PROJECT_ID` with the ID of your Cloud project.
   3. `PROJECT_LOCATION` with the location of your
   Cloud project.
6. Set the following environment variables:
Replace the following:
   ```bash
   export GOOGLE_GENAI_USE_VERTEXAI=true
   ```
   1. `CLOUD_STORAGE_BUCKET_NAME` with the name of the bucket you
   created.
   2. `PROJECT_ID` with the ID of your Cloud project.
   3. `PROJECT_LOCATION` with the location your
   Cloud project.
7. Install and deploy ADK agent from virtual environment.
   ```bash
   python3 -m venv myenv
   ```
8. Retrieve the agent ID. You need it later, when you configure the
Chat app.
   ```bash
   python3 deployment/deploy.py --list
   ```

## Create and configure the Chat app project

1. Click the following button to open the **A2A AI Agent Quickstart**
Apps Script project.
[Open the project](https://script.google.com/d/1e8Fa-KxSSdMAKa8vAvOOg6jBrpOU_ygtAheMkktCHU4d5M_M6lJk_uy6/edit?usp=sharing)
2. Click info_outline **Overview** >  **Make a copy**.
3. In your Apps Script project,
click  **Project Settings**
> **Edit script properties** > **Add script property**
to add the following script properties:
   1. `REASONING_ENGINE_RESOURCE_NAME` with the Vertex AI agent resource name
   copied in previous steps.
   2. `SERVICE_ACCOUNT_KEY` with the JSON key from the service account
   downloaded in previous steps such as `{ ... }`.
4. Click **Save script properties**.
5. In the Google API Console, go to Menu menu
> **IAM & Admin**
> **Settings**.
[Go to IAM & Admin Settings](https://console.developers.google.com/iam-admin/settings)
6. In the **Project number** field, copy the value.
7. In your Apps Script project,
click  **Project Settings**.
8. Under **Google Cloud Platform (GCP) Project**, click **Change project**.
9. In **GCP project number**, paste the Google Cloud project number copied in
previous steps.
10. Click **Set project**. The Cloud project and
Apps Script project are now connected.

## Create a test deployment

You need a deployment ID for this Apps Script project, so that
you can use it in the next step.

To get the head deployment ID, do the following:

1. In the Chat app Apps Script project,
click **Deploy**
> **Test deployments**.
2. Under **Head deployment ID**, click
**Copy**.
3. Click **Done**.

## Configure the Chat app

Using your Apps Script deployment, follow these steps to deploy
the Google Chat app for testing:

1. In the [API Console](https://console.developers.google.com/), search for `Google Chat API`,
and click **Google Chat API**.
2. Click **Manage**.
3. Click **Configuration** and set up the Chat app:
   1. In the **App name** field, enter `A2A Quickstart`.
   2. In the **Avatar URL** field, enter
   `https://developers.google.com/workspace/add-ons/images/quickstart-app-avatar.png`.
   3. In the **Description** field, enter `A2A Quickstart`.
   4. Under **Functionality**, select **Join spaces and group conversations**.
   5. Under Connection settings, select **Apps Script project**.
   6. In the **Deployment ID** field, paste the Head deployment ID that you
   previously copied.
   7. Under Visibility, select **Specific people and groups in your
   domain**, and enter your email.
4. Click **Save**.

The Chat app is ready to respond to messages.

## Test the Chat app

To test your Chat app, open a direct message space with
the Chat app and send a message:

1. Open Google Chat using the Google Workspace account that you
 provided when you added yourself as a trusted tester.
[Go to Google Chat](https://chat.google.com)
2. Click add **New chat**.
3. In the **Add 1 or more people** field, type the name of your
 Chat app.
4. Select your Chat app from the results. A direct
 message opens.
**Note:** If you don't see your Chat app in the list of
 results, ensure that you've included your Google Workspace account in the
 **Visibility** settings of the [**Chat API Configuration**](https://developers.google.com/workspace/chat/configure-chat-api)
 page in the Google API Console.
5. In the new direct message with the app, type `The Eiffel Tower was completed in 1900` and press`enter`.
The Chat app replies with **Critic** and **Reviser** sub-agent responses.

To add trusted testers and learn more about testing interactive features, see
[Test interactive features for
Google Chat apps](https://developers.google.com/workspace/chat/test-interactive-features).

## Troubleshoot

When a Google Chat app or
 [card](https://developers.google.com/workspace/chat/create-messages#create) returns an error, the
 Chat interface surfaces a message saying "Something went wrong."
 or "Unable to process your request." Sometimes the Chat UI
 doesn't display any error message, but the Chat app or
 card produces an unexpected result; for example, a card message might not
 appear.

Although an error message might not display in the Chat UI,
 descriptive error messages and log data are available to help you fix errors
 when error logging for Chat apps is turned on. For help viewing,
 debugging, and fixing errors, see
 [Troubleshoot and fix Google Chat errors](https://developers.google.com/workspace/chat/troubleshoot).

## Clean up

To avoid incurring charges to your Google Cloud account for the
 resources used in this tutorial, we recommend that you delete the
 Cloud project.

> **Caution:** Deleting a project has the following effects:
>
> - **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
> - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.
>
> If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1. In the Google API Console, go to the **Manage resources** page. Click
 **Menu** menu
> **IAM & Admin**
> **Manage Resources**.
[Go to Resource Manager](https://console.developers.google.com/cloud-resource-manager)
2. In the project list, select the project you want to delete and then click
 **Delete** delete.
3. In the dialog, type the project ID and then click **Shut down** to delete
 the project.

## Related topics

- [Build a Google Chat app with an ADK AI agent](https://developers.google.com/workspace/add-ons/chat/quickstart-adk-agent)
- [Build a Google Chat app with a Gemini Enterprise AI agent](https://developers.google.com/workspace/add-ons/chat/quickstart-ge-agent)
- [Build a Google Chat app with an Agent2UI agent](https://developers.google.com/workspace/add-ons/chat/quickstart-a2ui-agent)
- [Build Gemini Enterprise agents that are tightly integrated with Workspace data stores, APIs, and Chat apps](https://codelabs.developers.google.com/ge-gws-agents)
- [Build Vertex AI agents that are tightly integrated with Workspace data stores, APIs, and Chat apps](https://codelabs.developers.google.com/vertexai-gws-agents)
- [Fact-check statements with an ADK AI agent and Gemini model](https://developers.google.com/apps-script/samples/custom-functions/fact-check)
- [Plan travels with an AI agent accessible across Google Workspace](https://developers.google.com/workspace/add-ons/samples/travel-concierge)
- [Integrate fundamental AI concepts in Chat apps](https://codelabs.developers.google.com/chat-apps-ai-concepts)
- [Answer questions based on Chat conversations with a Gemini AI Chat app](https://developers.google.com/workspace/add-ons/samples/tutorial-ai-knowledge-assistant)
- [Respond to incidents with Google Chat, Vertex AI, Apps Script, and user authentication](https://developers.google.com/workspace/add-ons/samples/tutorial-incident-response-user-auth)
- [Manage projects with Google Chat, Vertex AI, and Firestore](https://developers.google.com/workspace/add-ons/samples/tutorial-project-management)
