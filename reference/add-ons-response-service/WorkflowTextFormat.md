# WorkflowTextFormat

A block of text with rich formatting options.

A block of text with rich formatting options including styles, hyperlinks, and interactive elements defined in `TextFormatElement`. A WorkflowTextFormat can contain one or more `TextFormatElement`s.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addTextFormatElement(textFormatElement)

`addTextFormatElement(textFormatElement: TextFormatElement): WorkflowTextFormat`

Adds a `TextFormatElement` to the workflow text format.

**Parameters**
- `textFormatElement` (TextFormatElement) — The text format element to be added.

**Returns**
- `WorkflowTextFormat` — This workflow text format object, for chaining.

## Code Sample

```javascript
const workflowTextFormat = AddOnsResponseService.newWorkflowTextFormat()
  .addTextFormatElement(
    AddOnsResponseService.newTextFormatElement()
      .setText("example_text")
  );
```
