# Manage projects

## Page Summary

- "The Apps Script API allows you to create, read, modify, and monitor your Apps Script projects."
- "The `projects.create` method creates a new Apps Script project, which can be a standalone script or a bound script associated with a Google Drive file."
- "The `projects.get` method retrieves project metadata, while `projects.getContent` retrieves the project's source code and manifest."
- "The `projects.updateContent` method allows you to change the files within a script project, replacing existing content."
- "The `projects.getMetrics` method provides metrics about a project, such as user count and execution errors, which can be filtered by deployment, function, or time interval."

This section provides an overview of the Google Apps Script API methods you can use to create, read, modify, and monitor your Google Apps Script projects. The [Project Management](https://developers.google.com/apps-script/api/samples/manage) samples page shows examples of API management requests. The reference documentation for each method provides implementation details.

## API method overview

### Create projects

**[projects.create](https://developers.google.com/apps-script/api/reference/rest/v1/projects/create)**

**Results**: Create a basic, empty project with no project files and a default [project manifest](https://developers.google.com/apps-script/concepts/manifests).

**Options**: You can provide a project title. You can also create a [bound script](https://developers.google.com/apps-script/guides/bound) by providing the Google Drive ID of a Google Docs, Google Sheets, Google Forms, or Google Slides file to act as the script's parent.

### Read project metadata

**[projects.get](https://developers.google.com/apps-script/api/reference/rest/v1/projects/get)**

**Results**: Retrieves a [`Project`](https://developers.google.com/apps-script/api/reference/rest/v1/projects#Project) object, which represents project metadata. This data includes the project title, script ID, creating user, creation time, and other details.

### Read project content

**[projects.getContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent)**

**Results**: Returns an array of [`File`](https://developers.google.com/apps-script/api/reference/rest/v1/File) objects, one for each code and HTML file in the project. The list also includes the [project manifest](https://developers.google.com/apps-script/concepts/manifests) as a JSON file. File objects contain the source content of the file (`File.source`) and other metadata, such as a list of functions in the file (`File.functionSet`).

**Options**: You can specify which [version](https://developers.google.com/apps-script/guides/versions) of the content to retrieve with a query parameter.

### Update project content

**[projects.updateContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/updateContent)**

**Results**: Changes the file content in a script project. You provide the new content as an array of [`File`](https://developers.google.com/apps-script/api/reference/rest/v1/File) objects. One of these `File` objects must have JSON type and represent the script project's new [project manifest](https://developers.google.com/apps-script/concepts/manifests). The new content is stored as the HEAD version of the project. It is used when the script executes as a trigger, in the script editor, in Google Workspace add-on preview mode, or as a web app or Apps Script API in development mode.

**Note**: To update script project content, first issue a [projects.getContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent) request to retrieve an array of the existing `File`s, make the intended changes to those objects, then use the `File`s as input for a [projects.updateContent](https://developers.google.com/apps-script/api/reference/rest/v1/projects/updateContent) request.

**Warning:** The new content replaces all existing files in the script project. Files not updated by the request are removed.

### Read project metrics

**[projects.getMetrics](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics)**

**Results**: Read certain metrics about a project. These metrics include the number of users, the total number of executions, the total number of execution errors, and other details. Use a [MetricType](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics#metrictype) to specify the information you are requesting.

**Options**: Restrict the results to specific deployments or script functions using a [MetricsFilter](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics#MetricsFilter). You can also define a specific metric interval using a [MetricsIntervalConfig](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getMetrics#metricsintervalconfig).

Source: https://developers.google.com/apps-script/api/how-tos/manage-projects
