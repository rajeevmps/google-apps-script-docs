# HTML Service Reference

Local offline markdown copy of the Google Apps Script HTML Service reference documentation.

- [HtmlService](./HtmlService.md) — Service for returning HTML and other text content from a script; the entry point for creating `HtmlOutput` and `HtmlTemplate` objects.
- [HtmlOutput](./HtmlOutput.md) — An object representing HTML content that can be served from a script, with methods to configure its content, title, size, favicon, meta tags, and frame/sandbox options.
- [HtmlOutputMetaTag](./HtmlOutputMetaTag.md) — An object that represents a single meta tag added to an `HtmlOutput` page via `addMetaTag(name, content)`.
- [HtmlTemplate](./HtmlTemplate.md) — A template object for dynamically constructing HTML using embedded server-side scriptlets.
- [SandboxMode](./SandboxMode.md) — An enum representing the (now legacy) sandbox modes for client-side `HtmlService` scripts; only `IFRAME` mode is currently supported.
- [XFrameOptionsMode](./XFrameOptionsMode.md) — An enum representing the `X-Frame-Options` modes that can be set on an `HtmlOutput` page to control clickjacking protection.
