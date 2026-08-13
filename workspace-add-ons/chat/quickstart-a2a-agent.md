# Build a Google Chat app with an Agent2Agent agent

## Overview

This guide explains how to construct a Google Workspace add-on functioning within Google Chat that interfaces with an AI agent utilizing the Agent2Agent (A2A) protocol. The agent is developed using the Agent Development Kit (ADK) and hosted in Vertex AI Agent Engine.

The tutorial deploys the LLM Auditor multi-agent sample, which critiques and revises facts using Gemini and Google Search grounding.

## Key Objectives

- Set up your development environment
- Deploy the A2A agent
- Deploy the Chat app
- Configure the Chat app
- Test the Chat app

## Prerequisites Required

- Business or Enterprise Google Workspace account with Chat access
- Google Cloud project with billing enabled
- Python 3.11+
- Python Poetry
- Google Cloud CLI

## Setup Steps

### Enable APIs

Enable Google Chat, Vertex AI, and Cloud Resource Manager APIs through the Google Cloud console.

### Configure OAuth Consent Screen

All apps using OAuth 2.0 require a consent screen configuration. Set app information, audience (Internal), and contact information through the Google Auth platform.

### Create Service Account

Follow these steps:
1. Create a new service account with `Vertex AI User` role
2. Assign necessary roles for Google Cloud resources
3. Create and download a private JSON key file named `credentials.json`

### Deploy A2A Agent

Update the ADK implementation:
- Modify `pyproject.toml` to add ADK and A2A SDK dependencies
- Update `deployment/deploy.py` to deploy as an A2A remote agent
- Create a Cloud Storage bucket
- Set environment variables
- Install and deploy from virtual environment

### Configure Chat App

1. Make a copy of the A2A AI Agent Quickstart Apps Script project
2. Add script properties for `REASONING_ENGINE_RESOURCE_NAME` and `SERVICE_ACCOUNT_KEY`
3. Connect to Google Cloud project using project number
4. Create test deployment to obtain deployment ID

## Chat App Configuration

In the API Console's Google Chat API section:
- Set app name to "A2A Quickstart"
- Enable "Join spaces and group conversations"
- Select Apps Script project as connection type
- Paste deployment ID
- Restrict visibility to your domain

## Testing

To test:
1. Open Google Chat
2. Start new chat and search for the Chat app
3. Send a test message like "The Eiffel Tower was completed in 1900"
4. The app responds with Critic and Reviser sub-agent responses

## Cleanup

Delete the Google Cloud project through the Resource Manager to avoid ongoing charges.
