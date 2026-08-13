# console

The console class enables developers to write to the Execution log and Google Cloud Logging.

The console class enables developers to write to the Execution log and Google Cloud Logging (when the script is associated with a standard Cloud Project). Unlike the Logger class, console methods serialize objects to strings and don't support structured logging with jsonPayload. For structured logging, use the Logger class instead.

## Methods

### error() → void

Outputs a blank ERROR level message to the console.

### error(formatOrObject: Object, values: Object...) → void

Outputs an ERROR level message to the console. Parameter `formatOrObject` is a string containing zero or more substitution strings, or a JavaScript object. Parameter `values` are the JavaScript objects with which to replace substitution strings within the message.

### info() → void

Outputs a blank INFO level message to the console.

### info(formatOrObject: Object, values: Object...) → void

Outputs an INFO level message to the console. Parameter `formatOrObject` is a string containing zero or more substitution strings, or a JavaScript object. Parameter `values` are the JavaScript objects with which to replace substitution strings within the message.

### log() → void

Outputs a blank DEBUG level message to the console.

### log(formatOrObject: Object, values: Object...) → void

Outputs a DEBUG level message to the console. Parameter `formatOrObject` is a string containing zero or more substitution strings, or a JavaScript object. Parameter `values` are the JavaScript objects with which to replace substitution strings within the message.

### time(label: String) → void

Starts a timer you can use to track how long an operation takes. Parameter `label` is the name to give the new timer.

### timeEnd(label: String) → void

Stops the specified timer and logs the elapsed time in seconds since it started, to Stackdriver. Parameter `label` is the name of the timer to stop.

### warn() → void

Outputs a blank WARNING level message to the console.

### warn(formatOrObject: Object, values: Object...) → void

Outputs a WARNING level message to the console. Parameter `formatOrObject` is a string containing zero or more substitution strings, or a JavaScript object. Parameter `values` are the JavaScript objects with which to replace substitution strings within the message.

## Code Sample

```javascript
function measuringExecutionTime() {
  const label = "myFunction() time";
  console.time(label);
  try {
    myFunction();
  } catch (e) {
    console.error("myFunction() yielded an error: " + e);
  }
  console.timeEnd(label);
}
```
