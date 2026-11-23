---
name: check-app-data
description: Read and change the records of an app hosted on Inference Bureau, run its actions and read its recent events, to check what code does to real data. Use when the user asks about an Inference Bureau app's data, its models, or why a request, job or webhook failed.
---

# Check an app's data

Every app on Inference Bureau has environments (development, production and any others), each with its own models,
records, actions and event log. Each tool names the app (`app`, its slug) and the environment (`environment`).

- Start with `list_apps` if you don't know the app's slug, then `list_models` for its models and their fields.
  In an app's checkout, `.ib/sync.json` (written by the `ib-apps` CLI) names its `app` and `env`.
- Read with `find_records`, `get_record`, `count_records` and `aggregate_records`. Filters use the model's field
  names; a relationship can be filtered through (`consignor.name`).
- `list_events` shows the environment's recent requests, jobs, webhooks, deploys and errors. Start there when
  something failed.
- Work in development unless the user says otherwise. Production is the live app: a write there reaches real
  users at once. Before `create_record`, `update_record`, `delete_record` or `run_action` on production, say what
  will change and wait for the user to agree.
