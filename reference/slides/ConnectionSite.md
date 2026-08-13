# ConnectionSite

A point on a PageElement that can connect to a connector.

The ConnectionSite class represents a point on a PageElement that can connect to a connector. It provides access to connection sites on page elements within Google Slides presentations.

## Methods

### getIndex()

`Integer`

Returns the index of the connection site. The index is unique among all the connection sites on the same page element. In most cases, it corresponds to the predefined connection site index from the ECMA-376 standard.

**Returns**

`Integer` — the index of the connection site

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPageElement()

`PageElement`

Returns the `PageElement` that the connection site is on.

**Returns**

`PageElement` — the page element that the connection site is on

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
