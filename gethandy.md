# GetHandy

[Website](https://www.gethandy.app/)

## From finding help to finishing the job

GetHandy connects people who need a job done with people who can do it. I built the mobile and web workflow from posting a task and comparing quotes through hiring, Stripe payments and completion.

https://github.com/user-attachments/assets/66dbddaf-0c7f-4914-8259-5dca5cbddb9b

*Real app walkthrough using fictional demo data: task drafting, a separate posted example and image, quotes, a provider profile and sample review, scheduling, and Stripe test checkout. No real payment is made.*

**Watch the narrated walkthrough · 54 seconds**

[Narration captions](assets/gethandy-demo.srt)

## What I own

- The customer/provider workflow: posting work, comparing quotes, choosing a provider, scheduling and payment.
- Expo app implementation and Stripe integrations, including signed webhooks, duplicate-event checks and payout recovery.
- Voice task posting with LiveKit and GPT Realtime, turning a conversation into structured job details; tested with real audio in staging.

## Engineering case study: a payout succeeds, then the worker crashes

### The failure

Stripe can complete a transfer before the app saves its result. If the worker crashes in that gap, the database still looks unpaid. Retrying from that record alone can send the provider another payment.

A consistent request key helps Stripe recognize repeated requests, but it is not a permanent record of whether money moved. I added a check against existing transfers before a retry can create or defer a payout.

### The decision

The recovery path compares transfers associated with the task against the expected provider, currency and amount:

| What the check finds | What the worker does |
| --- | --- |
| A matching transfer | Reuses its ID and records the payout that already happened. |
| A transfer for a different amount | Stops the automatic payout path for reconciliation. |
| No matching transfer | Checks funding availability before creating or deferring the payout. |
| The transfer lookup fails | Leaves the work for another attempt without creating or deferring a transfer. |

The order matters. A successful transfer can reduce the available balance. Checking balance first could mistake an already-paid job for one that still needs a deferred payout.

**Tradeoff:** when the result is uncertain, recovery can take longer or require reconciliation. I prefer that delay to treating an unknown payment outcome as permission to send more money.

### How I checked it

On September 15, 2026, the two focused settlement unit-test suites passed **83 tests**. They cover the recovery decision and money calculations, including:

- Reusing a transfer left by a crashed run.
- Detecting an amount mismatch instead of silently treating the job as unpaid.
- Ignoring transfers for another provider or currency.
- Deferring an unfunded first attempt.
- Checking refund, retained-tax and payout calculations against worked examples.

These are local logic tests, not a live-money test or a guarantee against every duplicate-payment scenario. The settlement work was also tested in staging in July 2026. The video above demonstrates the customer journey through Stripe test checkout; it does not demonstrate the recovery scenario.

**Built with:** Expo, React Native, Expo Router, TypeScript, Supabase, PostgreSQL, Stripe and LiveKit.

## Website preview

<a href="https://www.gethandy.app/">
  <img src="assets/gethandy-website.jpg" width="720" alt="GetHandy website — Your to-do list, handled.">
</a>

<sub>Explore the GetHandy website</sub>

[Back to projects](README.md)
