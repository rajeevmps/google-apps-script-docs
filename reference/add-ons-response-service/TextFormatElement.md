# TextFormatElement

A text format element, which can be a `TextFormatChip`, `StyledText`, `Hyperlink`, or `ListContainer`.

A text format element, which can be a `TextFormatChip`, `StyledText`, `Hyperlink`, or `ListContainer`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setHyperlink(hyperlink)

`setHyperlink(hyperlink: Hyperlink): TextFormatElement`

Sets the text format element as a `Hyperlink`.

### setListContainer(listContainer)

`setListContainer(listContainer: ListContainer): TextFormatElement`

Sets the text format element as a `ListContainer`.

### setStyledText(styledText)

`setStyledText(styledText: StyledText): TextFormatElement`

Sets the text format element as a `StyledText`.

### setText(text)

`setText(text: String): TextFormatElement`

Sets the text format element as a text string.

### setTextFormatChip(chip)

`setTextFormatChip(chip: TextFormatChip): TextFormatElement`

Sets the text format element as a `TextFormatChip`.

## Code Sample

```javascript
const sampleChip = AddOnsResponseService.newTextFormatChip()
        .setLabel("Label!");
const textFormatElement = AddOnsResponseService.newTextFormatElement()
        .setTextFormatChip(sampleChip);
```
