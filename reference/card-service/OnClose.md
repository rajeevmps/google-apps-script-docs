# OnClose

An enum that specifies what to do when a URL opened through an OpenLink is closed.

An enum that specifies what to do when a URL opened through an OpenLink is closed. When a link is opened, the client either forgets about it or waits until the window is closed, depending on client platform capabilities.

OnClose may cause OpenAs to be ignored; if the client platform cannot support both selected values together, OnClose takes precedence.

To call an enum, you call its parent class, name, and property. For example, `CardService.OnClose.RELOAD`.

## Properties

### NOTHING
Do nothing on close. Default.

### RELOAD
Reloads the add-on on when the window closes.

If OpenAs.OVERLAY is also set, then the main card is blocked until the overlay window is closed and the add-on has finished reloading.

### RELOAD_ADD_ON
DEPRECATED. Reload the add-on on closing the URL. This action differs from RELOAD in that it does not block the main card while showing an OpenAs.OVERLAY window.
