# HomepageTrigger Manifest Resource

## Overview

The `HomepageTrigger` resource defines how homepage triggers behave in Google Workspace add-ons. According to the documentation, "The `HomepageTrigger` configuration defines the behavior of homepage triggers in Google Workspace add-ons."

## Key Characteristics

**Configuration Hierarchy**: Homepage triggers can be set at a common level (`addOns.common.homepageTrigger`) or within individual host application resources. Host application settings take precedence when both are defined and enabled.

**Return Value**: "The function must return an array of `Card` objects for the add-on homepage."

## JSON Structure

The resource contains two primary fields:

| Field | Type | Description |
|-------|------|-------------|
| `enabled` | boolean | Controls whether non-contextual cards are enabled; defaults to `true` |
| `runFunction` | string | Names the trigger function that executes when the trigger fires |

## Configuration Details

The `runFunction` field specifies which function executes when the trigger activates. This function is responsible for constructing and returning the card array that populates the add-on's homepage display.

For complete integration guidance, consult the [Homepage configuration documentation](https://developers.google.com/workspace/add-ons/concepts/homepages#homepage_configuration) referenced within the resource specification.

Source: https://developers.google.com/apps-script/manifest/homepage-trigger
