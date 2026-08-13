# Determine if VBA macros are compatible

## Overview

Google's Macro Converter tool helps developers assess whether Excel files containing VBA macros can be converted to Apps Script. The process involves generating a compatibility report that evaluates which APIs can be directly converted, which require workarounds, and which need manual investigation.

## Compatibility Statuses

The tool assigns three primary statuses:

- **Supported exactly**: Files where all APIs have direct Apps Script equivalents and can proceed to conversion without modifications
- **Supported with workarounds**: Files containing at least one API requiring code adjustments to function in Apps Script
- **Needs more investigation**: Files with APIs lacking clear equivalents or requiring manual review to determine convertibility

## Generating a Report

The process involves these steps:

1. Open Google Drive and access the Macro Converter add-on from the right sidebar
2. Select Excel files for analysis (fewer than 2,000 at once)
3. Choose a destination folder for the report
4. Click "Generate report" and wait for completion
5. View the generated compatibility analysis

## Report Components

The compatibility report includes several worksheets:

- A summary sheet with aggregated compatibility analysis
- File-by-file compatibility listings
- Detailed API analysis with recommended actions
- Separate sheets for APIs requiring investigation and those with available workarounds

## Recommended Next Steps

For "Supported exactly" files, proceed directly with conversion. For files marked "Supported with workarounds," modify incompatible VBA APIs before or after conversion. Files needing investigation require manual evaluation by someone familiar with the original VBA code before attempting conversion.

Source: https://developers.google.com/apps-script/guides/macro-converter/compatibility-report
