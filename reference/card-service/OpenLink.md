# OpenLink

Represents an action to open a link with some options.

Represents an action to open a link with some options. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setOnClose(onClose: OnClose): OpenLink

Sets the behavior of the URL action when the URL window or tab is closed.

### setOpenAs(openAs: OpenAs): OpenLink

Sets the behavior of URL when it is opened.

### setUrl(url: String): OpenLink

Sets the URL to be opened. The URL must match a prefix in the manifest allowlist.

```javascript
// A button that opens as a link in an overlay and
// requires a reload when closed.
const button = CardService.newTextButton()
                   .setText('This button opens a link in an overlay window')
                   .setOpenLink(
                       CardService.newOpenLink()
                           .setUrl('https://www.google.com')
                           .setOpenAs(CardService.OpenAs.OVERLAY)
                           .setOnClose(CardService.OnClose.RELOAD_ADD_ON),
                   );

// An action response that opens a link in full screen and
// requires no action when closed.
const actionResponse = CardService.newActionResponseBuilder()
                           .setOpenLink(
                               CardService.newOpenLink()
                                   .setUrl('https://www.google.com')
                                   .setOpenAs(CardService.OpenAs.FULL_SIZE)
                                   .setOnClose(CardService.OnClose.NOTHING),
                               )
                           .build();
```

Note: To reload add-ons after closing a link, avoid links with Cross-Origin-Opener-Policy headers enabled, as add-ons cannot detect window state or update properly.
