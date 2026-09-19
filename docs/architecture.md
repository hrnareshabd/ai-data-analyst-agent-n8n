# Architecture

## Overview

The workflow combines a chat interface, a tool-using AI agent, spreadsheet access, conversational memory, and email delivery in one n8n automation.

## Components

| Component | Responsibility |
| --- | --- |
| Chat Trigger | Receives the user's natural-language question and returns the final response. |
| AI Agent | Decides when data must be retrieved, analyzes rows, and prepares concise answers. |
| OpenAI Chat Model | Provides language understanding, reasoning, and report generation. |
| Simple Memory | Retains recent conversation context across follow-up questions. |
| Google Sheets Tool | Retrieves current rows from the configured worksheet. |
| Gmail Tool | Sends requested findings as a structured HTML email. |

## Processing flow

1. The Chat Trigger receives a question.
2. The AI Agent interprets the request and uses the Google Sheets tool whenever spreadsheet data is required.
3. The agent analyzes the returned rows with the OpenAI model.
4. Simple Memory supplies recent context for follow-up questions.
5. The agent responds in chat or, when requested, formats the result as HTML and calls the Gmail tool.

## Agent behavior

The system prompt instructs the agent to retrieve fresh sheet data before answering data-dependent questions. Email messages use a predictable structure with a title, introduction, summary sections, notes, and sign-off. The agent is also instructed to preserve facts and avoid inventing values.

## Security model

OAuth credentials are managed inside n8n and are not embedded in the workflow export. The public JSON uses placeholders for the spreadsheet and recipient. Before sharing future workflow versions, remove credential IDs, workflow and instance identifiers, webhook identifiers, private URLs, personal addresses, and execution data.

## Extension ideas

- Add chart generation for visual summaries.
- Add a data-quality branch for missing values and duplicates.
- Store generated reports in Google Drive.
- Add scheduled weekly summaries.
- Add approval before outbound email delivery.
- Connect a database or warehouse for larger datasets.
