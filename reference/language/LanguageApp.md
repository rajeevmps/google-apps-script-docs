# LanguageApp

Provides scripts a way to compute automatic translations of text.

The Language service provides scripts a way to compute automatic translations of text.

## Methods

### translate(text, sourceLanguage, targetLanguage)

**Signature:** `translate(text: String, sourceLanguage: String, targetLanguage: String): String`

**Parameters:**
- `text` (String) — the text to translate
- `sourceLanguage` (String) — the language code in which text is written
- `targetLanguage` (String) — the language code to which the text should be translated

**Returns:** `String` — the translated text

**Description:** Automatically translates some text from a source language to a destination language. When sourceLanguage is set to an empty string, the source language code will be auto-detected.

**Code Sample:**
```javascript
const spanish = LanguageApp.translate('This is a test', 'en', 'es');
Logger.log(spanish);
```

### translate(text, sourceLanguage, targetLanguage, advancedArgs)

**Signature:** `translate(text: String, sourceLanguage: String, targetLanguage: String, advancedArgs: Object): String`

**Parameters:**
- `text` (String) — the text to translate
- `sourceLanguage` (String) — the language code in which text is written
- `targetLanguage` (String) — the language code to which the text should be translated
- `advancedArgs` (Object) — optional JavaScript object with fields:
  - `contentType` (String) — supported values are 'text' (default) and 'html'

**Returns:** `String` — the translated text

**Description:** Automatically translates some text from a source language to a destination language.

**Code Sample:**
```javascript
const spanish = LanguageApp.translate(
    'This is a <strong>test</strong>',
    'en',
    'es',
    {contentType: 'html'},
);
Logger.log(spanish);
```
