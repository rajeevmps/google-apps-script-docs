# Test an Editor add-on

Thoroughly test add-ons before you publish them to ensure they behave as intended. Apps Script lets you test Editor add-ons in development on specific Google Docs Sheets Forms, or Slides files. Use testing to:

*   Verify that an add-on in a standalone script functions as intended when applied to a sheet, doc, presentation, or form.
*   Verify that the add-on installation flow works as intended, particularly for different initial authorization lifecycle states (installed, enabled, or both).
*   Verify that the add-on functions as intended when acting on a particular document and its contents.
*   Test and compare the current and previous versions of the add-on.

## Create a test deployment

A test deployment is the combination of an add-on and a test document. After you develop a script version and want to test it as an add-on, follow these steps:

1.  If you don't have one already, create a spreadsheet, document, presentation, or form to test the add-on with.
2.  Open the script project containing your add-on.
3.  Select **Deploy** > **Test deployments**.
4.  Next to **Select type**, select **Enable deployment types** settings and select **Editor add-on**.
5.  Select **Create new test** or **Add test**.
6.  Choose a code version or select **Latest Code**.
7.  In the **Config** section, select the initial authorization state for the test.
8.  Under **Test document**, select **No document selected**. Select the Sheets, Docs, Slides, or Forms file you want to use to test the add-on and select **Insert**.
9.  Select **Save test**.

All saved test deployments appear in the **Test deployments** dialog. You can revisit the same test deployment later.

## Run a test deployment

To run a saved test deployment, follow these steps:

1.  Open the script project containing your add-on.
2.  Select **Deploy** > **Test deployments**.
3.  Under **Saved Tests**, select the radio button next to the saved test deployment you want to run and select **Execute**.

The test document opens in a new tab. The add-on is in the authorization state specified in the test deployment. Verify that the add-on functions as intended by interacting with its menu and UI elements.

To test the granular OAuth feature on your add-on, ensure that your project doesn't have authorizations. To invalidate any existing authorizations, use ScriptApp.invalidateAuth.

### Test details

Keep the following in mind when you test Editor add-ons:

*   Installable triggers aren't supported. Functionality that depends on installable triggers isn't testable.
*   When you run a test deployment set to test with the latest code, you can see changes saved to the script by refreshing the test document.
*   The test document has a URL that you can share with editors of the original test document. This lets you collaborate with others during testing and development.
*   If your add-on uses the Properties service, properties persist and remain available the next time you run the test deployment.
*   Any test deployment that uses the same combination of add-on and test document has access to the same property information. For example, if you create two test deployments, the properties saved while running the first are available when you run the second and the other way around, if the deployments use the same script and test document.
*   If you run a test deployment, you might be prompted for authorization. Authorizing a script during testing also authorizes the script outside of testing.
