[title]: # "Using Inbox Rules"
[tags]: # "inbox rules"
[priority]: # "1000"

# Using Inbox Rules

## Overview

An inbox rule triggers on specific notification types and sends either an email or a Slack message to a specified group of users. 

### Rule Components

Inbox rules have the following components:

#### Message Types

This is the message types that the rule responds to.

#### Rule Conditions

Rule conditions are filters that define who receives the email or Slack message when a notification arrives. Conditions are matched with text string matching: equals, not equals, or regex. If no condition exists, the rule triggers for every message of the defined types. Condition types include:
==Please explain value vs display value. Does it apply to all conditions? It does appear in the their dropdown lists.==

- ActionType: Specific entities via text matching of the action's value or display value. Actions types vary by system inbox templates. For example, the standard email template includes:

  - Dependency Failure

  - Inbox Test Message

  - Secret Access Cancel Request

  - Secret Access Deny Request

  - Secret Changed

  - Secret Heartbeat Failed

- Container: Specific containers via text matching of the container name. Containers include ==CONTAINER TYPES==.

- Details: Specific text string in the details section. ==NEED EXAMPLE.==

- EntityType: Specific entities via text matching of the entity name or value. Entities include:

  - Dual Controls
  - Encryption
  - Engine
  - Export Secrets
  - Group
  - Import Secrets
  - IP Address Range
  - Licenses
  - Role
  - Role Permission
  - Script - PowerShell
  - Script - SQL
  - Script - SSH
  - Secret Policy
  - Secret Template
  - Privileged Behavior Analytics Configuration
  - Site
  - Site Connector
  - Unlimited Administrator
  - User Audit

- EventDetails: Specific event details via text matching of the event detail's value or display value. See [Event List](../../event-subscription-page/event-list/index.md).

- ItemName: Specific items via text matching of the item's value or display value.

- SubscriptionName: Specific subscriptions via text matching of the subscription's value or display value.

- User: Specific users via text matching of the username's value or display value.

- **Rule Subscribers:**  Who receives the action result (an email or Slack message). 
- **Rule Actions:** What actions the rule performs:
  - Send to an email address using a specific HTML template, which the user defines.
  - Send to Slack using a specific markdown template, which the user defines.


### Predefined System Rules

Secret Server ships with several predefined system rules. These rules can only be disabled or enabled. However, you can copy a system template to your own custom template and edit that.  This allows us to upgrade system rules without interfering with your customizations. The predefined system rules are:

- Dependency Failure
- Inbox Test Message
- Password Reset
- Secret Access Deny Request
- Secret Access Request
- Secret Changed
- Secret Heartbeat Failed
- Workflow Access Approval Request

## Procedure

