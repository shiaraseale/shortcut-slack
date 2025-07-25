# shortcut-slack

# Shortcut Iteration Stats to Slack Notifier

This Google Apps Script function fetches active iteration statistics, including story details, from **Shortcut** (formerly Clubhouse) and posts a summary to a designated **Slack** channel. It provides an overview of each active iteration, broken down by workflow state and assigned team member.

---

## Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Prerequisites](#prerequisites)
* [Setup](#setup)
    * [1. Google Apps Script Setup](#1-google-apps-script-setup)
    * [2. Shortcut API Key](#2-shortcut-api-key)
    * [3. Slack Webhook URL](#3-slack-webhook-url)
    * [4. Update the Script](#4-update-the-script)
* [Usage](#usage)
* [Notes](#notes)

---

## Overview

The `postShortcutStatsToSlack()` function automates the process of generating a progress report from Shortcut and sharing it with your team on Slack. It's particularly useful for daily stand-ups, weekly summaries, or keeping stakeholders informed about the current state of active development iterations.

---

## Features

* **Fetches Active Iterations:** Identifies and processes only iterations currently marked as 'started' in Shortcut.
* **Detailed Iteration Stats:** Provides a summary of points in backlog, unstarted, started, and done states for each active iteration.
* **Story Breakdown by Member and State:** For each iteration, it lists team members and their assigned stories, categorised by workflow state (e.g., 'To Do', 'Doing', 'Done') and total points.
* **Slack Integration:** Formats the collected data into a clear and concise Slack message.
* **Handles Unassigned Stories:** Gracefully accounts for stories without an assigned owner.
* **Dynamic State Types:** Automatically adapts to the workflow state types configured in your Shortcut workflows.

---

## Prerequisites

Before you can use this script, you'll need the following:

* A **Google Account** (to use Google Apps Script).
* Access to **Shortcut** with an API token.
* A **Slack Workspace** with permissions to create incoming webhooks.

---

## Setup

Follow these steps to get the script up and running:

### 1. Google Apps Script Setup

1.  Go to [Google Apps Script](https://script.google.com/home).
2.  Click **"New project"**.
3.  Delete any default code in the `Code.gs` file.
4.  Copy and paste the entire `postShortcutStatsToSlack()` function from your code into the `Code.gs` file.
5.  Save the project (File > Save project or Ctrl + S / Cmd + S). You can name it something like "Shortcut Slack Notifier".

### 2. Shortcut API Key

1.  Log in to your **Shortcut** account.
2.  Navigate to **Settings > API Tokens**.
3.  Generate a new API token if you don't already have one.
4.  **Copy** this token. It's a long alphanumeric string.

### 3. Slack Webhook URL

1.  Log in to your **Slack** workspace.
2.  Go to **Administration > Manage Apps** (or search for "Incoming WebHooks" in the App Directory).
3.  Add or configure an **Incoming WebHooks** integration.
4.  Choose the default channel where messages will be posted (you can override this in the script if needed, but for simplicity, the script sends to the configured webhook channel).
5.  **Copy** the generated Webhook URL. It will look something like `https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`.

### 4. Update the Script

Open your Google Apps Script project and update the following lines with your copied keys:

```javascript
  const shortcutApiKey = 'YOUR_SHORTCUT_API_KEY_HERE'; // Replace with your actual Shortcut API Key
  const slackWebhookUrl = 'YOUR_SLACK_WEBHOOK_URL_HERE'; // Replace with your actual Slack Webhook URL