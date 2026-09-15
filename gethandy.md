# GetHandy

[Website](https://www.gethandy.app/)

## From finding help to finishing the job

GetHandy connects people who need a job done with people who can do it. I built the mobile and web workflow from posting a task and comparing quotes through hiring, Stripe payments and completion.

https://github.com/user-attachments/assets/66dbddaf-0c7f-4914-8259-5dca5cbddb9b

*Real app walkthrough using fictional demo data: task drafting, a separate posted example and image, quotes, a provider profile and sample review, scheduling, and Stripe test checkout. No real payment is made.*

**Watch the narrated walkthrough · 54 seconds**

[Narration captions](assets/gethandy-demo.srt)

## My work

- Product design and the customer/provider workflow.
- Stripe API and webhook integrations, including signature checks, duplicate-event handling and transfer reconciliation before settlement retries.
- Voice task posting with LiveKit and GPT Realtime, turning a conversation into structured job details. Tested with real audio in staging.

## An engineering decision

A payment callback can arrive more than once. A transfer can also succeed before its database record is saved. I built processed-event checks and transfer reconciliation into the recovery flow so a retry checks what already happened before attempting more work.

The voice and settlement examples were tested in staging in July 2026. The video above demonstrates task drafting, a posted example, quote comparison, provider review, scheduling and the Stripe test payment form.

**Built with:** Expo, React Native, Expo Router, TypeScript, Supabase, PostgreSQL, Stripe and LiveKit.

## Website preview

<a href="https://www.gethandy.app/">
  <img src="assets/gethandy-website.jpg" width="720" alt="GetHandy website — Your to-do list, handled.">
</a>

<sub>Explore the GetHandy website</sub>

[Back to projects](README.md)
