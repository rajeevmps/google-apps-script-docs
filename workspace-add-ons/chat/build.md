# Build Google Chat interfaces

This guide explains how to construct user interfaces for Google Workspace add-ons that extend Google Chat, enabling interactive functionality within Chat spaces.

Google Chat add-ons utilize triggers like adding to space, messages, and removal to initiate actions and responses.

Developers can use event objects to access data from user interactions and triggers within their Chat add-ons.

Chat apps can respond to interactions with various actions, including sending messages, displaying cards, and opening dialogs.

Add-ons can leverage the Google Chat API for advanced functionalities like delayed responses, cross-space operations, or user authentication.

## Core Components

To build interfaces for Chat apps, developers use three main add-on components:

**Triggers** — The ways Google Chat users invoke a Chat app, such as adding it to a space or sending it a message.

**Event objects** — The data that Chat apps receive from triggers or UI interactions.

**Actions** — The ways that Chat apps can respond to interactions, such as sending messages or returning a card-based user interface.

## Chat Triggers

| Trigger | Description | Typical Response |
|---------|-------------|------------------|
| **Added to space** | User adds the Chat app to a space, or administrator installs it in direct message spaces | App sends onboarding message explaining functionality |
| **Message** | User interacts through DM, @mention, link matching, or multiselect menu input | App responds based on message content |
| **Removed from space** | User removes app or administrator uninstalls it | App removes notifications and clears internal storage |
| **App command** | User uses a Chat app command | App responds with message or opens dialog |

## Building Chat Interfaces

Chat apps can build and display cards in these interfaces:

- **Messages** containing text, static or interactive cards, and buttons
- **Dialogs** which are cards that open in a new window, typically prompting information submission
- **Link previews** which are cards previewing external service information

## Responding to Interactions

Chat apps must respond within 30 seconds using one of these JSON objects:

**DataActions** — Creates or updates Google Workspace data. To send or update Chat messages, the object must contain relevant markup.

**RenderActions** — Creates or updates dialogs or provides input suggestions for multi-select menus.

**AuthorizationError** — Prompts users with an authorization card (only basic authorization supported in Chat).

## Google Chat API Usage

Chat apps must call the Google Chat API to:
- Respond after 30 seconds
- Perform tasks outside the interaction space
- Access Chat features unavailable as add-on actions
- Perform tasks on behalf of Chat users requiring authentication
