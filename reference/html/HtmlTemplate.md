# HtmlTemplate

A template object for dynamically constructing HTML.

A template object for dynamically constructing HTML. For more information, see the guide to templates.

## Methods

### evaluate()

Returns: `HtmlOutput`

Evaluates this template and returns an `HtmlOutput` object. Any properties set on this `HtmlTemplate` object are in scope when evaluating. To debug errors in a template, examine the code using the `getCode()` method.

```javascript
const template = HtmlService.createTemplate('<?= foo ?>');
template.foo = 'Hello World!';
Logger.log(template.evaluate().getContent());  // logs 'Hello World!'
```

### getCode()

Returns: `String`

Generates a string of JavaScript code, based on the template file, that can be evaluated. This method produces a string of JavaScript code based on the template file. Calling `eval(<code>)` returns a new `HtmlOutput` object with the content of the template after running all embedded server scripts. The generated code is intended to be human-readable, and so if you need to debug a template you can call `Logger.log(<code>)` to see what was produced. Evaluating this code implicitly binds in all variables in the current scope. In general, it's preferable to use the `evaluate()` method, which takes explicit bindings.

```javascript
const template = HtmlService.createTemplate(
    '<b>The time is <?= new Date() ?></b>',
);
Logger.log(template.getCode());
```

### getCodeWithComments()

Returns: `String`

Generates a string of JavaScript code that can be evaluated, with each line of the code containing the original line from the template as a comment. This method produces a string of JavaScript code based on the template file. Calling `eval(<code>)` returns a new `HtmlOutput` object with the content of the template after running all embedded server scripts. The generated code is intended to be human-readable, and so if you need to debug a template you can call `Logger.log(<code>)` to see what was produced. Evaluating this code implicitly binds in all variables in the current scope. In general, it's preferable to use the `evaluate()` method, which takes explicit bindings.

```javascript
const template = HtmlService.createTemplate(
    '<b>The time is <?= new Date() ?></b>',
);
Logger.log(template.getCodeWithComments());
```

### getRawContent()

Returns: `String`

Returns the unprocessed content of this template.

```javascript
const template = HtmlService.createTemplate(
    '<b>The time is <?= new Date() ?></b>',
);
Logger.log(template.getRawContent());
```

## Properties

None.
