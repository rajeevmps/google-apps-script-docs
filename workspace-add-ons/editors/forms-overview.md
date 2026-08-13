# Extend Google Forms with add-ons

## Page Summary

- Google Forms is a cloud-based solution for creating and sharing questionnaires, surveys, and quizzes, offering real-time collaboration and customization features.

- Forms add-ons enhance the form creation process by enabling connections to other systems, extending functionality, and integrating with Google Workspace apps.

- Developers can leverage Apps Script's Forms service to programmatically control form behavior, access responses, and modify form elements.

- Google Forms supports a variety of question types, including text-based, multiple-choice, grid, and date/time options, as well as static elements like images and videos.

- Forms can be designated as quizzes, allowing for assigning points, providing feedback, and enabling automated grading.

## Main Content

[Google Forms](https://workspace.google.com/products/forms/) is a cloud-based questionnaire and survey solution with real-time collaboration and powerful tools to customize form questions. Forms can also be used to create online quizzes.

You can extend Forms with add-ons that help users construct new surveys, establish connectivity to third-party systems, and integrate your Forms data with other Google Workspace applications (like Google Sheets).

You can see the Forms add-ons others have built on the [Google Workspace Marketplace](https://workspace.google.com/marketplace/category/works-with-form).

**Note:** "Forms add-ons only extend the Forms editor itself, where the forms are constructed. Forms add-ons can't extend the form that is presented to potential respondents."

### What you can do

Here are a few things you can do with add-ons that extend Forms:

- Create, access, and edit Forms using the built-in Apps Script Forms service. The Spreadsheet service lets you access the Google Sheets where form responses are stored.
- Control form behavior from an add-on using the Forms service. For example, determine whether the form is accepting responses or sends a confirmation message to respondents.
- Create custom menus and define multiple custom dialogs and sidebars interfaces using standard HTML and CSS. These UI components extend the Google Forms editor, not the form that respondents see.
- Use add-on triggers to run specified functions when certain triggering events occur. For example, form-submit installable triggers let your add-on react whenever someone submits a form response.

### Form structure

A Google form is composed of a title, description, and a list of form questions. Optionally, a Form can have an associated Google Sheet where the form responses are collected.

Each form question has a type indicating the kind of information it is asking the respondent for, or a static form element (like an image or video). Each type is represented by an object in the Apps Script Forms service. Forms add-ons can use this service to add, modify, rearrange, or remove these form elements:

#### Question types
- Short answer text
- Paragraph text
- Multiple choice
- Checkboxes
- Dropdown select menus (lists)
- Linear scale
- Multiple choice grid
- Checkbox grid
- Date
- Duration
- Date-time
- Time

#### Static types
- Image
- Page break
- Section header
- Video

### Quizzes

Forms can also act as quizzes. If you designate a form as a quiz, you can assign point values and feedback to each form question. Point values enable customized grading of the quiz. Feedback, represented by the `QuizFeedback` class in the Forms service, is text and links that are presented to the respondent after answering the associated form question.

### Triggers

Apps Script **triggers** let a script project execute a specified function when certain conditions are met, such as when a form is submitted or when an add-on is installed.

See add-on triggers for more information on what triggers can be used with Forms add-ons and what restrictions apply to their use.
