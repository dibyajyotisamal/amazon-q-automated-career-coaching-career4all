# Automating Career Coaching with Amazon Q Business (Career4All)

This repository documents an internal project for Career4All to automate the career coaching workflow using **Amazon Q Business**. The solution streamlines CV review, skill gap analysis, and training recommendations while enforcing **access control** and **content moderation** using AWS-native capabilities.

> Note: This repo contains configuration, prompts, ACLs, and documentation. It does not expose any proprietary course content or internal credentials.

---

## 1. Project Overview

### Business Context

Career4All is a career development platform that offers personalized coaching. Historically, coaches manually:

- Reviewed learner CVs  
- Compared them with job descriptions  
- Identified skill gaps  
- Recommended training from multiple catalogs  
- Built learning schedules

This process became **slow, manual, and difficult to scale** as the number of learners increased.

### Goal

Build an **AI-powered career coaching assistant** using **Amazon Q Business** that:

- Automates CV review and skill-gap analysis  
- Recommends relevant training programs from multiple catalogs (PDF + S3)  
- Generates a personalized learning schedule  
- Allows coaches to add tailored recommendations  
- Enforces **course-level access restrictions** and **keyword-based content moderation**

---

## 2. High-Level Architecture

The solution uses the following core components:

- **Amazon Q Business Application** : `CareerCoachAssistant`
- **Q App Web Experience:** multi-card interface for CV, job profile, skill gap analysis, recommendations, and schedule
- **Data Sources**
  - Manually uploaded **PDF course catalog**
  - **Amazon S3 bucket** for additional course catalogs
- **IAM Identity Center**
  - Group: `CareerCoaches`
  - Users: `career.coach.one`, `career.coach.two`
- **Access Control**
  - S3 data source with an **ACL configuration file** (`course_access_acl.json`)
- **Content Moderation**
  - **Global Controls / Guardrails** with restricted keywords  
    (e.g., `Gambling`, `Casino`, `Self-harm`, `Attack`)

See `docs/architecture-overview.md` for more detail.

---

## 3. Amazon Q App Design

### 3.1 Input Cards

The Q App interface includes the following input cards:

1. **CV Upload**
   - Type: File / text input  
   - Purpose: Provide the learner’s CV for analysis.

2. **Job Profile Upload**
   - Type: File / text input  
   - Purpose: Provide a target job description for comparison.

3. **Coach Recommendation (Override / Notes)**
   - Type: Text input  
   - Purpose: Allows Career Coaches to add manual recommendations or constraints that the assistant should incorporate.

### 3.2 Output Cards

The application generates three key outputs:

1. **Skill Gap Analysis**  
   - Output card summarizing:
     - Matched skills
     - Missing skills
     - Skills needing strengthening  
   - Prompt template stored in:  
     `prompts/skill_gap_analysis_prompt.txt`

2. **Training Recommendations**  
   - Output card listing:
     - Specific learning resources from the PDF and S3 catalogs
     - Mapped to the skill gaps  
   - Prompt template stored in:
     `prompts/training_recommendation_prompt.txt`

3. **Suggested Schedule**  
   - Output card generating:
     - A structured learning plan (e.g., weekly schedule, estimated duration)  
   - Prompt template stored in:
     `prompts/schedule_prompt.txt`

### 3.3 Basic & Advanced Interfaces

- `screenshots/app_basic_interface.png`:  
  Initial app with CV + Job profile + skill gap + recommendations.
- `screenshots/app_advanced_interface.png`:  
  Enhanced app including schedule output and coach recommendation input.

---

## 4. Data Sources

The project integrates multiple data sources into Amazon Q Business:

### 4.1 PDF Course Catalog (Manual Upload)

- A static **PDF course catalog** is manually uploaded into Amazon Q as a data source.
- Q indexes this document, making it retrievable for training recommendations.
- Verification:
  - Queries for training suggestions return results citing the PDF catalog.

Screenshot:  
- `screenshots/data_source_pdf_sync.png`

### 4.2 Amazon S3 Course Catalog

- An **S3 bucket** (same region as the Q app) is created to host additional training catalogs.
- Career Coaches can upload new course catalogs directly to this bucket.
- The bucket is added as a **data source in Amazon Q Business**.

Verification:

- `screenshots/data_source_s3_sync.png`:  
  Shows S3 data source and successful sync.
- `screenshots/data_sources_overview.png`:  
  Shows both PDF and S3 sources with last sync times.

See `docs/data-sources.md` for configuration details.

### 4.3 Daily Sync

- A scheduled **daily sync** is configured for the S3 data source to ensure new course files are indexed automatically.

Screenshot:
- `screenshots/data_source_s3_daily_sync.png`

---

## 5. Security & Access Control

### 5.1 Identity & Group Setup

The solution uses the existing IAM Identity Center configuration:

- **Group:** `CareerCoaches`
- **Users:** `career.coach.one`, `career.coach.two`

All testing and access verification is done using these provided identities, as required by the rubric.

### 5.2 Access Control List (ACL) Configuration for S3 Data Source

An S3 data source is protected using an **Access Control List (ACL) configuration file**, stored here:

- `access-control-list/course_access_acl.json`

The ACL file associates S3 `keyPrefix` paths with specific ALLOW / DENY rules for the `CareerCoaches` group, ensuring:

- Certain course catalogs are **visible only** to authorized coaches.
- Restricted catalogs (e.g., highly specialized or sensitive content) are **not visible** to unauthorized users.

Screenshots:

- `screenshots/acl_access_allowed.png` - Example of allowed course access.
- `screenshots/acl_access_denied.png` - Example of denied course access.

See `docs/security-and-acl.md` for detailed behavior.

---

## 6. Content Moderation (Keyword Blocking)

To maintain content integrity and comply with organizational policy, **Global Controls / Guardrails** in Amazon Q Business are used to block specific keywords in recommendations, including:

- Gambling  
- Casino  
- Self-harm  
- Attack  

These are configured under **Global Controls -> Blocked Phrases** so that any response containing these terms is blocked or replaced.

Screenshot:

- `screenshots/keyword_blocking_config.png`

Additional details in `docs/content-moderation.md`.

---

## 7. Sharing & Verification

### 7.1 Sharing the Application

The final application is:

- Shared with the appropriate users/groups (including `CareerCoaches`).
- Exposed as an internal tool for Career4All coaches.

Screenshot:

- `screenshots/app_sharing_and_labels.png`

### 7.2 Labels & Verified Q App

To increase discoverability and trust in the organization, the app is:

- Tagged with **custom labels** such as:
  - `Career Coaching`
  - `AI-powered`
  - `Internal Tool`
- Marked as a **Verified Q App**.

Screenshot:

- `screenshots/app_verified_status.png`

---

## 8. How to Use the Application (For Coaches)

A concise user guide is provided in:

- `docs/user-guide-for-coaches.md`

It covers:

- How to log in using IAM Identity Center.
- How to upload CV and job profile.
- How to interpret the skill gap analysis.
- How to review and modify training recommendations.
- How to use the suggested schedule with the learner.

---

## 9. Troubleshooting & Lessons Learned

Key operational learnings:

- **Data source sync is critical:**  Changes to ACLs or new course files are not reflected until the S3 data source is re-synced.
- Guardrail configuration can fail if the **system message** contains invalid characters (curly quotes, emojis, or control characters).
- Using a **separate ACL file** for restricted paths makes it easier to reason about access and debug issues.

Details and scenarios are captured in:

- `docs/troubleshooting-and-lessons-learned.md`

---

## 10. Future Enhancements

Potential future extensions:

- Custom branding and theming of the Q Web Experience (logo, colors, text).
- Integration with Outlook or calendar systems to:
  - Email recommendations
  - Schedule reminders and follow-ups.
- Role-based behavior:
  - Different flows or prompts for junior vs senior coaches.
  - More granular expertise-based course filtering.

---

## 11. Repository Contents Overview

- `README.md` : You are here. Main project overview.
- `/access-control-list/course_access_acl.json` : Access control file for restricted courses.
- `/prompts/*.txt` : Prompt templates used in the Q App output cards.
- `/docs/*.md` : Architecture, configuration, security, moderation, user guide, troubleshooting.
- `/screenshots/*.png` : Evidence for rubric: app UI, data sources, sync, ACL behavior, keyword blocking, sharing, and verification.


