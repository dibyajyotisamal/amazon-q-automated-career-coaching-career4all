# Architecture Overview - Career4All Automated Career Coaching System

This document provides a high-level overview of the system architecture for the Career4All automated career coaching application built using Amazon Q Business.

---

## 1. Core Components

### **Amazon Q Business Application**
- Primary AI-driven interface for coaches.
- Handles skill gap analysis, training recommendations, and schedule generation.
- Uses input/output cards as modular components.

### **Q App Web Experience**
- Provides the UI where users upload CVs, job profiles, and view results.
- Integrates coach override input and learning schedule generation.

### **Data Sources**
- **PDF Course Catalog** (manually uploaded)
- **Amazon S3 Bucket** containing additional course catalogs
- Both sources are indexed by Amazon Q Business to support recommendations.

### **IAM Identity Center**
- Group: `CareerCoaches`
- Users: `career.coach.one`, `career.coach.two`
- Access to course content is controlled based on this identity configuration.

### **ACL (Access Control List)**
- JSON configuration applied to the S3 data source.
- Controls access to restricted course catalogs based on coach expertise.

### **Guardrails (Content Moderation)**
- Blocks restricted terms such as: Gambling, Casino, Self-harm, Attack.
- Ensures clean and compliant recommendation output.

---

## 2. Data Flow Overview

1. **User uploads CV + job profile -> Q App**
2. **Skill gap analysis output card processes text**
3. **Training recommendation card retrieves courses from:**
   - PDF catalog
   - S3 catalog
4. **Amazon Q LLM generates personalized recommendations**
5. **Learning schedule card creates a weekly plan**
6. **Coach input modifies response (override mechanism)**
7. **ACL filters out unauthorized catalog content**
8. **Guardrails block restricted keywords**
9. **Final output shown to the Career Coach**

---

## 3. Region & Deployment Notes
- All components deployed in the same AWS region for compatibility.
- S3 must be in the same region as the Q Business application.
- IAM Identity Center must match the region selection for Q Business.

---

## 4. Future Extension Possibilities
- Custom Q Web App theme (branding).
- Outlook integration for automated schedule reminders.
  
