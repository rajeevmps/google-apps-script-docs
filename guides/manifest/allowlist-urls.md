# Allowlist URLs

## Overview

Allowlists designate specific URLs pre-approved for access by your script or add-on, protecting user data by restricting access to non-allowlisted URLs.

## Key Requirements

**When Allowlists Are Required:**
- Optional for test deployments
- Required for versioned deployments

**Use Cases:**
- Retrieving information from external HTTPS endpoints via UrlFetch service
- Opening or displaying external URLs in response to user actions (especially for Google Workspace add-ons)

## URL Prefix Rules

Each allowlisted prefix must meet these criteria:

- Valid URL format with `https://` protocol (not `http://`)
- Full domain name included
- Non-empty path required (e.g., `https://www.google.com/` is valid; `https://www.google.com` is not)
- Case-sensitive path matching
- A URL matches if identical to or a child of the prefix

**Example valid prefix:** `https://example.com/foo` matches:
- `https://example.com/foo`
- `https://example.com/foo/bar`
- `https://example.com/foo?bar`

## Wildcard Usage

You can use a single leading wildcard (`*`) to match subdomains:

**Valid:** `https://*.example.com/foo` matches `https://subdomain.example.com/foo`

**Invalid patterns:**
- Multiple wildcards (`https://*.*.example.com/foo`)
- Non-leading wildcards (`https://subdomain.*.example.com/foo`)

**Important Note:** While a single `*` wildcard is permitted in `addOns.common.openLinkUrlPrefixes` to match all links, this approach is "not recommended as it can expose a user's data to risk" and may complicate add-on review processes.

Source: https://developers.google.com/apps-script/manifest/allowlist-url
