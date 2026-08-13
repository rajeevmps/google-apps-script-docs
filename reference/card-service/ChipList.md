# ChipList

Holds a set of `Chip` objects that are displayed in a row.

Holds a set of `Chip` objects that are displayed in a row, wrapping to the next line to horizontal scrollable.

Available for Google Chat apps. In developer preview for Google Workspace add-ons.

```javascript
const chip = CardService.newChip();
// Finish building the text chip...

const chipList = CardService.newChipList()
                     .setLayout(CardService.ChipListLayout.WRAPPED)
                     .addChip(chip);
```

## Methods

### addChip(chip: Chip): ChipList

Adds a chip.

Parameters: `chip` (Chip) — The chip to add.

Returns: `ChipList` — This object, for chaining.

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters: `eventAction` (EventAction) — The `EventAction` to be added.

Returns: `Widget` — The Object, for chaining.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters: `id` (String) — The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

Returns: `Widget` — This object, for chaining.

### setLayout(layout: ChipListLayout): ChipList

Sets the chip list layout. If unset, it defaults to `ChipListLayout.WRAPPED` layout.

Parameters: `layout` (ChipListLayout) — The chip list layout.

Returns: `ChipList` — This object, for chaining.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters: `visibility` (Visibility) — The `Visibility` of the widget.

Returns: `Widget` — The Object, for chaining.
