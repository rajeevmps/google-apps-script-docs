# HtmlOutputMetaTag

An object that represents a meta tag added to the page.

An object that represents a meta tag added to the page by calling `HtmlOutput.addMetaTag(name, content)`.

## Methods

### getContent()

Returns: `String` — the content of this meta tag

Gets the content of this meta tag.

### getName()

Returns: `String` — the name of this meta tag

Gets the name of this `HtmlOutputMetaTag`.

```javascript
const output = HtmlService.createHtmlOutput('<b>Hello, world!</b>');
output.addMetaTag('viewport', 'width=device-width, initial-scale=1');

const tags = output.getMetaTags();
Logger.log(
    '<meta name="%s" content="%s"/>',
    tags[0].getName(),
    tags[0].getContent(),
);
```

## Properties

None.
