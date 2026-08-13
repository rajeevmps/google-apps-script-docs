# Manage deployments

## Page Summary

- The Apps Script API provides methods to manage script project deployments, including creating, listing, reading, modifying, and deleting them.
- You can create a new deployment by specifying the code version, manifest file, and description.
- The API allows you to list all deployments for a project, retrieve details of a specific deployment, and update existing deployments.
- Deleting a deployment using the API can break applications that depend on it.

This section provides an overview of the Google Apps Script API methods you can use to create, list, read, modify, and delete a script project's deployments.

## API method overview

### Create a deployment

**projects.deployments.create**

**Results**: Create a new deployment for a script project. You specify the code version, the manifest file, and deployment description to use. Returns a `Deployment` object, containing the deployment configuration details.

### List a project's deployments

**projects.deployments.list**

**Results**: Returns an array of `Deployment` objects, each representing one of the deployments of the script project.

### Read a deployment

**projects.deployments.get**

**Results**: Returns a `Deployment` that represents a specific deployment in a specific script project.

### Update a deployment

**projects.deployments.update**

**Results**: Changes a deployment's description, code version, or the manifest where the deployment is defined.

### Delete a deployment

**projects.deployments.delete**

**Results**: Removes a deployment.

**Warning:** Deleting a deployment causes any Google Workspace add-on, web app, or other application that makes use of that deployment to lose access to the Google Apps Script project. This usually causes them to fail. Don't delete a deployment without first updating any apps that depend on it.

Source: https://developers.google.com/apps-script/api/how-tos/manage-deployments
