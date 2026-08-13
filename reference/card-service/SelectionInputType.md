# SelectionInputType

The format of the items that users can select.

The format of the items that users can select. Different options support different types of interactions. For example, users can select multiple checkboxes, but can only select one item from a dropdown menu.

Each selection input supports one type of selection. Mixing checkboxes and switches, for example, isn't supported.

Available for Google Chat apps and Google Workspace add-ons.

To call an enum, you call its parent class, name, and property. For example, `CardService.SelectionInputType.CHECK_BOX`.

## Properties

### CHECK_BOX
Checkbox input style. Default.

### RADIO_BUTTON
Radio button input style. At most one item in the group can be selected.

### DROPDOWN
Dropdown menu selection input style.

### SWITCH
A set of switches. Users can turn on one or more switches.

### MULTI_SELECT
A multiselect menu for static or dynamic data.

### OVERFLOW_MENU
A UI element that houses additional options that don't fit within the primary interface
