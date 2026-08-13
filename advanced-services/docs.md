# Advanced Docs Service

Source: https://developers.google.com/apps-script/advanced/docs

## Overview

The advanced Docs service in Apps Script enables you to leverage the Google Docs API to read, edit, and format Google Docs content. As noted in the documentation, "this advanced service provides a few extra features" beyond the built-in Docs service, though the built-in option is often simpler to use.

This requires enabling the advanced service before use and following the quickstart guide for setup instructions.

## Key Features

The service allows you to:
- Read, edit, and format Google Docs content
- Access additional capabilities beyond the built-in Docs service
- Use the same objects, methods, and parameters as the public Docs API

## Sample Code

### Create Document

```javascript
function createDocument() {
  const document = Docs.Documents.create({ title: "My New Document" });
  console.log(`Created document with ID: ${document.documentId}`);
  return document.documentId;
}
```

### Find and Replace Text

```javascript
function findAndReplace(documentId, findTextToReplacementMap) {
  const requests = [];
  for (const findText in findTextToReplacementMap) {
    const replaceText = findTextToReplacementMap[findText];
    const replaceAllTextRequest = {
      replaceAllText: {
        containsText: {
          text: findText,
          matchCase: true,
        },
        replaceText: replaceText,
      },
    };
    requests.push(replaceAllTextRequest);
  }
  const response = Docs.Documents.batchUpdate(
    { requests: requests },
    documentId,
  );
  const replies = response.replies;
  for (const [index] of replies.entries()) {
    const numReplacements =
      replies[index].replaceAllText.occurrencesChanged || 0;
    console.log(
      "Request %s performed %s replacements.",
      index,
      numReplacements,
    );
  }
  return replies;
}
```

### Insert and Style Text

```javascript
function insertAndStyleText(documentId, text) {
  const requests = [
    {
      insertText: {
        location: {
          index: 1,
        },
        text: text,
      },
    },
    {
      updateTextStyle: {
        range: {
          startIndex: 1,
          endIndex: text.length + 1,
        },
        textStyle: {
          fontSize: {
            magnitude: 12,
            unit: "PT",
          },
          weightedFontFamily: {
            fontFamily: "Calibri",
          },
        },
        fields: "weightedFontFamily, fontSize",
      },
    },
  ];
  const response = Docs.Documents.batchUpdate(
    { requests: requests },
    documentId,
  );
  return response.replies;
}
```

### Read First Paragraph

```javascript
function readFirstParagraph(documentId) {
  const document = Docs.Documents.get(documentId, {
    includeTabsContent: true,
  });
  const firstTab = document.tabs[0];
  const bodyElements = firstTab.documentTab.body.content;
  for (let i = 0; i < bodyElements.length; i++) {
    const structuralElement = bodyElements[i];
    if (structuralElement.paragraph) {
      const paragraphElements = structuralElement.paragraph.elements;
      let paragraphText = "";
      for (let j = 0; j < paragraphElements.length; j++) {
        const paragraphElement = paragraphElements[j];
        if (paragraphElement.textRun !== null) {
          paragraphText += paragraphElement.textRun.content;
        }
      }
      console.log(paragraphText);
      return paragraphText;
    }
  }
}
```

## Best Practices

**Batch Updates:** Combine multiple requests in a single `batchUpdate` call rather than looping through multiple calls. "A best practice when using the advanced Docs service is to combine multiple update requests into a single `batchUpdate` call for efficiency."

### Recommended Approach

```javascript
var requests = [];
var textToReplace = ['foo', 'bar'];
for (var i = 0; i < textToReplace.length; i++) {
  requests.push({ replaceAllText: ... });
}

Docs.Documents.batchUpdate({
  requests: requests
}, docId);
```

## References

- Full API reference: [Docs API Reference Documentation](https://developers.google.com/docs/api/reference/rest) (external — not scraped)
- Support: [Docs API Support Guide](https://developers.google.com/docs/api/support) (external — not scraped)
</content>
