---
name: setmore
description: Use for anything about the user's Setmore account - their calendar and agenda, meetings, appointments and bookings, free time, time off, customers, services, booking settings, and Setmore Connect team messages. Triggers on requests like "what's on my calendar today", "book Jane for a haircut Friday at 4", "find 30 minutes with Kevin and Priya next week", "block Friday off", "any unread messages?", "reply to Priya". Use the Setmore tools for these instead of writing code or calling an API directly.
---

# Setmore

This plugin connects Grok to the user's Setmore account through Setmore's hosted MCP server, named `setmore`. This skill covers how to reach those tools in Grok Build.

How to use each tool (looking people up, timezones, sensible defaults, confirmations) is in the Setmore server's own instructions and tool descriptions. Follow them. They are the source of truth and win over anything here.

## Reaching the tools

- Setmore tools aren't loaded up front. Find them with `search_tool` ("setmore" plus the capability, e.g. "setmore agenda", "setmore available slots"), then call them with `use_tool` by full name, e.g. `setmore__get_agenda`.
- The first call opens a browser to sign in to Setmore. If a call fails because the user isn't signed in, ask them to finish signing in, then retry once. If it still fails, point them to the Setmore server in `/mcps`.

## What to search for

| The user wants | Tools |
|---|---|
| Their day or week, next meeting, earlier meetings | `get_agenda` |
| A time that works, for them or for several people | `fetch_available_slots`, `find_common_slots` |
| A meeting with teammates or a customer guest | `search_staff` or `search_customers`, then `create_appointment` |
| A customer booked for a service | `search_customers`, `list_services`, `book_service` |
| To move, edit or cancel something | `reschedule_appointment`, `update_appointment`, `cancel_appointment` |
| Time off | `block_time` |
| A link for someone to pick a time | `create_sharable_slot` |
| Customer details | `search_customers`, `get_customer`, `create_customer`, `update_customer` |
| What was booked, rescheduled or cancelled since last check | `get_booking_events` |
| Numbers and plan usage | `booking_stats`, `get_billing_usage` |
| Services and settings (owners and admins only) | `create_service`, `update_service`, `assign_service_staff`, `delete_service`, `get_settings`, `update_booking_settings`, `update_notification_settings`, `update_working_hours`, `list_integrations` |
| Connect team messages | `get_unread_messages`, `read_messages`, `search_messages`, `send_message`, `react_to_message`, `mark_as_read`, `mark_as_unread`, `get_connect_events`, `get_presence`, `list_channels`, `get_collab_members`, `add_collab_members`, `create_collab` |
| Realtime and push updates (only when user asks) | `list_event_subscriptions`, `create_event_subscription`, `enable_event_subscription`, `delete_event_subscription` |

If `search_tool` doesn't find something listed here, try the server's `find_new_tools` with the capability name, then `call_new_tool` if it's read-only. Only if that doesn't help, tell the user the capability isn't available. Never guess tool names.

## Ground rules

These hold even if the server's instructions aren't in view.

- Look things up rather than asking. "Me" is the signed-in user. Ids, durations, prices and the user's timezone all come from the tools.
- Tools already answer in the right timezone. Never convert times yourself. Never show ids, raw timestamps or field names.
- Before any write (booking, change, cancellation, customer edit, settings change, sending a message), show a one-line summary and wait for a clear yes.
- Service and settings tools refuse staff accounts. Say so once, and don't retry.

## Not available yet

Reminders, classes, and editing or deleting Connect messages. Say so in one line and point the user to the Setmore app.
