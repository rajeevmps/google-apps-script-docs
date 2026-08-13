# CollapseControl

A customizable collapse and expand control.

A customizable collapse and expand control. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

```javascript
const collapseButton = CardService.newTextButton()
    .setTextButtonStyle(CardService.TextButtonStyle.BORDERLESS)
    .setText('Collapse');

const expandButton = CardService.newImageButton()
    .setImageButtonStyle(CardService.ImageButtonStyle.FILLED);

const collapseControl = CardService.newCollapseControl()
    .setHorizontalAlign(CardService.HorizontalAlignment.END)
    .setExpandButton(expandButton)
    .setCollapseButton(collapseButton);
```

## Methods

### setCollapseButton(button: Button): CollapseControl

Sets the Button that is displayed for "show less" button. Optional. Must be set together with collapse button.

### setExpandButton(button: Button): CollapseControl

Sets the Button that is displayed for "show more" button. Optional. Must be set together with collapse button.

### setHorizontalAlign(horizontalAlignment: HorizontalAlignment): CollapseControl

Sets the HorizontalAlignment of the CollapseControl. Optional.
