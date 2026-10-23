---
platform: whatsapp
format: broadcast
constraints:
  max_chars: 4096
  image_ratio: null
  max_hashtags: null
---

# Best Practices: WhatsApp — Broadcast Message

## Format Rules

- Message length: under 300 words for broadcasts; under 150 words for promotional messages
- Character limit: 4096 characters per message
- WhatsApp Business API: supports text, images, documents, and approved message templates
- Template messages (HSM): must be pre-approved by Meta for outbound messaging to opted-in contacts
- Emojis: supported and expected — they increase readability and warmth in this channel
- Media: images (JPEG/PNG, max 5MB), documents (PDF, max 100MB), video (MP4, max 16MB)
- Opt-in: GDPR/LGPD compliance requires explicit opt-in before any broadcast

## Structure

```
[GREETING — personalized opener]
"Hi {first_name} 👋"

[CONTEXT — 1 sentence]
Brief, warm reference to why you're messaging

[CORE MESSAGE — 2–4 short paragraphs]
- One idea per paragraph
- Use line breaks generously
- Emojis for visual hierarchy (not decoration)
- Bold text: *bold* using asterisks

[CTA — single, clear action]
- "Reply YES to confirm"
- "Tap the link below"
- "Reply with your question"

[LINK or ATTACHMENT — if applicable]
[Brand sign-off or contact info]
```

## Guidelines

- **WhatsApp is the most intimate digital channel.** Write like a trusted contact, not a brand — formal marketing language kills response rates.
- Keep lines short — 1–2 sentences each. WhatsApp is read on mobile; long lines are exhausting.
- Use emojis as visual bullets and to convey tone, but avoid overloading (max 1–2 per paragraph).
- Response window: WhatsApp Business API allows messaging contacts within 24 hours of their last message; templates are required outside this window.
- Never send broadcast messages without explicit opt-in — WhatsApp bans accounts for spam complaints.
- Broadcast vs. group: broadcasts are sent individually (recipient sees it as a direct message); use groups only for community-style communication.
- Timing: avoid sending between 10 PM and 8 AM local time. Mid-morning (10–11 AM) and early evening (7–8 PM) see highest read rates.
- Always include an opt-out instruction: "Reply STOP to unsubscribe."

## Examples

**Promotional broadcast:**
```
Hi {first_name} 👋

It's [Brand Name] here.

We just launched something you asked for — and it's live today only. 🚀

✅ [Feature/Product name]
✅ [Key benefit 1]
✅ [Key benefit 2]

Available until midnight tonight.

👉 [link]

Questions? Just reply here.

— [Team Name]

_Reply STOP to unsubscribe._
```

**Appointment reminder:**
```
Hi {first_name},

Just a reminder that your appointment with [Name] is confirmed for:

📅 *{date}*
🕐 *{time}*
📍 *{location or link}*

Need to reschedule? Reply here and we'll sort it out.

See you soon! 😊
```
