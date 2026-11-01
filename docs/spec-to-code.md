# From a booking specification to code

A successful conversation with an agent didn't guarantee the same context and rules would carry into the next run. I needed to specify what the software should do when a request arrived twice, when a worker stopped halfway through, or when a saved appointment didn't match the call.

This is a sanitized documentary summary of a private booking specification drafted with my Claude review agent and approved by me on October 27, 2026. It describes existing requirements, not new operating instructions, executable code, or passed test results.

## Separate interpretation from writes

The model's job is to extract a case from the full call transcript. Fields describing what was agreed on the call carry supporting quotations; unsupported fields remain blank. Existing business records come from their own system rather than being invented from the conversation.

Code owns the writes and their sequence. Each save is read back before the next step. That makes interpretation, action, and verification separate responsibilities.

## Turn failure scenarios into requirements

| Scenario | Required behavior in the approved specification |
| --- | --- |
| The same call notification arrives twice | Create the intended booking once, not a second booking for the duplicate notification. |
| The worker stops immediately after a save | On restart, find the saved record instead of creating another one. |
| A save reports a failure | Read the business system before deciding whether a retry is needed. |
| A visit has been saved | Check that its date, start time, arrival window, pet, service, and price match the source agreement and applicable requirements. |
| Filing the transcript fails after booking | Retry the filing step, not the booking. |

These are acceptance requirements. This table does not say the newer implementation has passed them.

## What I want to demonstrate

The useful engineering work is making the business process precise enough to implement and inspect. “Book the appointment” becomes a set of responsibilities with an observable result, including what recovery should do after an interruption.

The private specification has more business-specific detail. This excerpt leaves out client information, staff rules, prices, internal locations, and system access details.

[Back to the projects and current status](../PROJECTS.md)
