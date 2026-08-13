# MimeType

An enumeration that provides access to MIME-type declarations without typing the strings explicitly.

An enumeration that provides access to MIME-type declarations without typing the strings explicitly. Methods that expect a MIME type rendered as a string (for example, `'image/png'`) also accept any of the values below, so long as the method supports the underlying MIME type.

## Code Sample

```javascript
// Use MimeType enum to log the name of every Google Doc in the user's Drive.
const docs = DriveApp.getFilesByType(MimeType.GOOGLE_DOCS);
while (docs.hasNext()) {
  const doc = docs.next();
  Logger.log(doc.getName());
}

// Use plain string to log the size of every PNG in the user's Drive.
const pngs = DriveApp.getFilesByType('image/png');
while (pngs.hasNext()) {
  const png = pngs.next();
  Logger.log(png.getSize());
}
```

## Properties

| Property | Description |
|----------|-------------|
| `GOOGLE_APPS_SCRIPT` | Representation of MIME type for a Google Apps Script project. |
| `GOOGLE_DRAWINGS` | Representation of MIME type for a Google Drawings file. |
| `GOOGLE_DOCS` | Representation of MIME type for a Google Docs file. |
| `GOOGLE_FORMS` | Representation of MIME type for a Google Forms file. |
| `GOOGLE_SHEETS` | Representation of MIME type for a Google Sheets file. |
| `GOOGLE_SITES` | Representation of MIME type for a Google Sites file. |
| `GOOGLE_SLIDES` | Representation of MIME type for a Google Slides file. |
| `FOLDER` | Representation of MIME type for a Google Drive folder. |
| `SHORTCUT` | Representation of MIME type for a Google Drive shortcut. |
| `BMP` | Representation of MIME type for a BMP image file (typically .bmp). |
| `GIF` | Representation of MIME type for a GIF image file (typically .gif). |
| `JPEG` | Representation of MIME type for a JPEG image file (typically .jpg). |
| `PNG` | Representation of MIME type for a PNG image file (typically .png). |
| `SVG` | Representation of MIME type for an SVG image file (typically .svg). |
| `PDF` | Representation of MIME type for a PDF file (typically .pdf). |
| `CSS` | Representation of MIME type for a CSS text file (typically .css). |
| `CSV` | Representation of MIME type for a CSV text file (typically .csv). |
| `HTML` | Representation of MIME type for an HTML text file (typically .html). |
| `JAVASCRIPT` | Representation of MIME type for a JavaScript text file (typically .js). |
| `PLAIN_TEXT` | Representation of MIME type for a plain text file (typically .txt). |
| `RTF` | Representation of MIME type for a rich text file (typically .rtf). |
| `OPENDOCUMENT_GRAPHICS` | Representation of MIME type for an OpenDocument graphics file (typically .odg). |
| `OPENDOCUMENT_PRESENTATION` | Representation of MIME type for an OpenDocument presentation file (typically .odp). |
| `OPENDOCUMENT_SPREADSHEET` | Representation of MIME type for an OpenDocument spreadsheet file (typically .ods). |
| `OPENDOCUMENT_TEXT` | Representation of MIME type for an OpenDocument word-processing file (typically .odt). |
| `MICROSOFT_EXCEL` | Representation of MIME type for a Microsoft Excel spreadsheet file (typically .xlsx). |
| `MICROSOFT_EXCEL_LEGACY` | Representation of MIME type for a Microsoft Excel legacy file (typically .xls). |
| `MICROSOFT_POWERPOINT` | Representation of MIME type for a Microsoft PowerPoint presentation file (typically .pptx). |
| `MICROSOFT_POWERPOINT_LEGACY` | Representation of MIME type for a Microsoft PowerPoint legacy file (typically .ppt). |
| `MICROSOFT_WORD` | Representation of MIME type for a Microsoft Word document file (typically .docx). |
| `MICROSOFT_WORD_LEGACY` | Representation of MIME type for a Microsoft Word legacy file (typically .doc). |
| `ZIP` | Representation of MIME type for a ZIP archive file (typically .zip). |
