# Content Moderation - Keyword & Topic-Level Blocking

This document explains the content moderation configuration applied to the Career4All Career Coaching Assistant, including both keyword blocking and a custom topic-level rule for Self-harm.

---

## 1. Purpose

To ensure safe and compliant recommendations, the assistant must block any training content or responses containing the following categories:

- Gambling
- Casino
- Self-harm
- Attack

These controls prevent inappropriate or harmful topics from appearing in the AI-generated outputs.

---

## 2. Keyword Blocking (Global Controls)

Keyword blocking was configured under:

**Admin Controls -> Guardrails -> Global Controls -> Blocked Words**

The following keywords were added:

- Gambling
- Casino
- Self-harm
- Attack

If any output contains these keywords, Amazon Q Business suppresses or replaces the response.

Screenshot reference:  
`keyword_blocking_config.png`

---

## 3. Topic-Level Blocking: Self-harm (Custom Safety Rule)

A dedicated **Self-harm topic rule** was created to block harmful intent beyond simple keyword matches.

### Configuration Path
**Admin Controls -> Guardrails -> Topic Specific Controls -> Create Topic Control**

### Topic Name
`Self-harm`

### Example User Messages Included
I want to harm myself.
How can I hurt myself?
I feel like ending it.
I want to do something dangerous to myself.

### Behavior Selected
`Block`

### System Message Override Used
I’m sorry, but I can’t help with that request. If you are feeling distressed or unsafe, please reach out immediately to your HR wellness support team or an available internal counselor.

> This ensures responses involving self-harm intent are blocked safely, even if the keyword is not explicitly mentioned.

---

## 4. How Keyword Blocking and Topic Controls Work Together

| Rule Type             | What It Blocks                                              |
|----------------------|--------------------------------------------------------------|
| Blocked Keywords     | Explicitly banned words (e.g., “Casino”, “Gambling”)           |
| Self-harm Topic Rule | Underlying intent or similar phrasing (e.g., “I feel unsafe”) |

Together, these create a layered safety system:  
**keyword-level protection + intent-level detection.**

---

## 5. Impact on Training Recommendations

If a training resource contains a blocked keyword or resembles a blocked topic:

- It will not appear in recommendations  
- Results referencing restricted terms are filtered out  
- For topic-level triggers, a safety message replaces the output  

This ensures all training guidance remains appropriate and safe.

---

## 6. Future Enhancements

Potential improvements:

- Add more topic-level controls (e.g., violence, adult content)
- Expand keyword list based on compliance policy updates
