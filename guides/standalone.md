# Standalone Scripts

[Video](https://www.youtube.com/watch?v=BK9sWR0I6Ys)

A standalone script is any script that is not
[bound to a Google Sheets, Google Docs, Google Slides, or
Google Forms file](https://developers.google.com/apps-script/guides/bound). These scripts appear
among your files in Google Drive.

## Create a standalone script

To create a standalone script, visit
[`script.google.com`](https://script.google.com)
and click **New project**.

You can also create standalone scripts from Google Drive. Go to [Google Drive](https://drive.google.com)
and click **New \> More \> Google Apps Script**.

## Run a standalone script

From the script editor, select the name of the function to execute and
click **Run**.

## Use a standalone script

Standalone scripts are often utility scripts, such as a script that
[searches Drive for files named "untitled"](https://developers.google.com/apps-script/reference/drive/drive-app#searchFiles(String))
so you can delete them.

A standalone script can also be deployed as a [web app](https://developers.google.com/apps-script/guides/web)
or set up to run automatically from an
[installable trigger](https://developers.google.com/apps-script/guides/triggers/installable).

Apps Script standalone scripts are suitable for lightweight
add-on development for you, your team, or your
organization. For larger projects, consider building a
Google Workspace add-on on a
[different runtime](https://developers.google.com/workspace/add-ons/guides/alternate-runtimes) environment.