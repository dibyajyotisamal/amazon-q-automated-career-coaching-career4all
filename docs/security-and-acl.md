# Security Model and ACL Configuration

This document describes how access to course catalogs is controlled in the Career4All Career Coaching Assistant.

## Identity Model

- IAM Identity Center Group: `CareerCoaches`
- Users:
  - `career.coach.one`
  - `career.coach.two`

These identities are used to test and verify access behavior.

## ACL Configuration

The S3 data source for course catalogs uses an ACL configuration file:

- Path: `acl/course_access_acl.json`

The ACL defines access at the `keyPrefix` level, allowing or denying access to specific folders for the `CareerCoaches` group. This ensures that only qualified coaches can view certain specialized catalogs while others remain hidden.

## Verification

We verified ACL behavior using the provided test users:

- **Allowed scenario:**  
  Authorized user can see courses in allowed prefixes.  
  Screenshot: `screenshots/acl_access_allowed.png`

- **Denied scenario:**  
  The same or other users cannot see restricted catalogs.  
  Screenshot: `screenshots/acl_access_denied.png`
