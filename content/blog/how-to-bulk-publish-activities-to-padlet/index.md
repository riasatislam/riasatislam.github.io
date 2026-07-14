---
title: "How to Bulk Publish Activities to Padlet from a Spreadsheet"
date: 2026-07-14T12:00:00+01:00
draft: false
summary: "A practical guide for educators who want to bulk publish seminar questions, tutorial prompts, reading responses, and other classroom activities to Padlet from a spreadsheet."
tags: ["Padlet", "Teaching", "Educational Technology", "Python", "Automation", "Higher Education"]
categories: ["Teaching"]
---

You have changed 30 activity prompts and you do not want to copy-paste them into Padlet one by one.

That is the problem this guide solves. You will put your activity prompts in a spreadsheet, run one careful check, and then publish them to a Padlet board as new posts.

This is useful when you prepare seminar questions, starter activities, tutorial prompts, reading responses, exit tickets, or weekly discussion boards.

This guide is for educators. You do not need to understand web development. The main idea is simple:

> One row in your spreadsheet becomes one post on your Padlet board.

The example code is available on GitHub: [riasatislam/padlet-bulk-publish](https://github.com/riasatislam/padlet-bulk-publish).

## What This Guide Does

This guide shows how to create new Padlet posts in bulk.

It does not update or delete existing Padlet posts. Padlet's official public API documentation includes endpoints for creating posts and retrieving board data, so this workflow is best understood as seeding or republishing activity prompts, not editing old posts.

## Official Padlet Documentation Used

These are the real Padlet documentation pages this guide is based on:

- [Padlet Public API help article](https://padlet.help/l/en/article/3933026qoo-public-api)
- [Padlet API introduction](https://docs.padlet.dev/reference/introduction)
- [Padlet authentication](https://docs.padlet.dev/reference/authentication)
- [Create a post endpoint](https://docs.padlet.dev/reference/add-post)
- [Get board by ID endpoint](https://docs.padlet.dev/reference/get-board-by-id)
- [Error handling and rate limiting](https://docs.padlet.dev/reference/error-handling)

The important points are:

- Padlet has a public API that can send posts to boards.
- You need API access and an API key.
- Your API key is sent in the `x-api-key` request header.
- You need administrator access to the Padlet board.
- New posts are created with the `POST /v1/boards/{board_id}/posts` endpoint.
- Padlet documents common error codes and a rate limit.

## What You Need

Before starting, make sure you have:

- A Padlet account with Public API access.
- Administrator access to the board you want to fill.
- Your Padlet API key.
- The board ID for the Padlet.
- Python installed on your computer.
- A copy of the example GitHub repo: [riasatislam/padlet-bulk-publish](https://github.com/riasatislam/padlet-bulk-publish).

If you are unsure whether your account can use the API, open your Padlet Developer settings and check whether you can generate an API key. Padlet's own pages describe API access and account requirements; where the wording differs between pages, your own Developer settings are the source of truth.

## Step 1: Make Your Spreadsheet

Create a CSV file. CSV is a plain spreadsheet format that Excel, Google Sheets, and Numbers can export.

Use these column names:

```csv
row_id,subject,body,attachment_url,attachment_caption,color
q1,Starter question,"What is one example of learning by trial and error?",,,blue
q2,Pair discussion,"Compare supervised learning and reinforcement learning in two bullet points.",,,green
q3,Useful link,"Open the reading before answering the prompt.",https://example.com/reading,Course reading,purple
```

What each column means:

| Column | What to put there |
| --- | --- |
| `row_id` | A short unique ID, such as `q1` or `week2-starter`. Keep this the same if you run the tool again. |
| `subject` | The Padlet post title. |
| `body` | The main activity instructions. |
| `attachment_url` | Optional link to attach to the post. |
| `attachment_caption` | Optional label for the link. |
| `color` | Optional Padlet color: `red`, `orange`, `green`, `blue`, or `purple`. |

You can leave optional cells blank.

## Step 2: Download the Example Repo

Open Terminal on Mac, PowerShell on Windows, or the terminal in your code editor.

Download the example repo from GitHub: [riasatislam/padlet-bulk-publish](https://github.com/riasatislam/padlet-bulk-publish).

Install the example:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -e .
```

On Windows PowerShell, the activation command is usually:

```powershell
.\.venv\Scripts\Activate.ps1
```

## Step 3: Add Your Padlet Details

Copy the example settings file:

```bash
cp .env.example .env
```

Open `.env` and fill in:

```bash
PADLET_API_KEY=your_api_key_here
PADLET_BOARD_ID=your_board_id_here
```

Keep this file private. Do not upload it to GitHub.

## Step 4: Do a Dry Run

A dry run is a practice run.

It checks your spreadsheet and shows what would be posted, but it does not post anything to Padlet.

```bash
padlet-bulk-publish publish \
  --csv examples/activities.csv \
  --state published-posts.json \
  --dry-run
```

Read the preview. Check that the titles, instructions, links, and colors look right.

## Step 5: Publish to Padlet

When the dry run looks correct, publish for real:

```bash
padlet-bulk-publish publish \
  --csv examples/activities.csv \
  --state published-posts.json \
  --execute
```

The tool will create one new Padlet post for each valid row in the spreadsheet.

It will also create a local file called `published-posts.json`. This file records which spreadsheet rows have already been published.

## Step 6: Run It Again Safely

If you run the same command again, the tool will skip rows that were already published.

That matters because Padlet post creation is not the same thing as editing. If the tool created every row every time, you would get duplicates.

If you change a row after publishing, the tool reports that it changed and skips it. That is intentional. Review the changed row and decide whether to manually edit the Padlet post or publish a new version.

Use `--force` only if you deliberately want changed rows to be posted again as new posts.

## Troubleshooting

| What you see | Likely cause | What to do |
| --- | --- | --- |
| `INVALID_API_KEY` | The API key is wrong or was refreshed. | Copy the current key from Padlet Developer settings. |
| `NOT_ADMIN` | You are not an administrator of the board. | Use a board you created or ask to be added as an administrator. |
| `NOT_PAYING_USER` | The account cannot use the public API. | Check your Padlet plan or Developer settings. |
| `PADLET_ARCHIVED` | The board is archived. | Unarchive the Padlet before using the API. |
| `PARAMETER_MISSING` or `BAD_REQUEST` | A spreadsheet row is missing required content or has an invalid value. | Check that each row has a title, body, or attachment URL. Check the color spelling. |
| `RATE_LIMIT_EXCEEDED` | Too many API requests were sent too quickly. | Wait a minute and run the command again. |
| `NOT_FOUND` | The board ID is wrong or the board is unavailable to your account. | Recheck the board ID from Padlet. |

## Safety Checklist

Before using this with a live class board:

- Test with a private practice Padlet.
- Run a dry run.
- Check every row in the preview.
- Keep your API key private.
- Keep your `.env` file out of GitHub and shared folders.
- Keep the `published-posts.json` file so reruns do not create duplicates.

## When This Workflow Helps Most

This workflow is most useful when:

- You already write activities in a spreadsheet.
- You need to seed many prompts at once.
- You revise activities before each semester.
- You reuse a board structure but change the content.
- You want a repeatable process instead of manual copying.

For small one-off changes, editing directly in Padlet may still be faster.

## Final Reminder

Treat the spreadsheet as your source copy. Treat Padlet as the published classroom space.

Run a dry run first, publish only when the preview looks right, and keep the state file so you do not accidentally create duplicate posts.
