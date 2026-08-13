# CSS package for Editor add-ons

To help your Editor add-on look and feel like Google Sheets, Docs, Slides, or Forms, link in the CSS package following to apply Google styling to fonts, buttons, and form elements. For a sample of the CSS package in use, see the Docs add-on quickstart. To use the CSS package, include the following at the top of each HTML file:

```
<link rel="stylesheet" href="https://ssl.gstatic.com/docs/script/css/add-ons1.css">
```

Note that the style for form elements cannot be completely controlled in all browsers. In particular, `<select>` elements display some visual artifacts in Firefox and Internet Explorer, although they still work properly. To see what the styles look like in a given browser, load this page in that browser.

## Typography

Use Arial font for all text, in the following styles depending on use:

| Use and appearance | Markup with CSS package |
|---|---|
| Titles and headers | `<h1>Titles and headers</h1>` |
| Bold text | `<b>Bold text</b>` |
| Normal text | Normal text |
| Links | `<a href="">Links</a>` |
| Current navigation selection | `<span class="current">Current navigation selection</span>` |
| Form input errors | `<span class="error">Form input errors</span>` |
| Gray text | `<span class="gray">Gray text</span>` |
| Secondary text | `<span class="secondary">Secondary text</span>` |

## Buttons

You can use any of the standard types of buttons—`<button>`, `<input type="button">`, or `<input type="submit">`, as well as `<a class="button">`. Buttons that are horizontally adjacent space themselves out automatically. There are several colors available, for various uses:

| Use | Markup with CSS package |
|---|---|
| Primary action | `<button class="action">Translate</button>` |
| Secondary action(s) | `<button>Close</button>` |
| Create action | `<button class="create">Create</button>` |
| Share action | `<button class="share">Share</button>` |

## Checkboxes

Markup with CSS package:

```html
<div>
<input type="checkbox" id="checkbox1" checked>
<label for="checkbox1">Checked</label>
</div>
<div>
<input type="checkbox" id="checkbox2">
<label for="checkbox2">Unchecked</label>
</div>
<div>
<input type="checkbox" id="checkbox3" checked disabled>
<label for="checkbox3">Checked, disabled</label>
</div>
<div>
<input type="checkbox" id="checkbox4" disabled>
<label for="checkbox4">Unchecked, disabled</label>
</div>
```

## Radio buttons

Markup with CSS package:

```html
<div>
<input type="radio" name="radio-a" id="radio1" checked>
<label for="radio1">Checked</label>
</div>
<div>
<input type="radio" name="radio-a" id="radio2">
<label for="radio2">Unchecked</label>
</div>
<div>
<input type="radio" name="radio-b" id="radio3"
checked disabled>
<label for="radio3">Checked, disabled</label>
</div>
<div>
<input type="radio" name="radio-b" id="radio4" disabled>
<label for="radio4">Unchecked, disabled</label>
</div>
```

## Select menus

Markup with CSS package:

```html
<div class="block form-group">
<label for="select">Select</label>
<select id="select">
<option selected>Google Docs</option>
<option>Google Forms</option>
<option>Google Sheets</option>
</select>
</div>
<div class="block form-group">
<label for="disabled-select">Disabled select</label>
<select id="disabled-select" disabled>
<option selected>Google Docs</option>
<option>Google Forms</option>
<option>Google Sheets</option>
</select>
</div>
```

## Text areas

Markup with CSS package:

```html
<div class="form-group">
<label for="sampleTextArea">Label</label>
<textarea id="sampleTextArea" rows="3"></textarea>
</div>
```

## Text fields

Markup with CSS package:

```html
<div class="inline form-group">
<label for="city">City</label>
<input type="text" id="city" style="width: 150px;">
</div>
<div class="inline form-group">
<label for="state">State</label>
<input type="text" id="state" style="width: 40px;">
</div>
<div class="inline form-group">
<label for="zip-code">Zip code</label>
<input type="text" id="zip-code" style="width: 65px;">
</div>
```

## Sidebars

Sidebars can be tricky to style because while the height is variable, many add-ons need to include a branding area that does not scroll. The following is a copy of the sidebar from the Google Docs add-on quickstart. If you drag the bottom-right corner of the text area to make the content taller than the sidebar, the content area automatically scrolls but the branding at the bottom does not.

The example uses the `sidebar` class to apply the correct padding and the `bottom` class to force the branding area to the bottom. A local class, `branding-below`, then defines the area that the main area of the sidebar should leave clear from the bottom.

Markup with CSS package:

```html
<style>
.branding-below {
bottom: 56px;
top: 0;
}
</style>
<div class="sidebar branding-below">
<div class="block form-group">
<label for="translated-text">
<b>Translation</b></label>
<textarea id="translated-text" rows="15">
</textarea>
</div>
<div class="block">
<input type="checkbox" id="save-prefs">
<label for="save-prefs">
Use these languages by default</label>
</div>
<div class="block">
<button class="blue">Translate</button>
<button>Insert</button>
</div>
</div>
<div class="sidebar bottom">
<span class="gray">
Translate sample by Google</span>
</div>
```
