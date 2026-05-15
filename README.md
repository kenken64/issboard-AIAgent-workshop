# ISS Board AI Agentic Workshop (Openclaw , Hermes)

Starter repository for the ISS Board AI Agent workshop.

## Purpose

This repository is intended to hold workshop materials, experiments, and project files for building and testing AI-agent workflows.

## Prerequisites

Before working with workshop integrations, set up a separate Gmail account and a Telegram bot token:

1. Create a secondary Gmail account dedicated to this workshop so you can keep credentials, notifications, and test activity separate from your primary account.
2. Install Telegram on your phone or desktop and create or sign in to your Telegram account.
3. In Telegram search for `@BotFather` and open the verified BotFather chat.
4. Send `/start` to begin.
5. Send `/newbot` and follow the prompts.
6. Enter a display name for your bot when BotFather asks for it.
7. Enter a unique username for your bot. Telegram requires bot usernames to end with `bot`, for example `issboard_workshop_bot`.
8. After the bot is created, BotFather will return an HTTP API token.
9. Copy the token and store it securely. Do not commit it into this repository.

## Platform Setup Walkthrough

Use the following flow to create and provision the workshop agent. The screenshots in the [`screens`](./screens) folder match these steps.

1. Open `https://kere.ceo` and click `Log in` or `Get started`. The landing page is shown in [screen1.png](screens/screen1.png).
2. Sign in using the secondary Gmail account created for this workshop. After login, the onboarding flow is shown under the `2ndbrain.ceo` interface.
3. In `Step 1 of 4`, complete the enrolment form with your owner name, AI avatar name, avatar gender, and Telegram bot token, then click `Continue`. See [screen2.png](screens/screen2.png).
4. In `Step 2 of 4`, scan the Avaturn QR code with your smartphone to start avatar creation. See [screen3.png](screens/screen3.png).
5. Wait for the avatar to process, then continue once the Avaturn editor loads. Processing is shown in [screen4.png](screens/screen4.png).
6. Customize the avatar inside Avaturn, including body, face, clothing, glasses, shoes, and movement options, then click `Next`. Example editor views are shown in [screen5.png](screens/screen5.png) and [screen6.png](screens/screen6.png).
7. Finish the Avaturn flow and export the avatar as `GLB`. When the site shows `Avatar exported. You can finish setup now.`, click `Finish setup`. See [screen6.png](screens/screen6.png).
8. In `Step 3 of 5`, choose the agent to provision. Select `OpenClaw`. `HermesAgent` is marked `Coming Soon` and is not available in the current flow. See [screen7.png](screens/screen7.png).
9. In `Step 4 of 5`, click `Fast Provision OpenClaw` to restore the AWS Lightsail snapshot and prepare Telegram, OpenClaw identity, and Remotion settings. See [screen8.png](screens/screen8.png).
10. Wait for provisioning to complete. The provisioning screen shows a target time of under 3 minutes. See [screen9.png](screens/screen9.png).
11. In `Step 5 of 5`, open your Telegram bot chat and send `/start` if needed to trigger the pairing message. The bot returns an 8-character pairing code. Examples are shown in [screen11.png](screens/screen11.png) and [screen12.png](screens/screen12.png).
12. Paste the 8-character pairing code into the `Telegram approval code` field and click `Approve Telegram`. See [screen10.png](screens/screen10.png).
13. After approval, open the workspace and go to `LLM Wiki`. The ready state is shown in [screen13.png](screens/screen13.png).
14. Create the wiki for this workshop, load the persona prompt and data prompt below, and upload [property_agent_data.xlsx](data/property_agent_data.xlsx) when the workspace asks for the CRM workbook.

## Persona Definition

Use the following prompt to define the agent persona:

> "Create a Second Brain for a Singapore property agent named Aaron Tan.
>
> Requirements:
> - HDB, condo, EC workflow
> - factual, direct, downside-first advice
> - ask buyer status, holdings, income, CPF/cash, purpose, time horizon before recommendations
> - output: verdict, numbers block, 3 risks, next action
> - all figures in SGD and PSF
> - date-stamp ABSD, BSD, SSD, LTV, MSR
> - tell users to verify with IRAS, HDB, MAS, URA
> - no financial/tax/legal advice
> - no promises of appreciation or yield
> - refuse ABSD/LTV evasion schemes
>
> Generate the markdown scaffold, starter pages, folder structure, and graph-ready links."

## Data Prompt

Use the following prompt to define how the agent should use the CRM workbook:

> "Entities (sheets):
>
> Clients — identity, contact, residency, household, language, personal notes
> Property_Preferences — buy/rent, budget, type, tenure, size, districts, must-haves, deal-breakers, timeline, financing
> Listings_Shortlist (LS-####) — project, district, price, PSF, tenure, pros/cons, status
> Viewings_Log (VW-####) — reactions/observations per client-listing pair
> Follow_Ups (FU-###) — task, priority, due date, status, channel
> Pipeline — stage, probability, expected value, commission, co-broke, close month, risk flags
> Notes (NT-###) — family context, decision dynamics, sensitivities
>
> Rules: Ingest all sheets; join on Client_ID; resolve clients by name, preferred name, or ID; cite exact row IDs; never invent data; flag stale items (last contact >30d, overdue tasks, unaddressed risk flags)."

The workbook to upload is [property_agent_data.xlsx](data/property_agent_data.xlsx).
