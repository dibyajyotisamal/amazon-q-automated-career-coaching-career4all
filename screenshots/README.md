# Screenshots – Documentation and Rubric Mapping

This folder contains all screenshots required for the “Amazon Q Automated Career Coaching – Career4All” project.  
Screenshots are organized according to the project rubric.  
Each screenshot filename is listed below along with a clear description of what it represents.

---

## 1. Create and Customize Amazon Q Application

| File Name | Description |
|----------|-------------|
| app_basic_interface.png | Shows the basic Q App interface with CV Upload, Job Profile Upload, Skill Gap Analysis, and Training Recommendation cards. |
| app_advanced_interface.png | Shows the enhanced interface with Learning Schedule output card and Coach Recommendation input card. |
| app_advanced_interface_with_results.png | Shows the Q App after generating results from uploaded CV and Job Profile. |
| skill-gap-analysis-prompt.png | Shows the exact prompt used for the Skill Gap Analysis output card. |
| training_recommendation-prompt.png | Shows the exact prompt used for the Training Recommendation output card. |
| training-schedule-prompt.png | Shows the exact prompt used for the Learning Schedule output card. |

---

## 2. Upload Static PDF and Connect Amazon S3

| File Name | Description |
|----------|-------------|
| data_source_pdf_sync.png | Shows the manually uploaded PDF course catalog successfully synced in Amazon Q Business. |
| data_source_s3_files.png | Shows the S3 bucket and the static course catalog files stored inside it. |
| data_source_s3_sync.png | Shows the successful sync of the S3 data source. |
| data_source_s3_daily_sync.png | Shows the daily sync configuration and next scheduled sync time. |
| data_sources_overview.png | Shows all connected data sources with their most recent sync timestamps. |

---

## 3. Secure the Application (ACL and Guardrails)

| File Name | Description |
|----------|-------------|
| data_source_acl_configuration.png | Shows the ACL configuration attached to the S3 data source. |
| acl_access_allowed.png | Shows `career.coach.two` successfully accessing restricted Medicine catalog content. |
| acl_access_denied.png | Shows `career.coach.one` being denied access to Medicine catalog content. |
| blocked_words_configuration.png | Shows the Global Controls configuration with blocked keywords: Gambling, Casino, Self-harm, Attack. |
| topic_specific_controls.png | Shows the topic-level blocking rule for Self-harm with example messages and block behavior. |

---

## 4. Publish and Share the Application

| File Name | Description |
|----------|-------------|
| app_sharing_and_labels.png | Shows the application shared with required users and custom labels applied. |
| app_verified_status.png | Shows the final application marked as a Verified Q App. |

---

## Folder Structure

The screenshots are organized as follows:

    screenshots/
      Create and Customize Amazon Q Application/
      Upload Static PDF and Connect Amazon S3/
      Secure the Application/
      Publish and Share the Application/

