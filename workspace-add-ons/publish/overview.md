# Publish an add-on

- Before publishing, determine your add-on's target audience and choose between public or private visibility, bearing in mind this choice is permanent.
- Ensure your add-on meets all publication requirements, has proper collaborator access, and undergoes thorough testing before publishing.
- Create a version of your add-on and record its version number or deployment ID for configuration during the publishing process.
- Set up a standard Google Cloud project and link it to your Apps Script project, as the default project cannot be used for publishing.
- Publish your add-on through the Google Workspace Marketplace once all the preparatory steps are completed.

## Before you publish

Before you start the publication process, determine your goal and review the requirements.

### Determine your audience

To let any user find and install your add-on, publish it *publicly*. When you publish publicly, the Google team reviews your add-on before it's published on Google Workspace Marketplace.

To limit your add-on to users in a specific domain, publish it *privately*. When you publish privately, the Google team doesn't review the add-on before it's published.

If you build your add-on in Apps Script, align it with the intended use for lightweight add-ons. If your add-on is designed for many users or requires high resources and scalability, consider a [different runtime](/workspace/add-ons/guides/alternate-runtimes).

**Warning:** After you save your visibility option during publication, you can't change it.

### Review the publication requirements

Review the publication requirements for your add-on type and verify that it satisfies them. See [Areas of review](/workspace/marketplace/about-app-review).

**Note:** Even if you publish privately, meet the publishing requirements to provide an optimal experience for your users.

### Verify collaborator access

The Apps Script project for your add-on belongs to either a user account or a [shared drive](/apps-script/guides/collaborating#collaborating_with_shared_drives). To publish, a script collaborator must be the publisher, which includes creating a standard Google Cloud project.

To publish, you must have edit access to the script project. If you aren't the project owner, your account must be in the same domain as the owner.

To verify collaborator access, see the overview for [Building Google Workspace add-ons](/workspace/add-ons/how-tos/building-workspace-addons#set-up-projects).

## Test your add-on

Verify that your add-on is fully functional and not a work in progress.

For testing, install unpublished add-ons (also called Developer add-ons). Share unpublished add-ons with others by sharing the project.

- For Google Workspace add-ons, see [Test Google Workspace add-ons](/workspace/add-ons/how-tos/testing-workspace-addons).
- For Editor add-ons, see [Test Editor add-ons](/workspace/add-ons/how-tos/testing-editor-addons).

## Create a version

[Create a version](/apps-script/guides/versions#creating_a_version) and record the version number. A version is a snapshot of code that the published add-on uses.

- **If you publish an Editor add-on**, use the version number when you configure the Google Workspace Marketplace SDK.
- **If you publish a Google Workspace add-on**, use the deployment ID of the version to publish.

If your add-on uses a library, create and use a version of the library project. See [Libraries](/apps-script/guides/libraries).

## Create a standard Google Cloud project

When you build your add-on in Apps Script, a default Google Cloud project is automatically created. You can't use the default Google Cloud project to publish. Instead, follow these steps to create a standard Google Cloud project:

1. Open the [Google Cloud console projects list](https://console.developers.google.com/project).
2. Select **Create Project**.
3. Fill out the project information for your add-on.
4. Select **Create**.

After you create your standard Google Cloud project, [switch your Apps Script project to it](/apps-script/guides/cloud-platform-projects#switching_to_a_different_standard_gcp_project).

## Publish your add-on

When ready to publish, follow the steps to publish an app in the Google Workspace Marketplace. See [How to publish](/workspace/marketplace/how-to-publish).
