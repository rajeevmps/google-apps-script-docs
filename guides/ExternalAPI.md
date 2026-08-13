# External APIs

Google Apps Script can interact with APIs from all over the web. Use this
guide to work with different types of APIs in your scripts.

## Connect to public APIs

Use the [`UrlFetch`](https://developers.google.com/apps-script/reference/url-fetch) service to make API
requests directly.

The following example uses the
[GitHub API](https://developer.github.com/v3/search/#search-repositories) to
search for repositories with 100 or more stars that mention
"Apps Script". This API request does not require authorization or
an API key.

    var query = '"Apps Script" stars:">=100"';
    var url = 'https://api.github.com/search/repositories'
      + '?sort=stars'
      + '&q=' + encodeURIComponent(query);

    var response = UrlFetchApp.fetch(url, {'muteHttpExceptions': true});
    Logger.log(response);

## Make requests to services with OAuth

APIs that act on behalf of a user usually require authorization, often using the
[OAuth protocol](http://oauth.net/). Apps Script doesn't provide
built-in support for the protocol, but there are open source libraries you can
use to perform the OAuth flow and send the credentials with your requests:

- [OAuth1 for Apps Script](https://github.com/googlesamples/apps-script-oauth1): Compatible with OAuth 1.0 and 1.0a.
- [OAuth2 for Apps Script](https://github.com/googlesamples/apps-script-oauth2): Compatible with OAuth2.

## Authenticate using a service account

To call an API from Apps Script, you might choose to use
service account authentication for any of the following reasons:

- Better performance with Google Cloud APIs
- Automations and long-running tasks
- Improved security (least privilege)
- Centralized access management

To use a service account in Apps Script, see
[Authenticate as an Apps Script project using service accounts](https://developers.google.com/apps-script/guides/service-account).

## Connect to Google Cloud services

You can use the [`ScriptApp.getIdentityToken()`](https://developers.google.com/apps-script/reference/script/script-app#getidentitytoken)
method to get an
[OpenID Connect](https://developers.google.com/identity/openid-connect/openid-connect)
identity token (a [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token)
or JWT) for the effective user. You can use this token to authenticate
with Google Cloud services, such as Cloud Run, that are configured to
accept it.

For more information, see [Connect to Google Cloud services](https://developers.google.com/apps-script/guides/services/cloud-run).

## Work with JSON

Working with JSON objects is similar to working with XML, except that parsing or
encoding a JSON object is much easier.

When an API returns a raw JSON response, access the JSON string response using
the method
[`HTTPResponse.getContentText`](https://developers.google.com/apps-script/reference/url-fetch/http-response#getContentText()).
After you retrieve the string, use `JSON.parse()` to parse it into a JavaScript
object.

    // Make request to API and get response before this point.
    var json = response.getContentText();
    var data = JSON.parse(json);
    Logger.log(data.title);

Similarly, to convert a JavaScript object into a JSON string for a request
payload, use `JSON.stringify()`.

    var data = {
      'entry': {
        'group': {
          'title': 'Dog Skateboarding',
          'description': 'My dog gets some serious air'
        },
        'keywords': 'dog, skateboard'
      }
    }
    var payload = JSON.stringify(data);
    // Make request to API with payload after this point.

## Parse XML

If an external API returns a raw XML response for a request, access the
XML response using the method
[`HTTPResponse.getContentText()`](https://developers.google.com/apps-script/reference/url-fetch/http-response#getContentText()).

    // Make request to API and get response before this point.
    var xml = response.getContentText();
    var doc = XmlService.parse(xml);

When making XML requests to an API, use the
[`XmlService`](https://developers.google.com/apps-script/reference/xml-service/xml-service) methods to
construct the XML to send.

    var root = XmlService.createElement('entry')
        .setAttribute('keywords', 'dog, skateboard');
    var group = XmlService.createElement('group')
        .setAttribute('title', 'Dog Skateboarding')
        .setAttribute('description', 'My dog gets some serious air');
    root.addContent(group);
    var document = XmlService.createDocument(root);
    var payload = XmlService.getPrettyFormat().format(document);
    // Make request to API with payload after this point.