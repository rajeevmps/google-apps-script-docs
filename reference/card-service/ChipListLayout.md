# ChipListLayout

An enum that specifies the layout of a ChipList.

An enum that specifies the layout of a ChipList. WRAPPED is the default; chips wrap to the next line if there isn't enough horizontal space. HORIZONTAL_SCROLLABLE chips scroll horizontally if they don't fit in the available space.

To call an enum, you call its parent class, name, and property. For example, `CardService.ChipListLayout.WRAPPED`.

## Properties

### WRAPPED
The chip list wraps to the next line if there isn't enough horizontal space. Default.

### HORIZONTAL_SCROLLABLE
The chips scroll horizontally if they don't fit in the available space.
