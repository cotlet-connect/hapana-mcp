# Hapana MCP server

Connect Hapana to ChatGPT, Claude and any AI agent through Cotlet.dev. Work in your own CORE and GROW login with 31 hosted operations for clients, memberships, classes, payments and messages. All 28 write operations ask for approval by default.

## What you can ask

> Show today's classes and their bookings.

> Find a member and show their memberships and payments.

> Run the member delinquency report.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps & Connectors → Create, with connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Settings → Connectors → Add custom connector, with URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Hapana tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

Run the included Python module with Python 3.10 or later:

```bash
python3 hapana_agent.py serve
```

Or with Docker:

```bash
docker build -t hapana-mcp .
docker run -i --rm -e COTLET_API_KEY hapana-mcp
```

Tools: `hapana_guide`, `hapana_status`, `hapana_open`, `hapana_read`, `hapana_click`, `hapana_type`, `hapana_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, with no third-party runtime dependencies. Clone this repository and run:

```bash
export COTLET_API_KEY="your-key"
python3 hapana_agent.py connect   # ready config for ChatGPT, Claude, Claude Code and Cursor
python3 hapana_agent.py status    # is Hapana ready in your Cotlet.dev account
python3 hapana_agent.py guide     # Hapana screens and sign-in link
python3 hapana_agent.py read      # open Hapana, read the page, close the browser
python3 hapana_agent.py tools     # list Cotlet.dev tools
python3 hapana_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Hapana users

**Which Hapana login should I use?**

Use your own CORE login with the permissions needed for the task. Add GROW in the same Cloud Browser for campaigns, bulk SMS and contact import or export.

**Which operations ask for approval?**

All 28 write operations ask for approval by default. The three read operations find clients, list sessions and run reports.

**Is Cotlet affiliated with Hapana?**

No. Cotlet.dev is independent and not affiliated with Hapana.

## Learn more

- [Hapana integration and hosted tools](https://cotlet.dev/integrations/hapana-api-mcp-server)

---

More: https://cotlet.dev/integrations/hapana-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=hapana

Request access: https://cotlet.dev/signup?app=hapana&utm_source=github&utm_medium=readme&utm_campaign=hapana

## Workflows on the hosted integration

The live integration page documents these 31 operations:

- `find_client`
- `add_client`
- `merge_clients`
- `manage_client_groups`
- `manage_leads`
- `send_workout_program`
- `update_membership_status`
- `update_package_credits`
- `edit_future_payments`
- `send_package_agreement`
- `process_sale`
- `membership_payment`
- `charge_no_show_fee`
- `send_invoice_email`
- `list_sessions`
- `add_session`
- `book_client`
- `check_in_client`
- `change_instructor`
- `bulk_cancel_sessions`
- `manage_schedule_templates`
- `configure_room`
- `manage_memberships_packages`
- `manage_promo_codes`
- `manage_pos_products`
- `send_bulk_message`
- `send_email_campaign`
- `send_bulk_sms`
- `import_export_contacts`
- `add_time_clock_entry`
- `get_report`

The local stdio adapter exposes seven browser helpers listed above. These helpers forward to Cotlet.dev; the workflow operations are documented on the hosted integration page.
