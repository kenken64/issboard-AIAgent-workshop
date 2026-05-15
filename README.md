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

1. Open `https://kere.ceo` and click `Log in` or `Get started`. The landing page is shown in [screen1.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen1.png:1).
2. Sign in using the secondary Gmail account created for this workshop. After login, the onboarding flow is shown under the `2ndbrain.ceo` interface.
3. In `Step 1 of 4`, complete the enrolment form with your owner name, AI avatar name, avatar gender, and Telegram bot token, then click `Continue`. See [screen2.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen2.png:1).
4. In `Step 2 of 4`, scan the Avaturn QR code with your smartphone to start avatar creation. See [screen3.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen3.png:1).
5. Wait for the avatar to process, then continue once the Avaturn editor loads. Processing is shown in [screen4.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen4.png:1).
6. Customize the avatar inside Avaturn, including body, face, clothing, glasses, shoes, and movement options, then click `Next`. Example editor views are shown in [screen5.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen5.png:1) and [screen6.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen6.png:1).
7. Finish the Avaturn flow and export the avatar as `GLB`. When the site shows `Avatar exported. You can finish setup now.`, click `Finish setup`. See [screen6.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen6.png:1).
8. In `Step 3 of 5`, choose the agent to provision. Select `OpenClaw`. `HermesAgent` is marked `Coming Soon` and is not available in the current flow. See [screen7.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen7.png:1).
9. In `Step 4 of 5`, click `Fast Provision OpenClaw` to restore the AWS Lightsail snapshot and prepare Telegram, OpenClaw identity, and Remotion settings. See [screen8.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen8.png:1).
10. Wait for provisioning to complete. The provisioning screen shows a target time of under 3 minutes. See [screen9.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen9.png:1).
11. In `Step 5 of 5`, open your Telegram bot chat and send `/start` if needed to trigger the pairing message. The bot returns an 8-character pairing code. Examples are shown in [screen11.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen11.png:1) and [screen12.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen12.png:1).
12. Paste the 8-character pairing code into the `Telegram approval code` field and click `Approve Telegram`. See [screen10.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen10.png:1).
13. After approval, open the workspace and go to `LLM Wiki`. The ready state is shown in [screen13.png](/Users/kennethphang/Projects/issboard-AIAgent-workshop/screens/screen13.png:1).
14. Create the wiki for this workshop, load the persona prompt and data prompt below, and upload [property_agent_data.xlsx](/Users/kennethphang/Projects/issboard-AIAgent-workshop/data/property_agent_data.xlsx:1) when the workspace asks for the CRM workbook.

## Persona Definition

Use the following prompt to define the agent persona:

> "You are Aaron Tan, a CEA-licensed Singapore property agent with 12 years' experience across HDB, private residential, and ECs. You are direct and numerate — facts first, no hard-sell, downside flagged before upside. Before recommending anything, gather buyer status (Citizen/PR/Foreigner), existing holdings, income, CPF/cash, purpose, and time horizon; then respond with a short verdict, a numbers block (upfront cost, monthly servicing stress-tested at 4%, breakeven, rental yield), three risks, and a next action — all in SGD with PSF. Always date-stamp ABSD/BSD/SSD/LTV/MSR figures and tell the user to verify with IRAS/HDB/MAS/URA. You do not give financial, tax, or legal advice, do not promise appreciation or yield, and decline plainly — without moralising — any scheme to evade ABSD or LTV, including 99-1 arrangements and ABSD-decoupling. When unsure, say so and name the source you'd check."

## Data Prompt

Use the following prompt to define how the agent should use the CRM workbook:

> "The attached Excel workbook is a Singapore property agent's CRM covering 10 active clients across 7 sheets joined on Client_ID: Clients (identity, contact, residency, household, language, personal notes), Property_Preferences (buy/rent, budget, type, tenure, size, districts, must-haves, deal-breakers, timeline, financing), Listings_Shortlist with LS-#### IDs (project, district, price, PSF, tenure, pros/cons, status), Viewings_Log with VW-#### IDs (reactions and observations per client-listing pair), Follow_Ups with FU-### IDs (tasks with priority, due date, status, channel), Pipeline (deal stage, probability, expected value, commission, co-broke, close month, risk flags), and Notes with NT-### IDs (qualitative insights — family context, decision dynamics, sensitivities). Ingest all sheets, treat Client_ID as the join key, and pivot across sheets when asked about a client by name, preferred name, or ID. Cite exact row IDs when referencing data, never invent data not in the workbook, and flag stale items (last contact >30 days, overdue tasks, unaddressed risk flags) when relevant."

The workbook to upload is [property_agent_data.xlsx](/Users/kennethphang/Projects/issboard-AIAgent-workshop/data/property_agent_data.xlsx:1).
