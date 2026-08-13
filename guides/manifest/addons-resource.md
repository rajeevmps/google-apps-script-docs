# AddOns Manifest Resource

The AddOns manifest resource defines Google Workspace add-on content and behavior. According to the documentation, "add-on manifests must include all components marked as **Required**."

## Key Components

**Top-level structure** includes:
- `common` (required): Settings applying across all host applications
- Host-specific configs: `calendar`, `chat`, `drive`, `gmail`, `docs`, `sheets`, `slides`, `meet`

## Common Section

The Common section defines general add-on settings:

- **logoUrl** (required): "The public URL of the toolbar image"
- **name** (required): "The name of the add-on shown in the toolbar"
- **openLinkUrlPrefixes** (required if displaying outbound links): "A list of HTTPS URL prefixes"
- **homepageTrigger**: Default trigger function for the add-on homepage
- **layoutProperties**: Toolbar and button color configuration
- **universalActions**: "List of universal actions always available in the add-on UI"
- **useLocaleFromApp**: Boolean to include user locale/timezone in event objects

## Layout Properties

Controls add-on appearance with two color settings:
- **primaryColor**: Toolbar color (defaults to grey #424242)
- **secondaryColor**: Default button color (defaults to primary color or blue #2196F3)

## Universal Actions

Each universal action requires a **label** and either an **openLink** URL or **runFunction** name. These provide actions "always available in the add-on UI."

Note: Host-specific configuration objects (`calendar`, `chat`, `drive`, `gmail`, `docs`, `sheets`, `slides`, `meet`) are documented in detail on their own manifest resource pages (see calendar-resource.md, drive-resource.md, gmail-resource.md, editors-resource.md, meet-resource.md, homepage-trigger-resource.md in this same folder).

Source: https://developers.google.com/apps-script/manifest/addons
