# Custom function quickstart

## Page Summary

- Google Apps Script can be used to create custom functions for Google Sheets.
- This sample demonstrates creating a custom function to calculate and format the sale price of discounted items in US dollars.
- The process involves setting up the script in the Apps Script editor and then running the function in a spreadsheet cell.

You can use Google Apps Script to write a custom function, then use it in Google Sheets just like a built-in function.

The following quickstart sample creates a custom function that calculates the sale price of discounted items. The sale price is formatted as US dollars.

## Objectives

- Set up the script.
- Run the script.

## Prerequisites

To use this sample, you need the following prerequisites:

- A Google Account (Google Workspace accounts might require administrator approval).
- A web browser with access to the internet.

## Set up the script

1. Create a [new spreadsheet](https://sheets.google.com/create).
2. From within your new spreadsheet, select the menu item **Extensions** > **Apps Script**.
3. Delete any code in the script editor and paste in the following code. Then click **Save**.

```javascript
/**
 * Calculates the sale price of a value at a given discount.
 * The sale price is formatted as US dollars.
 *
 * @param {number} input The value to discount.
 * @param {number} discount The discount to apply, such as .5 or 50%.
 * @return The sale price formatted as USD.
 * @customfunction
 */
function salePrice(input, discount) {
  let price = input - (input * discount);
  let dollarUS = Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
  });
  return dollarUS.format(price);
}
```

## Run the script

1. Switch back to your spreadsheet.
2. In a cell, enter `=salePrice(100,20)`. The first parameter represents the original price and the second parameter represents the discount percentage. If you're in a location that uses decimal commas, you might need to enter `=salePrice(100;20)` instead.

The formula that you enter in the cell runs the function in the script you created in the previous section. The function results in a sale price of `$80.00`.

## Next steps

To continue learning about how to extend Sheets with Apps Script, see the following resources:

- [Spreadsheet custom functions](https://developers.google.com/apps-script/execution_custom_functions)
- [Custom menus in Google Workspace](https://developers.google.com/apps-script/guides/menus)
- [Extend Sheets](https://developers.google.com/apps-script/guides/sheets)

Source: https://developers.google.com/apps-script/quickstart/custom-functions
