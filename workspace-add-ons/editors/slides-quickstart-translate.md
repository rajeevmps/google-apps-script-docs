# Translate text from Google Slides

This quickstart creates a Google Slides Editor add-on that translates selected text in a presentation.

## Objectives

- Set up the script.
- Run the script.

## Prerequisites

To use this sample, you need the following prerequisites:

- A Google Account (Google Workspace accounts might require administrator approval).
- A web browser with access to the internet.

## Set up the script

1. Create a Slides presentation at [slides.new](https://docs.google.com/presentation/create).
2. Click **Extensions** > **Apps Script**.
3. Click **Untitled project**.
4. Rename the Apps Script project to **Translate Slides** and click **Rename**.
5. Next to the `Code.gs` file, click More more_vert > **Rename**. Name the file `translate`.
6. Click Add a file add > **HTML**. Name the file `sidebar`.
7. Replace the contents of each file with the following corresponding code, then click Save .

### translate.gs

```
/**
 * @OnlyCurrentDoc Limits the script to only accessing the current presentation.
 */

/**
 * Create a open translate menu item.
 * @param {Event} event The open event.
 */
function onOpen(event) {
  SlidesApp.getUi()
    .createAddonMenu()
    .addItem("Open Translate", "showSidebar")
    .addToUi();
}

/**
 * Open the Add-on upon install.
 * @param {Event} event The install event.
 */
function onInstall(event) {
  onOpen(event);
}

/**
 * Opens a sidebar in the document containing the add-on's user interface.
 */
function showSidebar() {
  const ui =
    HtmlService.createHtmlOutputFromFile("sidebar").setTitle("Translate");
  SlidesApp.getUi().showSidebar(ui);
}

/**
 * Recursively gets child text elements a list of elements.
 * @param {PageElement[]} elements The elements to get text from.
 * @return {Text[]} An array of text elements.
 */
function getElementTexts(elements) {
  let texts = [];
  for (const element of elements) {
    switch (element.getPageElementType()) {
      case SlidesApp.PageElementType.GROUP:
        for (const child of element.asGroup().getChildren()) {
          texts = texts.concat(getElementTexts(child));
        }
        break;
      case SlidesApp.PageElementType.TABLE: {
        const table = element.asTable();
        for (let r = 0; r < table.getNumRows(); ++r) {
          for (let c = 0; c < table.getNumColumns(); ++c) {
            texts.push(table.getCell(r, c).getText());
          }
        }
        break;
      }
      case SlidesApp.PageElementType.SHAPE:
        texts.push(element.asShape().getText());
        break;
    }
  }
  return texts;
}

/**
 * Translates selected slide elements to the target language using Apps Script's Language service.
 *
 * @param {string} targetLanguage The two-letter short form for the target language. (ISO 639-1)
 * @return {number} The number of elements translated.
 */
function translateSelectedElements(targetLanguage) {
  // Get selected elements.
  const selection = SlidesApp.getActivePresentation().getSelection();
  const selectionType = selection.getSelectionType();
  let texts = [];
  switch (selectionType) {
    case SlidesApp.SelectionType.PAGE:
      for (const page of selection.getPageRange().getPages()) {
        texts = texts.concat(getElementTexts(page.getPageElements()));
      }
      break;
    case SlidesApp.SelectionType.PAGE_ELEMENT: {
      const pageElements = selection.getPageElementRange().getPageElements();
      texts = texts.concat(getElementTexts(pageElements));
      break;
    }
    case SlidesApp.SelectionType.TABLE_CELL:
      for (const cell of selection.getTableCellRange().getTableCells()) {
        texts.push(cell.getText());
      }
      break;
    case SlidesApp.SelectionType.TEXT:
      for (const element of selection.getPageElementRange().getPageElements()) {
        texts.push(element.asShape().getText());
      }
      break;
  }

  // Translate all elements in-place.
  for (const text of texts) {
    text.setText(
      LanguageApp.translate(text.asRenderedString(), "", targetLanguage),
    );
  }

  return texts.length;
}
```

### sidebar.html

```
<html>
<head>
  <link rel="stylesheet" href="https://ssl.gstatic.com/docs/script/css/add-ons1.css">
  <style>
    .logo { vertical-align: middle; }
    ul { list-style-type: none; padding: 0; }
    h4 { margin: 0; }
  </style>
</head>
<body>
<form class="sidebar branding-below">
  <h4>Translate selected slides into:</h4>
  <ul id="languages"></ul>
  <div class="block" id="button-bar">
    <button class="blue" id="run-translation">Translate</button>
  </div>
  <h5 class="error" id="error"></h5>
</form>
<div class="sidebar bottom">
  <img alt="Add-on logo" class="logo"
       src="https://www.gstatic.com/images/branding/product/1x/translate_48dp.png" width="27" height="27">
  <span class="gray branding-text">Translate sample by Google</span>
</div>

<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script>
  $(function() {
    // Add an input radio button for every language.
    const languages = {
      ar: 'Arabic',
      zh: 'Chinese',
      en: 'English',
      fr: 'French',
      de: 'German',
      hi: 'Hindi',
      ja: 'Japanese',
      pt: 'Portuguese',
      es: 'Spanish'
    };
    const languageList = Object.keys(languages).map((id)=> {
      return $('<li>').html([
        $('<input>')
                .attr('type', 'radio')
                .attr('name', 'dest')
                .attr('id', 'radio-dest-' + id)
                .attr('value', id),
        $('<label>')
                .attr('for', 'radio-dest-' + id)
                .html(languages[id])
      ]);
    });

    $('#run-translation').click(runTranslation);
    $('#languages').html(languageList);
  });

  /**
   * Runs a server-side function to translate the text on all slides.
   */
  function runTranslation() {
    this.disabled = true;
    $('#error').text('');
    google.script.run
            .withSuccessHandler((numTranslatedElements, element) =>{
              element.disabled = false;
              if (numTranslatedElements === 0) {
                $('#error').empty()
                        .append('Did you select elements to translate?')
                        .append('<br/>')
                        .append('Please select slides or individual elements.');
              }
              return false;
            })
            .withFailureHandler((msg, element)=> {
              element.disabled = false;
              $('#error').text('Something went wrong. Please check the add-on logs.');
              return false;
            })
            .withUserObject(this)
            .translateSelectedElements($('input[name=dest]:checked').val());
  }
</script>
</body>
</html>
```

## Run the script

1. In your Slides presentation, reload the page.
2. Click **Extensions** > **Translate Slides** > **Start**. It can take several seconds for the add-on menu item to appear.
3. When prompted, authorize the add-on.
4. Again, click **Extensions** > **Translate Slides** > **Start**.
5. Add text to your presentation and select it.
6. In the add-on, click **Translate** to replace the selected text.

## Next steps

- [Extending Google Slides with Apps Script](/apps-script/guides/slides)
- [Slides service reference](/apps-script/reference/slides)
