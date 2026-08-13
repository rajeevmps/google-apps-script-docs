# UI style guide for Google Workspace add-ons

Google Workspace add-ons should be consistent with the style and layout of the host application they extend. They should extend the UI naturally by using familiar controls and behaviors. The guidelines presented here describe ways of handling text, images, controls, and branding that promote a high-quality user experience.

If your add-on opens separate web pages that are an integral part of the add-on's operation (such as a settings page for the add-on), make sure those web pages also follow these style guidelines.

## Text and images

This section tells you how to use text and images in your add-on.

### Add-on name

You must set your add-on's name in its project manifest and when you configure your add-on for publication. The name appears in many places, such as the Google Workspace Marketplace listing and within menus. When choosing a name:

- Use title case.
- Avoid punctuation, especially parentheses, unless part of your brand.
- Keep it short—15 or fewer characters is best. Long names may be automatically truncated in the Google Workspace Marketplace listing and elsewhere.
- Don't include the words "Google", "Gmail", or other Google product names in your add-on name.
- Don't include the word "add-on" in your add-on name.
- Leave out version information.

### Writing style

You shouldn't need to write much. Most actions should be made clear through iconography, layout, and short labels. If you find a portion of your add-on needs more extensive explanation than short labels can provide, it's a best practice to create a separate web page describing your add-on and link to it.

When writing UI text:

- Use sentence case (especially for buttons, labels, and card actions).
- Prefer short, clear text without jargon or acronyms.

### Universal and card actions

If you use universal actions or card actions in your add-on, they appear as menu items in the cards you define. You can choose the text that is used in these menus for these actions. When choosing the text to use:

- Avoid menu text that repeats your add-on's name.
- Start each menu item with an action word such as "Run", "Configure", or "Create".
- Describe the task, not the UI component that the action displays.
- If your action begins a workflow and there's no single verb that describes what it does, call it "Start".
- Keep the number of menu items small to avoid forcing the user to scroll through a large list. If you have more actions to implement, consider using multiple cards with different actions on each.

### Error messages

When something goes wrong, it's important to use plain language. Explain the problem from the user's standpoint, and suggest how to fix it.

- Don't let the user see any exceptions your code throws. Instead, use `try...catch` statements to intercept exceptions, then display a user-friendly error message.
- Before you publish, check that your add-on doesn't display debug information in the UI.

### Help content

You might want or need to design cards that display help information or explain the operation of the add-on to the user. If you do build help content for your add-on, remember to:

- When possible, show instructions in a bulleted or numbered list. Walk users through to the end result, with clear references to named UI elements.
- Make sure your instructions clearly explain any requirements, like setting up a spreadsheet in a certain way.
- Feel free to link to external help content, such as supporting web pages.

### Images

Images used in your add-on are either one of the built-in icon types or a publicly hosted image specified by a URL. When using hosted images, be sure that they are accessible by everyone who may use your add-on.

## Controls

This section provide user experience guidelines for interactive widgets.

### Buttons

Use buttons to control your user interface's main actions rather than other widgets.

- Most text button labels should start with a verb.
- Button rows should be limited to three or fewer buttons in most cases.

### DecoratedText

DecoratedText widgets let you present text content with icons, buttons or switches.

- Use sentence case for the text content.
- The text of a DecoratedText widget is truncated if it cannot fit into the available space. For this reason, always try to keep the text content as short as you can.

### Selection inputs

You can use a variety of selection input widgets in your add-on: drop-down selection boxes, checkboxes, and radio buttons.

- Use checkboxes when people can select multiple options, or no option at all. Use radio buttons (or a select menu) when exactly one option must be selected. Use dropdowns when providing a short list of alternatives while trying to save space in the UI.
- Use sentence case for the text that is assigned to each option.
- Avoid using selection changes to trigger major, hard-to-reverse actions, because people often make mistakes when making selections. Instead, consider adding a button that reads the current selection values and then triggers the action.
- For dropdowns, sort the options alphabetically or by a logical scheme that all users can understand (such as presenting the days of the week in order, starting from Sunday or Monday).
- Restrict the number of options in a given selection input widget to a reasonable number. If there are too many options, users may find it hard to use the widget. In those cases, consider breaking the option into different categories and multiple widgets.

### Text inputs

Text inputs provide a place for users to enter string data.

- Don't use a text input to make the user type one of a specific set of possible entries. Use a drop-down select instead.
- Use hints and suggestions to help the user enter text with the correct format and content.
- Use multiline text inputs if the text to be entered is more than a few words.

## Branding

This section provide user experience guidelines for adding branding elements to your add-on interface.

### In your add-on

If you'd like to include branding in your add-on UI, keep it brief and light. This helps people focus on your add-on functionality.

- All aspects of your add-on must follow the branding guidelines.
- Don't include the word "Google", "Gmail", or other Google product names.
- Don't include Google product icons, even if they are altered.
- Don't include the word "add-on" in your branding text.
- Branding text should be no more than a few words.

### In the Google Workspace Marketplace

When you configure your add-on for publication, you provide a number of graphical and text assets to build the Google Workspace Marketplace listing.

All aspects of your store listing and these assets must follow the branding guidelines.
