# Open and use installed add-ons

Google Workspace add-ons that you have installed automatically appear in the host application interface as a column of icons. Clicking an add-on icon opens the add-on interface, and clicking the icon again hides the interface. The location of the icon depends on the client (desktop or mobile).

## Start a Google Workspace add-on

Google Workspace add-ons that you have installed automatically appear in the host application interface as a column of icons (under icons for Google products like Calendar, Keep, and Tasks). The host application represents each add-on by a small icon; this icon is specified in the add-on's manifest.

Clicking an add-on icon opens the add-on interface, and clicking the icon again hides the interface. The location of the icon depends on the client (desktop or mobile).

### On desktop

An icon for each Google Workspace add-on a user has installed appears in the right-nav of the Google Workspace host application. An icon is only presented if that Google Workspace add-on has been enabled for use with that host in its manifest.

When a user clicks a Google Workspace add-on icon, a corresponding trigger fires to build the initial homepage for the add-on. Once the homepage card is constructed, the add-on returns it to the host application for display. If the add-on doesn't define a homepage, a default card is presented instead.

If you open an add-on that isn't fully authorized, it prompts you to authorize it. After you review and authorize the requested permissions, the add-on homepage appears, and you can then begin interacting with it.

You can close the add-on UI at any time by clicking the add-on icon again (or clicking the icon of a different add-on), or by clicking the close icon in the add-on header.

#### Gmail compose

Google Workspace add-ons can extend the Gmail compose UI, which provides add-on functionality from Gmail's "compose message" window. For these add-ons, the add-on icon appears in the horizontal row at the bottom of the compose window. The add-on icons are placed to the right of the standard icons for message formatting, attaching files, and so forth.

#### Calendar conference solutions

Google Workspace add-ons can add one or more conference solutions to the Google Calendar event interface. These solutions don't appear as a card interface; rather, they appear as conferencing options in Google Calendar's built-in **Edit event** interface.

Calendar represents each add-on conferencing solution by a name and a small icon, each specified by the `calendar.conferenceSolution[]` fields in the add-on's manifest.

When you select an add-on's conference solution, Calendar asks you to authorize the add-on (if you haven't already), and may ask you to further authorize the third-party conferencing system the add-on connects to. After authorizing, you can freely select any of the add-on conference solutions for your events.

### On mobile (Gmail only)

On mobile, the Google Workspace add-ons that extend Gmail have icons that appear as a horizontal row at the bottom of the open message or draft. Clicking an icon opens that interface at the bottom of the message.

For Google Workspace add-ons that extend the Gmail with compose actions, the add-on icons appear in the compose view's top-right menu.

## Start an Editor add-on

**Note:** Editor add-ons are only available on desktop clients, and not on mobile.

Most Editor add-ons create one or more menu items in the **add-ons** menu of the editor. It's a best practice to create at least one menu item for an Editor add-on to serve as the initial launch point that explains the add-on's purpose and usage. Selecting one of the add-on menu items causes some functionality of that add-on to start; often add-ons use menu items to open the main sidebar or dialog that represents the primary add-on interface.

Google Forms doesn't use the same menu bar as the other editors. Instead, you can find Forms add-on menu items by clicking the extension icon in the upper left of the Forms editor interface. Forms add-ons only extend the form editor, not the forms that are sent out to for replies.
