# Inference Bureau for Cursor

Brings [Inference Bureau](https://www.inferencebureau.com) into Cursor: Auditor's review findings on your pull
requests, and your apps' data.

## What it adds

- **MCP server** `inference-bureau` at `https://api.inferencebureau.com/mcp`. The first time Cursor uses it, it
  opens Inference Bureau in your browser: sign in and pick your team. It acts as you, with what your role in that
  team allows. You can see and sign out every session on your account page.
  - Auditor: `list_findings`, `get_finding`, `get_review`, `resolve_finding`.
  - Apps: `list_apps`, `list_recipes`, `create_app`, `create_environment`.
  - An app environment's data: `list_models`, `list_actions`, `find_records`, `get_record`, `count_records`,
    `aggregate_records`, `search_records`, `create_record`, `update_record`, `delete_record`, `run_action`,
    `list_events`.
  - Building an app, by app and environment: its files (`list_files`, `read_file`, `search_files`, `write_file`,
    `edit_file`, `delete_file`), models and fields, actions, roles, problems, tests, pages, integrations and
    `deploy`. Production's code changes only by `deploy`, which the agent calls only when you ask.
- **Skills**
  - `fix-auditor-findings`: works through the open findings on the checked-out branch's pull request, worst first,
    and marks each fixed or not to fix once you've seen the changes.
  - `check-app-data`: reads and changes an app's records and reads its events, in development unless you say
    otherwise.

## Setup

No key or variable to set: install the plugin and ask, for example, "Fix Auditor's findings on this branch" or
"Which items are still listed in my Consign app?". Cursor asks before running a tool that changes something.

Auditor needs its GitHub App installed on the repository. Apps need a team on Inference Bureau.

## Docs and support

- Connector docs: https://www.inferencebureau.com/docs/connectors
- Privacy: https://www.inferencebureau.com/privacy
- Contact: https://www.inferencebureau.com/contact

## License

MIT
