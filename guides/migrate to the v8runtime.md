# Migrate scripts to the V8 runtime

The Rhino runtime is turning down on or after January 31, 2026. If you have an
existing script using the Rhino runtime, you must migrate the script to V8.

Often the only prerequisite to adding V8 syntax and features to a script is to
[enable the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime#enable-v8).
However, there is a small set of [incompatibilities](https://developers.google.com/apps-script/guides/v8-runtime/migration#incompatibilities) and
[other differences](https://developers.google.com/apps-script/guides/v8-runtime/migration#other_differences) that can result in a script failing or
behaving unexpectedly in the V8 runtime. As you migrate a script to use V8, you
must search the script project for these issues and correct any you find.

## V8 migration procedure

To migrate a script to V8, follow this procedure:

1. [Enable the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime#enable-v8) for the script. The `runtimeVersion` can be checked using the [manifest](https://developers.google.com/apps-script/concepts/manifests) for the Google Apps Script project.
2. Carefully review the following [incompatibilites](https://developers.google.com/apps-script/guides/v8-runtime/migration#incompatibilities). Examine your script to determine if any of the incompatibilities are present; if one or more incompatibilities are present, adjust your script code to remove or avoid the issue.
3. Carefully review the following [other differences](https://developers.google.com/apps-script/guides/v8-runtime/migration#other_differences). Examine your script to determine if any of the listed differences impact your code's behavior. Adjust your script to correct the behavior.
4. Once you have corrected any discovered incompatibilities or other differences, begin updating your code to use [V8 syntax and other features](https://developers.google.com/apps-script/guides/v8-runtime#features_of_the_v8_runtime).
5. After finishing your code adjustments, thoroughly test your script to make sure it behaves as expected.
6. If your script is a web app or published [add-on](https://developers.google.com/workspace/add-ons/overview), you must [create a new version](https://developers.google.com/apps-script/guides/versions#creating_a_version) of the script with the V8 adjustments, and point the deployment to the newly created version. To make the V8 version available to users, you must re-publish the script with this version.
7. If your script is used as a library then create a new versioned deployment of your script. Communicate this new version to all scripts and users that consume your library, instructing them to update to the V8-enabled version. Verify that any older, Rhino-based versions of your library are no longer in active use or accessible.
8. Verify that no instances of your script are still operating on the legacy Rhino runtime. Verify that all [deployments](https://developers.google.com/apps-script/concepts/deployments) are associated with a version which is on V8. Archive old deployments. Review all the [versions](https://developers.google.com/apps-script/guides/versions) and delete the versions which are not using V8 Runtime.

## Incompatibilities

The original Rhino-based Apps Script runtime unfortunately
permitted several non-standard ECMAScript behaviors. Since V8 is standards
compliant, these behaviors aren't supported after migration. Failing to correct
these issues results in errors or broken script behavior once the V8 runtime is
enabled.

The following sections describe each of these behaviors and steps you must take
to correct your script code during migration to V8.

### Avoid `for each(variable in object)`

The
[`for each (variable in object)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for_each...in)
statement was added to JavaScript 1.6, and removed in favor of `for...of`.

**When migrating your script to V8, avoid using `for each (variable in object)`
statements**.

Instead, use `for (variable in object)`:

|---|---|---|
| ``` // Rhino runtime var obj = {a: 1, b: 2, c: 3}; // Don't use 'for each' in V8 for each (var value in obj) { Logger.log("value = %s", value); } ``` |   | ``` // V8 runtime var obj = {a: 1, b: 2, c: 3}; for (var key in obj) {  // OK in V8 var value = obj[key]; Logger.log("value = %s", value); } ``` |

### Avoid `Date.prototype.getYear()`

In the original Rhino runtime,
[`Date.prototype.getYear()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getYear)
returns two-digit years for years from 1900-1999, but four-digit years for other
dates, which was the behavior in JavaScript 1.2 and earlier.

In the V8 runtime,
[`Date.prototype.getYear()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getYear)
returns the year minus 1900 instead as required by ECMAScript standards.

**When migrating your script to V8, always use
[`Date.prototype.getFullYear()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear)**,
which returns a four-digit year regardless of the date.

### Avoid using reserved keywords as names

ECMAScript prohibits the use of certain
[reserved keywords](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)
in function and variable names. The Rhino runtime allowed many of these words,
so if your code uses them, you must rename your functions or variables.

**When migrating your script to V8, avoid naming variable or functions using one
of the
[reserved keywords](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)** .
Rename any variable or function to avoid using the keyword name. Common uses of
keywords as names are `class`, `import`, and `export`.

One exception is that object literals are allowed to use
reserved keywords (in all runtimes):

```
function class() {}     // Syntax error in V8.
var obj = { class: 1 }; // Allowed.
```

### Avoid reassigning `const` variables

In the original Rhino runtime, you can declare a variable using `const` which
means the value of the symbol never changes and future assignments to the
symbol are ignored.

In the new V8 runtime, the `const` keyword is standard compliant and assigning
to a variable declared as a `const` results in a
`TypeError: Assignment to constant variable` runtime error.

**When migrating your script to V8, don't attempt to reassign the value of a
`const` variable**:

|---|---|---|
| ``` // Rhino runtime const x = 1; x = 2;          // No error console.log(x); // Outputs 1 ``` |   | ``` // V8 runtime const x = 1; x = 2;          // Throws TypeError console.log(x); // Never executed ``` |

### Avoid XML literals and the XML object

This
[non-standard extension](https://developer.mozilla.org/en-US/docs/Archive/Web/E4X/Processing_XML_with_E4X)
to ECMAScript allows Apps Script projects to use XML syntax
directly.

**When migrating your script to V8, avoid using direct XML literals or the XML
object**.

Instead, use the [XmlService](https://developers.google.com/apps-script/reference/xml-service/xml-service) to
parse XML:

|---|
| ``` // V8 runtime var incompatibleXml1 = <container><item/></container>;             // Don't use var incompatibleXml2 = new XML('<container><item/></container>');  // Don't use var xml3 = XmlService.parse('<container><item/></container>');     // OK ``` |

### Don't build custom iterator functions using `__iterator__`

JavaScript 1.7 added a feature to allow adding a custom iterator to any class
by declaring an `__iterator__` function in that class's prototype; this was also
added into Apps Script's Rhino runtime as a developer
convenience. However, this feature was never part of the
[ECMA-262 standard](https://www.ecma-international.org/publications/standards/Ecma-262.htm)
and was removed in ECMAScript-compliant JavaScript engines. Scripts using V8
can't use this iterator construction.

**When migrating your script to V8, avoid `__iterator__` function to build
custom iterators** . Instead, use
[ECMAScript 6 iterators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols).

Consider the following array construction:

|---|
| ``` // Create a sample array var myArray = ['a', 'b', 'c']; // Add a property to the array myArray.foo = 'bar'; // The default behavior for an array is to return keys of all properties, //  including 'foo'. Logger.log("Normal for...in loop:"); for (var item in myArray) { Logger.log(item);            // Logs 0, 1, 2, foo } // To only log the array values with `for..in`, a custom iterator can be used. ``` |

The following code examples show how an iterator could be constructed in the
Rhino runtime, and how to construct a replacement iterator in the V8 runtime:

|---|---|---|
| ``` // Rhino runtime custom iterator function ArrayIterator(array) { this.array = array; this.currentIndex = 0; } ArrayIterator.prototype.next = function() { if (this.currentIndex >= this.array.length) { throw StopIteration; } return "[" + this.currentIndex + "]=" + this.array[this.currentIndex++]; }; // Direct myArray to use the custom iterator myArray.__iterator__ = function() { return new ArrayIterator(this); } Logger.log("With custom Rhino iterator:"); for (var item in myArray) { // Logs [0]=a, [1]=b, [2]=c Logger.log(item); } ``` |   | ``` // V8 runtime (ECMAScript 6) custom iterator myArray[Symbol.iterator] = function() { var currentIndex = 0; var array = this; return { next: function() { if (currentIndex < array.length) { return { value: "[${currentIndex}]=" + array[currentIndex++], done: false}; } else { return {done: true}; } } }; } Logger.log("With V8 custom iterator:"); // Must use for...of since //   for...in doesn't expect an iterable. for (var item of myArray) { // Logs [0]=a, [1]=b, [2]=c Logger.log(item); } ``` |

In the V8 runtime, you must use `for...of` when traversing arrays with custom
iterators, since `for..in` doesn't expect iterables.

### Avoid conditional catch clauses

The V8 runtime doesn't support `catch..if` conditional catch clauses, as they
are not standard-compliant.

**When migrating your script to V8, move any catch conditionals inside the
catch body**:

|---|---|---|
| ``` // Rhino runtime try { doSomething(); } catch (e if e instanceof TypeError) {  // Don't use // Handle exception } ``` |   | ``` // V8 runtime try { doSomething(); } catch (e) { if (e instanceof TypeError) { // Handle exception } } ``` |

### Avoid using `Object.prototype.toSource()`

JavaScript 1.3 contained a
[Object.prototype.toSource()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toSource)
method that was never part of any ECMAScript standard. It isn't supported in
the V8 runtime.

**When migrating your script to V8, remove any use of
[Object.prototype.toSource()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toSource)**
from your code.

## Other differences

In addition to the preceding incompatibilities that can cause script failures,
there are a few other differences that, if uncorrected, might result in
unexpected V8 runtime script behavior.

The following sections explain how to update your script code to avoid these
unexpected surprises.

### Adjust locale-specific date and time formatting

The [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
methods [`toLocaleString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString),
[`toLocaleDateString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString),
and [`toLocaleTimeString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleTimeString)
behave differently in the V8 runtime as compared to Rhino.

In Rhino, the default format is the *long format* , and any parameters passed in
are *ignored*.

In the V8 runtime, the default format is the *short format* and parameters
passed in are handled according to the ECMA standard (see the
[`toLocaleDateString()` documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString)
for details).

**When migrating your script to V8, test and adjust your code's expectations
regarding the output of locale-specific date and time methods**:

|---|---|---|
| ``` // Rhino runtime var event = new Date( Date.UTC(2012, 11, 21, 12)); // Outputs "December 21, 2012" in Rhino console.log(event.toLocaleDateString()); // Also outputs "December 21, 2012", //  ignoring the parameters passed in. console.log(event.toLocaleDateString( 'de-DE', { year: 'numeric', month: 'long', day: 'numeric' })); ``` |   | ``` // V8 runtime var event = new Date( Date.UTC(2012, 11, 21, 12)); // Outputs "12/21/2012" in V8 console.log(event.toLocaleDateString()); // Outputs "21. Dezember 2012" console.log(event.toLocaleDateString( 'de-DE', { year: 'numeric', month: 'long', day: 'numeric' })); ``` |

### Avoid using `Error.fileName` and `Error.lineNumber`

In the V8 runtime, the standard JavaScript
[`Error`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
object doesn't support the `fileName` or `lineNumber` as constructor parameters
or object properties.

**When migrating your script to V8,
remove any dependence on `Error.fileName` and `Error.lineNumber`**.

An alternative is to use the
[`Error.prototype.stack`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/stack).
This stack is also non-standard, but supported in V8. The format of the stack
trace produced by the two platforms is slightly different:

|---|---|---|
| ``` // Rhino runtime Error.prototype.stack // stack trace format at filename:92 (innerFunction) at filename:97 (outerFunction) ``` |   | ``` // V8 runtime Error.prototype.stack // stack trace format Error: error message at innerFunction (filename:92:11) at outerFunction (filename:97:5) ``` |

### Adjust handling of stringified enum objects

In the original Rhino runtime, using the JavaScript
[`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
method on an enum object only returns `{}`.

In V8, using the same method on an enum object retuns the enum name.

**When migrating your script to V8, test and adjust your code's expectations
regarding the output of
[`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
on enum objects**:

|---|---|---|
| ``` // Rhino runtime var enumName = JSON.stringify(Charts.ChartType.BUBBLE); // enumName evaluates to {} ``` |   | ``` // V8 runtime var enumName = JSON.stringify(Charts.ChartType.BUBBLE); // enumName evaluates to "BUBBLE" ``` |

### Adjust handling of undefined parameters

In the original Rhino runtime, passing `undefined` to a method as a parameter
resulted in passing the string `"undefined"` to that method.

In V8, passing `undefined` to methods is equivalent to passing `null`.

**When migrating your script to V8, test and adjust your code's expectations
regarding `undefined` parameters**:

|---|---|---|
| ``` // Rhino runtime SpreadsheetApp.getActiveRange() .setValue(undefined); // The active range now has the string // "undefined"  as its value. ``` |   | ``` // V8 runtime SpreadsheetApp.getActiveRange() .setValue(undefined); // The active range now has no content, as // setValue(null) removes content from // ranges. ``` |

### Adjust handling of global `this`

The Rhino runtime defines an implicit special context for scripts that use it.
Script code runs in this implicit context, distinct from the actual global
`this`. This means that references to the "global `this`" in the code actually
evaluate to the special context, which only contains the code and variables
defined in the script. The built-in Apps Script services and
ECMAScript objects are excluded from this use of `this`. This situation was
similar to this JavaScript structure:

|---|
| ``` // Rhino runtime // Apps Script built-in services defined here, in the actual global context. var SpreadsheetApp = { openById: function() { ... } getActive: function() { ... } // etc. }; function() { // Implicit special context; all your code goes here. If the global this // is referenced in your code, it only contains elements from this context. // Any global variables you defined. var x = 42; // Your script functions. function myFunction() { ... } // End of your code. }(); ``` |

In V8, the implicit special context is removed. Global variables and functions
defined in the script are placed in the global context, beside the built-in
Apps Script services and ECMAScript built-ins like `Math` and
`Date`.

**When migrating your script to V8, test and adjust your code's expectations
regarding the use of `this` in a global context.** In most cases the differences
are only apparent if your code examines the keys or property names of the global
`this` object:

|---|---|---|
| ``` // Rhino runtime var myGlobal = 5; function myFunction() { // Only logs [myFunction, myGlobal]; console.log(Object.keys(this)); // Only logs [myFunction, myGlobal]; console.log( Object.getOwnPropertyNames(this)); } ``` |   | ``` // V8 runtime var myGlobal = 5; function myFunction() { // Logs an array that includes the names // of Apps Script services // (CalendarApp, GmailApp, etc.) in // addition to myFunction and myGlobal. console.log(Object.keys(this)); // Logs an array that includes the same // values as above, and also includes // ECMAScript built-ins like Math, Date, // and Object. console.log( Object.getOwnPropertyNames(this)); } ``` |

### Adjust handling of `instanceof` in libraries

Using `instanceof` in a library on an object that is passed as a parameter in a
function from another project can give false negatives. In the V8 runtime, a
project and its libraries are run in different execution contexts and hence have
different globals and prototype chains.

This is only the case if your library uses `instanceof` on an object that isn't
created in your project. Using it on an object that is created in your project,
whether in the same or a different script inside your project, should work as
expected.

**If a project that's running on V8 uses your script as a library, check if your
script uses `instanceof` on a parameter that is passed from another project.
Adjust the usage of `instanceof` and use other feasible alternatives as per your
use case.**

One alternative for `a instanceof b` can be to use the constructor of `a` in
cases where you don't need to search the entire prototype chain and just check
the constructor. Usage: `a.constructor.name == "b"`

Consider Project A and Project B where Project A uses Project B as a library.

|---|---|---|
| ``` //Rhino runtime //Project A function caller() { var date = new Date(); // Returns true return B.callee(date); } //Project B function callee(date) { // Returns true return(date instanceof Date); } ``` |   | ``` //V8 runtime //Project A function caller() { var date = new Date(); // Returns false return B.callee(date); } //Project B function callee(date) { // Incorrectly returns false return(date instanceof Date); // Consider using return (date.constructor.name == // "Date") instead. // return (date.constructor.name == "Date") -> Returns // true } ``` |

Another alternative can be to introduce a function that checks `instanceof` in
the main project and pass the function in addition to other parameters when
calling a library function. The passed function can then be used to check
`instanceof` inside the library.

|---|
| ``` //V8 runtime //Project A function caller() { var date = new Date(); // Returns True return B.callee(date, date => date instanceof Date); } //Project B function callee(date, checkInstanceOf) { // Returns True return checkInstanceOf(date); } ``` |

### Adjust passing of non-shared resources to libraries

Passing a [non-shared](https://developers.google.com/apps-script/guides/libraries#resource_scoping)
resource from the main script to a library works differently in the V8 runtime.

In the Rhino runtime, passing a non-shared resource won't work. The library uses
its own resource instead.

In the V8 runtime, passing a non-shared resource to the library works. The
library uses the passed non-shared resource.

Do not pass non-shared resources as function parameters. Always declare
non-shared resources in the same script that uses them.

Consider Project A and Project B where Project A uses Project B as a library. In
this example, `PropertiesService` is a non-shared resource.

|---|---|---|
| ``` // Rhino runtime // Project A function testPassingNonSharedProperties() { PropertiesService.getScriptProperties() .setProperty('project', 'Project-A'); B.setScriptProperties(); // Prints: Project-B Logger.log(B.getScriptProperties( PropertiesService, 'project')); } //Project B function setScriptProperties() { PropertiesService.getScriptProperties() .setProperty('project', 'Project-B'); } function getScriptProperties( propertiesService, key) { return propertiesService.getScriptProperties() .getProperty(key); } ``` |   | ``` // V8 runtime // Project A function testPassingNonSharedProperties() { PropertiesService.getScriptProperties() .setProperty('project', 'Project-A'); B.setScriptProperties(); // Prints: Project-A Logger.log(B.getScriptProperties( PropertiesService, 'project')); } // Project B function setProperties() { PropertiesService.getScriptProperties() .setProperty('project', 'Project-B'); } function getScriptProperties( propertiesService, key) { return propertiesService.getScriptProperties() .getProperty(key); } ``` |

<br />

### JDBC recommendations in V8 Runtime

With V8 runtime, we have added new features to the JDBC service.

#### Use `executeBatch` for batch operations

Use `executeBatch(params)` operations to perform batch database
operations.

The following example shows how to insert multiple rows into a database using
batching:

Here's the Rhino runtime (old method):

```
var conn = Jdbc.getCloudSqlConnection("jdbc:google:mysql://...");
var stmt = conn.prepareStatement("INSERT INTO employees (name, age) VALUES (?, ?)");
var params = [["John Doe", 30], ["John Smith", 25]];
for (var i = 0; i < params.length; i++) {
  stmt.setString(1, params[i][0]);
  stmt.setInt(2, params[i][1]);
  stmt.execute();
}
```

<br />

Here's the V8 runtime (new method):

```
var conn = Jdbc.getCloudSqlConnection("jdbc:google:mysql://...");
var stmt = conn.prepareStatement("INSERT INTO employees (name, age) VALUES (?, ?)");
var params = [["John Doe", 30], ["John Smith", 25]];
stmt.executeBatch(params);
```

<br />

#### Use `getRows` to fetch result set

Use `getRows(queryString)` to fetch result set data in one call. The
`queryString` consists of comma-separated calls to getter methods of
`JdbcResultSet`, for example: `"getString(1), getDouble('price'), getDate(3,
'UTC')"`. Supported methods include all getter methods which are responsible for
reading column data, for example, `getHoldability`, `getMetaData` etc are not
supported. Arguments can be integer column indexes (1-based) or single or double
quoted string column labels.

The following example shows you how to fetch rows from result set:

Here's the Rhino runtime (old method):

```
var conn = Jdbc.getCloudSqlConnection("jdbc:google:mysql://...");
var stmt = conn.createStatement();
var rs = stmt.executeQuery("SELECT name, age FROM employees");
while (rs.next()) {
  Logger.log(rs.getString('name') + ", " + rs.getInt('age'));
}
```

<br />

Here's the V8 runtime (new method):

```
var conn = Jdbc.getCloudSqlConnection("jdbc:google:mysql://...");
var stmt = conn.createStatement();
var rs = stmt.executeQuery("SELECT name, age FROM employees");
var rows = rs.getRows("getString('name'), getInt('age')");
for (var i = 0; i < rows.length; i++) {
  Logger.log(rows[i][0] + ", " + rows[i][1]);
}
```

<br />

### Update access to standalone scripts

For standalone scripts running on V8 runtime, you need to provide users at least
view access to the script in order for the script's triggers to work properly.