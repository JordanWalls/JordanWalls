# What I'm building

I run Woofie's of North Fort Worth and work full time as a systems analyst. These projects come from work I need done in the business: helping someone choose a service, responding to an inquiry, getting a visit booked, and making sense of the notes afterward.

## Easy Booking: guided service requests

**Live:** [bookyournextgroom.com](https://bookyournextgroom.com)

I built Easy Booking with Codex.

A customer shouldn't need to know our service menu before asking for help. The site has separate paths for grooming and walks/sitting, with questions that help customers describe what they need.

The walks/sitting path includes a needs advisor. Choosing “I'm traveling” presents pet-sitting visits and overnight care, with explanations of the services. The grooming path collects pet and location details and supports more than one pet.

The important boundary is visible throughout: submitting a request does not confirm an appointment. Availability and pricing are confirmed before booking.

[See the walkthrough and design decisions](docs/booking-app-case-study.md)

## From agent-assisted operations to persistent software

I started by asking ChatGPT to rewrite lead responses and card-on-file explanations. That grew into using ChatGPT Work for full business workflows. The next run didn't always carry forward the same context or apply the same rules. I needed those requirements in persistent code rather than having to establish them again in each conversation.

Today, Minerva and Atlas take booking requests, and I confirm them. Tiro is the separate booking program I'm still building.

Codex built the server foundation and is now working alongside Cursor on Tiro. As of November 1, 2026, Codex is handling the server-side build and real-model Practice runs; Cursor has added extraction tracing. This work is still in progress.

### Historical results from the earlier server work

**Owner-reported, logs kept private.** These are my dated records of earlier work, not publicly reproducible production benchmarks.

- **October 15, 2026:** deployed intake collected email and SMS, and real inbound texts reached the coordination workflow. Its output was summaries and proposals, not automatic bookings.
- **October 16, 2026:** an owner-scoped live test program exercised the earlier booking executor against the actual scheduling system. Saved records were checked, and the test visits were cleaned up afterward.
- **October 19, 2026:** controlled, owner-scoped live acceptance of the earlier scheduling queue demonstrated booking-record creation, duplicate blocking, and restart recovery that found the existing saved record rather than saving it again.
- **October 19, 2026:** Google Maps components returned real provider results for traffic, future departures, route optimization, and address validation. These were component-level results, not proof that every booking checked travel.
- **October 19–21, 2026:** the vehicle-telemetry pipeline backfilled 560 real trips and received live events, including a trip-end event within seconds. Matching those trips to scheduled visits was not established.

These are dated results from the earlier server generation, not claims about today's uptime or acceptance of the newer booking build. The earlier scheduler was subsequently retired.

### Making the requirements concrete

The booking specification separates interpreting a call from writing business records. It also defines what must happen when a request is duplicated, a worker restarts, or a saved appointment differs from its source.

[Read the sanitized spec-to-code excerpt](docs/spec-to-code.md)

**Current status, November 1, 2026:** the newer booking workflow is in Practice mode, using sandbox/sample operating data rather than live customer bookings. The current work has not yet established a completed end-to-end backend booking. It is separate from the live customer-facing request site and my earlier agent-assisted work.

The operational code and client information remain private. I share the public-facing work and the decisions behind it here.
