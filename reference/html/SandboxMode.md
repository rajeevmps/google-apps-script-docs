# SandboxMode

An enum representing the sandbox modes that can be used for client-side HtmlService scripts.

An enum representing the sandbox modes that can be used for client-side `HtmlService` scripts. These values can be accessed from `HtmlService.SandboxMode`, and set by calling `HtmlOutput.setSandboxMode(mode)`.

The `NATIVE` and `EMULATED` modes were deprecated on October 13, 2015 and are now sunset. Only `IFRAME` mode is currently supported.

To protect users from being served malicious HTML or JavaScript, client-side code served from HTML service executes in a security sandbox that imposes restrictions on the code.

```javascript
// Read the sandbox mode (in a client-side script).
<script>
  alert(google.script.sandbox.mode);
</script>
```

## Properties

### EMULATED

A legacy sandbox mode that emulates ECMAScript 5 strict mode using only the features available in ECMAScript 3. This mode was the default prior to February 2014. This mode was sunset as of December 10, 2015. All scripts attempting to use `EMULATED` now use `IFRAME` instead.

### IFRAME

A sandbox mode that uses iframe sandboxing instead of the Caja sandbox technology used by the `EMULATED` and `NATIVE` modes. This mode is the default for new scripts as of November 12, 2015 and for all scripts as of July 6, 2016. It imposes many fewer restrictions than the other sandbox modes and runs fastest, but does not work at all in certain older browsers, including Internet Explorer 9.

### NATIVE

A sandbox mode that is built on top of ECMAScript 5 strict mode. This mode was sunset as of July 6, 2016. All scripts now use `IFRAME` mode.
