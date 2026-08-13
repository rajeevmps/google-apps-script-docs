# Provide conference solution logos

Note: This functionality was built for conference providers specifically, and was originally available as Calendar conferencing add-ons.

In your Google Workspace add-on manifest, you can specify a distinct `conferenceSolution[].logoUrl` for each conference solution your add-on defines. These `conferenceSolution[].logoUrl` images are used in the Google Calendar user interface to identify the conference solution.

Since these `logoUrl` images are used within Calendar directly, the images must be present on Google's infrastructure. Specifically, use the same icon that you use for the add-on's Google Workspace Marketplace store listing.

To obtain an image URL that can be used as the `conferenceSolution[].logoUrl`:

1. Open the Google Cloud console.
2. If necessary, switch to the project hosting your add-on.
3. At the top-left, click Menu menu > APIs & Services.
4. In the list at the bottom, click Google Workspace Marketplace SDK.
5. Select the Store Listing tab.
6. In the Graphics Assets section, upload the intended attachment icon image as an Application Icon 32x32.
7. Copy the resulting image URL and use it as the `attachment.iconUrl`.
