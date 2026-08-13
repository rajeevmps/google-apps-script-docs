# Use the Gemini side panel in the Apps Script editor

You can use Gemini in the Apps Script editor side panel to
generate, modify, and debug code. You can also ask questions about
Apps Script.

Gemini uses the saved context from your active script project to provide relevant,
Apps Script code and explanation, minimizing the need to context-switch
between the editor and external resources.

## Licensing and setup requirements

- **Google Workspace Licenses:** You must have one of the following licenses:
    - Google Workspace Business Standard
    - Google Workspace Business Plus
    - Google Workspace Enterprise Standard
    - Google Workspace Enterprise Plus
    - Workspace Gemini Add-on licenses (e.g., Gemini Business, Gemini Enterprise)
    - Google AI Pro for Education
    - Google AI Pro
    - Google AI Ultra
- **Admin Console Settings:** The Google Workspace domain administrator must
enable Gemini or Generative AI features in the Google Admin console.
For details, see
[Turn access to Google Workspace with Gemini Beta on or off](https://knowledge.workspace.google.com/admin/generative-ai/workspace-with-gemini/turn-access-to-google-workspace-with-gemini-beta-on-or-off)
in the Workspace Admin Help Center.
- **Single-Account Profile:** The Gemini side panel might not load if you are
signed in to multiple Google Accounts simultaneously in the same browser
session. If you encounter issues, load the editor in a browser profile with
a single active Google Account or in an incognito window.

## Access the Gemini side panel

To open the Gemini side panel in the Apps Script editor:

1. Open the script editor by creating a new project (at script.new) or opening
an existing project on [script.google.com](https://script.google.com/). You
can also open the editor from container-bound documents (Google Sheets,
Docs, Slides, or Forms) by clicking **Extensions** > **Apps Script**.
2. Click the **Gemini** icon (spark)
in the right-side panel menu.
3. Type a prompt in the box at the bottom of the side panel and hit **Enter**
or click the submit arrow.

## Generate and modify code

You can ask Gemini to write new code or modify existing code using natural language prompts.

- **Generate code:** Describe the automation task you'd like to perform. For
example:
    - *"Create a custom function CONSOLIDATE_DATA that groups columns by ID,
  calculates the maximum amount, and lists unique statuses."*
    - *"Write a script that searches my Gmail inbox for unread emails with
  'URGENT' in the subject from the last 30 days and adds these in my
  Google Tasks."*
    - *"Create a custom menu in Google Sheets called 'Export to Docs' that
  exports table contents into a new Google Doc and messages the user the
  path."*
- **Modify code:** Explicitly refer to existing functions or variables in
your working file. For example:
    - *"Update the function `myFunctionName` to incorporate the variable
  `xyz`."*
    - *"Refactor the data loops in this file to be more efficient."*

When Gemini generates or modifies code, the proposed code block appears in the working file in the code editor, with **Differential
View (Diff View)** highlighting additions and removals. Click **Accept All** or
**Reject All** to confirm or discard changes.

## Debug errors

Gemini can diagnose and fix errors in your script, debugging not just obvious errors in execution logs, but also issues with performance and output.

1. Execute your function in the editor and observe the error in the execution
logs console.
2. Click **Fix with Gemini**.
Gemini uses the details of the error and the surrounding code context to
analyze the root cause (e.g. *"Cannot read property 'getValue' of null
because the cell was empty"*), prints an explanation, and inserts a proposed diff.
3. Review the proposed fix in the editor and click **Accept All** or **Reject All**.
4. Save and re-run your script to confirm the error is solved.

To address issues with performance and output, a specific prompt can be
an effective approach. For example:

- *"The script doesn't throw an error but the output is wrong. Please fix it."*
- *"The script hangs without producing output. Please fix it."*
- *"The script is extremely slow — taking over a minute to execute. Please fix it."*

## Ask conceptual questions (Ask Me Anything)

You can ask Gemini general questions about how Apps Script works:

- *"What are the security differences between a simple trigger and an
installable trigger?"*
- *"How do I authenticate with a basic external REST API using UrlFetchApp?"*
- *"How do I use the Drive API to manage file permissions?"*

Gemini returns detailed text explanations along with illustrative code snippets.
Conceptual questions don't modify code in the editor.

## Key guidelines and limitations

- **Active file context:** Gemini operates on the active file open in the Apps Script editor.
- **Access controls:** Gemini only works on script projects you own or can edit.
- **Authentication & permissions:** Once you insert and save code generated by Gemini, running the script for the first time will trigger standard Workspace OAuth permission prompts. Ensure you review the requested permissions before clicking **Allow**.
- **Accepting/rejecting changes:** You can't accept or reject a subsection of the code Gemini proposes; you must accept all of it or reject all of it.
- **Language support:** English is the only supported language.
- **Drive file grounding:** File grounding with a file picker—that is,
using @ to pick files from a list of Drive items—is unsupported. You can
still ground your prompts with file context by using @ followed directly
by the file's URL (for example, @https://docs.google.com/...).
- **Missing URLs:** Gemini occasionally omits URLs from generated code due to security sanitization. If you notice a missing link, explicitly provide the exact URL you want to use in your prompt to ensure it is included.
- **Regionalization:** Gemini in the Apps Script editor side panel does not support regionalization.
