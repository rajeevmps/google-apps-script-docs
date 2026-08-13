# OptionBuilder

A builder for creating options for SelectSingles and SelectMultiples.

A builder for creating options for SelectSingles and SelectMultiples. The OptionBuilder is utilized within the Data Studio community connector framework to construct dropdown options.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
const config = cc.getConfig();

const option1 = config.newOptionBuilder()
    .setLabel('option label')
    .setValue('option_value');

const option2 = config.newOptionBuilder()
    .setLabel('second option label')
    .setValue('option_value_2');

const info1 = config.newSelectSingle()
    .setId('api_endpoint')
    .setName('Data Type')
    .setHelpText('Select the data type you\'re interested in.')
    .addOption(option1)
    .addOption(option2);
```

## Methods

### setLabel(label)

**Signature:** `setLabel(label: String): OptionBuilder`

**Description:** Sets the label of this option builder. Labels are the text that the user sees when selecting one or more options from the dropdown. Returns this builder, for chaining.

### setValue(value)

**Signature:** `setValue(value: String): OptionBuilder`

**Description:** Sets the value of this option builder. Values are what is passed to the code when a user selects one or more options from the dropdown. Returns this builder, for chaining.
