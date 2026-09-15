# GetHandy

[Website](https://www.gethandy.app/)

## From finding help to finishing the job

GetHandy connects people who need a job done with people who can do it. I built the mobile and web workflow from posting a task and comparing quotes through hiring, Stripe payments and completion.

<img src="assets/gethandy-demo-poster.png" width="900" alt="GetHandy posted task with a TV-mounting demo image, title and description">

*Real app walkthrough using fictional demo data: task drafting, a separate posted example and image, quotes, a provider profile and sample review, scheduling, and Stripe test checkout. No real payment is made.*

[Download the narrated walkthrough — 54 seconds, MP4](https://github.com/TrackerXXX23/TrackerXXX23/raw/refs/heads/main/assets/gethandy-demo.mp4)

[Narration captions](assets/gethandy-demo.srt)

## My work

- Product design and the customer/provider workflow.
- Stripe API and webhook integrations, including signature checks, duplicate-event handling and transfer reconciliation before settlement retries.
- Voice task posting with LiveKit and GPT Realtime, turning a conversation into structured job details. Tested with real audio in staging.

## An engineering decision

A payment callback can arrive more than once. A transfer can also succeed before its database record is saved. I built processed-event checks and transfer reconciliation into the recovery flow so a retry checks what already happened before attempting more work.

The voice and settlement examples were tested in staging in July 2026. The video above demonstrates task drafting, a posted example, quote comparison, provider review, scheduling and the Stripe test payment form.

**Built with:** React Native, TypeScript, Supabase, PostgreSQL, Stripe and LiveKit.

[Back to projects](README.md)
