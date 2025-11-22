# Data Sources Overview

This document describes all data sources integrated into the Career4All Career Coaching Assistant.

---

## 1. Overview of Data Sources

### **1. Manually Uploaded PDF Catalog**
- A static PDF course catalog is manually uploaded into Amazon Q Business.
- Indexed automatically once uploaded.
- Used by the Training Recommendation card to retrieve relevant courses.
- Sync records are shown in `data_source_pdf_sync.png`.

---

### **2. Amazon S3 Course Catalog**

An Amazon S3 bucket was created to store additional training catalogs.

Contents include:
- Additional static course catalogs
- Specialized training files (e.g., medical, security, advanced tech)

Benefits:
- Coaches can upload new catalogs directly
- S3 → Q Business index sync keeps training data fresh

---

## 2. Data Source Configuration

### Steps Followed:

1. Create S3 bucket  
2. Upload training catalog files  
3. Add S3 bucket as a data source in Q Business  
4. Attach ACL file to the S3 data source  
5. Sync the data source manually  
6. Enable daily scheduled sync

Screenshots:
- `data_source_s3_sync.png`
- `data_sources_overview.png`
- `data_source_s3_daily_sync.png`

---

## 3. Daily Sync Configuration

Daily sync ensures new catalogs added to S3 are indexed automatically.

- Sync frequency: **Daily**
- Configured inside:  
  **Q Business -> Applications -> Data Sources -> S3 bucket -> Edit -> Sync Run Schedule**
- Verified with `data_source_s3_daily_sync.png`

---

## 4. Retrieval Behavior

Amazon Q automatically:
- Searches both the PDF and S3 training catalogs
- Combines results during recommendation generation
- Respects ACL restrictions (users only get courses they’re allowed to see)

The training recommendations are therefore:
- Fresh
- Multi-source
- Personalized according to access privileges


