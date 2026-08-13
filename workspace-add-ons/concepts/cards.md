# Cards

A card-based Google Workspace add-on appears as a pane in the sidebar (or, on mobile, as another activity window reached through the menu). The add-on has a top toolbar that identifies the add-on and displays a card—essentially a "page" of the add-on's UI. Google Apps Script represents cards in project code using Card objects.

## Card anatomy

A card is a group of UI elements you design. A card consists of the following sections:

A card header. This identifies the cards. It has title text, and may optionally have a subtitle and an icon.

One or more card sections. These are sub-divisions of the card's UI area. A section can have a text section header. Card sections are separated from each other on the card by a horizontal rule. If a card section is particularly large, it is automatically rendered as a collapsible section that users can expand or collapse as needed. A card can have no more than 100 card sections, and should have only a few for better performance.

Each card section contains one or more UI widgets. Widgets provide the user with information or interactive controls. Cards and card sections are structural widgets, so you cannot add those to a card section. A card section can have no more than 100 widgets, and should be as concise as possible for best performance.

You should design cards around particular user activities or data sets. For example, a Google Workspace add-on that displays data taken from Google Sheets might have a separate card for each sheet it pulls data from.

## Use multiple cards

Add-ons usually consist of more than one card. You can either configure these cards as a list for basic navigation or configure more complex navigation methods to control how the user moves between the cards. For details, see basic navigation with multiple cards.

If the add-on uses basic navigation, when the add-on is first opened the Google Workspace application it extends constructs a list of the card headers and presents those to the user. Clicking on the card header opens that card. A back arrow is also provided to get back to the card header list. You don't have to code the header and back arrow functionality—this is done automatically when you define the cards in your add-on.

When designing add-ons, it's best to limit the number of cards you display at once, since cards must share a limited amount of screen space. It's also best to avoid unnecessary complexity in cards.

For performance reasons, you can't add more than 100 widgets or 100 card sections to a card.
