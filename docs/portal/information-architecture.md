# Portal Information Architecture & Required Views

The portal must expose the same domain model used by backend APIs; UI labels must not hide important state distinctions such as issued vs delivered vs accepted.

## Primary navigation

~~~text
Dashboard
Customers
Sites
Devices
Licenses
├── Entitlements
├── Grants
├── Renewals
└── Trials
Marketplace
├── Features
├── Trial Requests
└── Purchase Requests
Releases
├── Feature Releases
├── Models
├── Dependencies
└── Release Channels
Deployments
├── Online Updates
├── Offline Exports
└── Installation Status
Capacity
├── Hardware Profiles
└── Assessments
Audit
~~~

## Customer/device Marketplace feature view

Required fields:
- feature name/code and description
- screenshots or approved visual assets where available
- release notes/current release
- product/OS/runtime compatibility
- capacity preview and recommendation
- current entitlement/allocation state
- trial eligibility and configured duration
- purchase/request-purchase action and request status
- dependency/model requirements
- device installation/health status

## Admin catalog view

Required fields/actions:
- feature code/name/description
- supported products/OS/architecture
- minimum hardware/runtime requirements
- dependencies
- current release and channel
- trial/commercial policy
- campaign configuration
- release status
- model associations
- marketplace visibility

## Device detail view

Show separately: registration status, license/grant status, commercial expiry, offline freshness, grace state, capacity state, installed release set, model inventory, last check-in, site assignments and active deployment jobs.

## Renewal view

Do not collapse lifecycle into a single 'renewed' flag. Display: Due Soon -> Requested -> Approved/Grant Issued -> Delivered/Imported -> Accepted/Active, plus Failed/Rejected and Expired/Restricted states.

## Audit UX

Every sensitive action should expose actor, timestamp, object/revision, reason, approval status and resulting state without exposing secret material.