# Build a Google Chat app with an ADK AI agent

## Overview
This tutorial guides developers through creating a Google Workspace add-on that integrates with Google Chat and connects to an Agent Development Kit (ADK) AI agent hosted on Vertex AI Agent Engine. The example deploys the ADK LLM Auditor multi-agent sample, which critiques and revises facts using Gemini and Google Search grounding.

## Key Objectives
The guide outlines five main goals:
- Set up your development environment
- Deploy the ADK AI agent
- Deploy the Chat app
- Configure the Chat app
- Test the Chat app

## Architecture Flow
The documentation describes a six-step information flow:

1. User sends a message to the Chat app
2. Chat app logic (Apps Script or HTTP) processes the message
3. ADK AI agent hosted on Vertex AI receives and processes interaction
4. Optional integration with Google Workspace or Google services
5. Chat app asynchronously sends responses via Google Chat API
6. Responses deliver to users

## Prerequisites
- Business or Enterprise Google Workspace account with Chat access
- Google Cloud project with billing enabled

## Key Setup Steps

**Enable APIs:** Google Chat, Vertex AI, and Cloud Resource Manager APIs

**Service Account:** Create one with the "Vertex AI User" role and download JSON credentials

**ADK Deployment:** Deploy the LLM Auditor sample from Vertex AI Agent Garden, then copy the resource name

**Apps Script Configuration:** Add script properties for the agent resource name and service account key

**Chat App Registration:** Configure through Google Chat API with the deployment ID

## Testing
Users can test by opening a direct message with the Chat app and submitting test prompts like: "The Eiffel Tower was completed in 1900"

## Cleanup
The guide recommends deleting the Google Cloud project after completion to avoid unnecessary charges.
