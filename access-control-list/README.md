# ACL File Structure

Amazon Q Business expects ACL files in the following structure:

```json
[
  {
    "keyPrefix": "s3://careercoach-additional-catalogs/Security/",
    "aclEntries": [
      {
        "Name": "CareerCoaches",
        "Type": "GROUP",
        "Access": "ALLOW"
      }
    ]
  },
  {
    "keyPrefix": "s3://careercoach-additional-catalogs/Medicine/",
    "aclEntries": [
      {
        "Name": "career.coach.one",
        "Type": "USER",
        "Access": "DENY"
      },
      {
        "Name": "career.coach.two",
        "Type": "USER",
        "Access": "ALLOW"
      }
    ]
  }
]

```
---
# Access Control List (ACL) Configuration - Documentation

This directory contains the Access Control List (ACL) configuration used in the Career4All automated career coaching project built with Amazon Q Business.  
The ACL enforces fine-grained access control over course catalog files stored in Amazon S3, ensuring that only authorized Career Coaches can access specific restricted training materials.

---

## 1. Purpose of This ACL

Career Coaches have different areas of expertise. Some course catalogs contain specialized or restricted content that should only be accessible to certain qualified users.

This ACL enables:

- ALLOW access to authorized catalogs for the `CareerCoaches` group  
- DENY access to restricted catalogs  
- Ensures Amazon Q only retrieves and recommends courses a coach is authorized to see  
- Enforces organizational compliance and data access boundaries  

---

## 2. How Amazon Q Business Uses This ACL

When indexing S3 content:

1. Amazon Q reads the ACL configuration file  
2. It applies ALLOW / DENY rules to the specified `keyPrefix` paths  
3. Users only see documents they are permitted to access  
4. Training recommendations automatically adapt to user authorization  

This ensures restricted course catalogs never appear in training suggestions for unapproved users.

---

## 3. File Included in This Directory

### `course_access_acl.json`

This ACL file defines the access rules applied to the S3 data source.

---

## 4. Where the ACL Is Applied

The ACL file is attached to the Amazon Q Business S3 data source inside:

**Amazon Q Business -> Applications -> CareerCoachAssistant -> Data Sources**

Setup performed:

1. Upload training catalogs to the S3 bucket  
2. Upload the ACL JSON file  
3. Attach the ACL file under **Access Control Configuration**  
4. Sync the data source to apply changes (mandatory)

---

## 5. Verification Steps

To confirm correct ACL behavior, the following procedure was used:

1. Log in using IAM Identity Center users:  
   - `career.coach.one`  
   - `career.coach.two`

2. Query training content from both allowed and restricted folders.

3. Expected outcomes:
   - Allowed catalog -> visible and included in recommendations  
   - Restricted catalog -> hidden or inaccessible, not referenced in any training suggestions  

Screenshots of both the allowed and denied scenarios are included in the `/screenshots` folder.

---

## 6. Common Pitfalls and Notes

- The S3 data source **must be synced** after uploading or modifying the ACL file  
- IAM Identity Center group names must match exactly  
- Prefix paths must be exact, including trailing slashes  
- ACL rules apply only to the data source they are attached to  
- Documents outside defined prefixes remain unrestricted

---

## 7. Security Notes

- Keep restricted content in dedicated S3 prefixes for clear rule separation 
- Track ACL versions through version control for auditing and rollback    
