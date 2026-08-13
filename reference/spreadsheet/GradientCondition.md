# GradientCondition

Access gradient color conditions in ConditionalFormatRules.

GradientCondition is used to access gradient color conditions in ConditionalFormatRules. A gradient condition is defined by three points (min, mid, max), each with a color, value, and InterpolationType. Cell colors are interpolated based on their content's proximity to the min, mid, and max points of the gradient condition.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getMinColorObject()` | `Color\|null` | Gets the color set for the minimum value of this gradient condition. Returns `null` if the color hasn't been set. |
| `getMinType()` | `InterpolationType\|null` | Gets the interpolation type for the minimum value of this gradient condition. Returns `null` if the gradient min type hasn't been set. |
| `getMinValue()` | `String` | Gets the minimum value of this gradient condition. Returns an empty string if the `InterpolationType` is `MIN` or if the min value hasn't been set. |
| `getMidColorObject()` | `Color\|null` | Gets the color set for the midpoint value of this gradient condition. Returns `null` if the color hasn't been set. |
| `getMidType()` | `InterpolationType\|null` | Gets the interpolation type for the midpoint value of this gradient condition. Returns `null` if the gradient mid type hasn't been set. |
| `getMidValue()` | `String` | Gets the midpoint value of this gradient condition. Returns an empty string if the gradient mid value hasn't been set. |
| `getMaxColorObject()` | `Color\|null` | Gets the color set for the maximum value of this gradient condition. Returns `null` if the color hasn't been set. |
| `getMaxType()` | `InterpolationType\|null` | Gets the interpolation type for the maximum value of this gradient condition. Returns `null` if the gradient max type hasn't been set. |
| `getMaxValue()` | `String` | Gets the max value of this gradient condition. Returns an empty string if the `InterpolationType` is `MAX` or if the max value hasn't been set. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getMinColor()` | `String` | Deprecated. Replaced by `getMinColorObject()`. Gets the color set for the minimum value of this gradient condition. Returns an empty string if the color hasn't been set. |
| `getMidColor()` | `String` | Deprecated. Replaced by `getMidColorObject()`. Gets the color set for the midpoint value of this gradient condition. Returns an empty string if the color hasn't been set. |
| `getMaxColor()` | `String` | Deprecated. Replaced by `getMaxColorObject()`. Gets the color set for the maximum value of this gradient condition. Returns an empty string if the color hasn't been set. |

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (let i = 0; i < rules.length; i++) {
  const gradient = rules[i].getGradientCondition();
  const minColor = gradient.getMinColorObject().asRgbColor().asHexString();
  const minType = gradient.getMinType();
  const minValue = gradient.getMinValue();
  const midColor = gradient.getMidColorObject().asRgbColor().asHexString();
  const midType = gradient.getMidType();
  const midValue = gradient.getMidValue();
  const maxColor = gradient.getMaxColorObject().asRgbColor().asHexString();
  const maxType = gradient.getMaxType();
  const maxValue = gradient.getMaxValue();
  Logger.log(`The conditional format gradient information for rule ${i}:
    MinColor ${minColor}, MinType ${minType}, MinValue ${minValue},
    MidColor ${midColor}, MidType ${midType}, MidValue ${midValue},
    MaxColor ${maxColor}, MaxType ${maxType}, MaxValue ${maxValue}`);
}
```
