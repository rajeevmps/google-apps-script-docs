# OpenAs

An enum that specifies how to open a URL.

An enum that specifies how to open a URL. The client can open a URL as either a full size window or an overlay. The implementation depends on the client platform capabilities, and the value selected may be ignored if the client does not support it. FULL_SIZE is supported universally.

Using OnClose may cause OpenAs to be ignored; if the client platform cannot support both selected values together, OnClose takes precedence.

To call an enum, you call its parent class, name, and property. For example, `CardService.OpenAs.FULL_SIZE`.

## Properties

### FULL_SIZE
Open in a full window or tab. Default.

### OVERLAY
Open as an overlay such as a pop-up.
