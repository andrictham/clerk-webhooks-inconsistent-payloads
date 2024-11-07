# clerk-webhooks-inconsistent-payloads

# About

This repository documents the discrepancies between those documented in the Clerk dashboard and the actual payloads received by Clerk.

It contains JSON files representing select Clerk webhook payloads, and covers the following events:

1. `user.created`
2. `user.updated`
3. `organization.created`
4. `organization.updated`
5. `organizationMembership.created`
6. `organizationMembership.updated`
7. `organizationMembership.deleted`

For each event, we’ve included two JSON files:

- **Documented** files contain the payloads that were documented by Clerk in the dashboard
- **Received** files contain the actual payloads that we received from Clerk

We’ve noticed the following discrepancies between the documented and received payloads:

- **➖ Missing fields**, that are documented but not included in the received payloads
- **➕ Additional fields** are included in the received payloads, but are not documented

As a consumer of the webhooks, we expect that both should be in sync, specifically:

1. The documentation to include fields that are sent in the actual payloads.

2. The received payloads to include fields that are documented in the dashboard.

Specific instances of these issues are documented in the [Issues](#issues) section below.

# Issues

All disceancies documented below are those nested in the `"data"` object of the payloads.

### 1. `user.created`

#### ➖ Documented Fields Missing from Received Payload

- birthday
- gender

#### ➕ Received Fields Not Documented

- banned
- locked
- passkeys
- has_image
- totp_enabled
- saml_accounts
- last_active_at
- mfa_enabled_at
- mfa_disabled_at
- backup_code_enabled
- delete_self_enabled
- lockout_expires_in_seconds
- create_organization_enabled
- verification_attempts_remaining
- legal_accepted_at
- email_addresses
  - reserved
  - created_at
  - updated_at
  - verification
    - attempts
    - expire_at

### 2. `user.updated`

Same issues as as [`user.created`](#1-usercreated)

### 3. `organization.created`

#### ➕ Received Fields Not Documented

- has_image
- private_metadata
- admin_delete_enabled
- max_allowed_memberships

### 4. `organization.updated`

Same issues as as [`organization.created`](#3-organizationcreated)

### 5. `organizationMembership.created`

#### ➖ Documented Fields Missing from Received Payload

- organization
  - created_by

#### ➕ Received Fields Not Documented

- role_name
- permissions
- organization
  - has_image
  - members_count
  - admin_delete_enabled
  - max_allowed_memberships
  - pending_invitations_count
- public_user_data
  - has_image
- public_metadata

### 6. `organizationMembership.updated`

Same issues as [`organizationMembership.created`](#5-organizationmembershipcreated)

### 7. `organizationMembership.deleted`

Same issues as [`organizationMembership.created`](#5-organizationmembershipcreated)
