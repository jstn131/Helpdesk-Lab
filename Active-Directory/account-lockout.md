# Account Lockout — Helpdesk SOP

**Category:** Active Directory — User Account Management  
**Ticket Type:** Incident  
**Priority:** High  
**Environment:** Windows Server 2022, Active Directory, Jira  

---

## Overview

An account lockout occurs when a user is unable to log into their account after entering an incorrect password too many times. This triggers the account lockout policy configured in Active Directory, preventing further login attempts until an administrator manually unlocks the account.

> **Note:** In a real helpdesk environment, the user would submit this ticket themselves through a customer portal. For the purposes of this lab, tickets are created on the user's behalf to simulate real helpdesk scenarios.

---

## Scenario

**User:** John Smith (`john.smith@homelab.local`)  
**Department:** Finance  
**Issue:** User reports they are unable to log into CLIENT01. User believes they may have entered their password incorrectly multiple times.  
**Ticket:** KAN-2 — *Account Lockout - john.smith cannot log into workstation*

<img width="2879" height="1551" alt="Screenshot 2026-05-14 202603" src="https://github.com/user-attachments/assets/47f443c9-64ef-462d-83be-2a1817966e22" />

---

## Common Causes

- User entered incorrect password too many times
- Account lockout threshold set via Group Policy (e.g., locks after 5 failed attempts)
- A background application or cached credential attempting to authenticate with an old password

---

## How to Identify an Account Lockout

In Active Directory Users and Computers:

1. Locate the user account
2. Right-click → **Properties** → **Account** tab
3. If the **Unlock Account** checkbox is **checked**, the account is locked out
4. If the checkbox is grayed out or unchecked, the account is not locked — this may indicate a different issue such as a forgotten password requiring a password reset instead

---

## Resolution Steps

### Step 1 — Acknowledge the User

As soon as the ticket comes in, notify the user that you are actively working on their issue. Do not leave them without a response.

> *"Hi John, I've received your ticket and I'm currently investigating your account lockout. Please do not attempt to log in again until I confirm the issue is resolved."*

<img width="1852" height="1153" alt="Screenshot 2026-05-16 141706" src="https://github.com/user-attachments/assets/e16ba973-7ce4-44ef-926a-c6119c76a1d4" />


---

### Step 2 — Verify Identity

Before making any changes in Active Directory, verify that the person submitting the ticket is who they say they are. This is a critical step that many beginners overlook.

Ask the user one or more of the following:

- Employee ID
- Name of their direct manager
- A company-assigned security PIN

> ⚠️ Never make changes to a user account without verifying identity first. An unauthorized person could be attempting to gain access to someone else's account.

<img width="1860" height="1242" alt="Screenshot 2026-05-16 142143" src="https://github.com/user-attachments/assets/c75b7777-2eb0-4027-8b21-942797c36ee6" />


---

### Step 3 — Locate the User in Active Directory

1. On the Domain Controller, open **Active Directory Users and Computers**
2. Ask the user what department they are in to locate them quickly
3. Navigate to the correct OU — in this case `Finance > Finance-Users`
4. Locate **John Smith**

---

### Step 4 — Unlock the Account

1. Right-click **John Smith** → **Properties**
2. Click the **Account** tab
3. Locate the **Unlock Account** checkbox — if checked, the account is locked
4. **Uncheck** the Unlock Account checkbox
5. Click **Apply** → **OK**

<img width="1018" height="771" alt="Screenshot 2026-05-16 140816" src="https://github.com/user-attachments/assets/d53421c2-a04e-402e-b608-95f6c58f04ae" />

---

### Step 5 — Notify the User

Let John know his account has been unlocked and instruct him on next steps.

> *"Hi John, your account has been unlocked. Please restart your computer and attempt to log in. Let me know once you're back in and I'll close out this ticket."*

> ⚠️ Do not close the ticket until the user confirms they are able to log in successfully.

---

### Step 6 — Confirm Resolution and Close Ticket

Once John confirms he is able to log in:

1. Add a closing note to the Jira ticket documenting the resolution
2. Change the ticket status to **Closed**

> *"User confirmed successful login. Issue resolved via AD account unlock. Ticket closed."*

<img width="2879" height="1553" alt="Screenshot 2026-05-16 142504" src="https://github.com/user-attachments/assets/1a9dcec9-7452-4d01-94e1-8c8a01266f1e" />

---

## What If the Unlock Account Checkbox Is Not Available?

If the Unlock Account checkbox is grayed out or unchecked when you open the Account tab, the account is **not locked out**. This points to a different issue — most likely the user has forgotten their password or their password has expired. In that case a **password reset** procedure is required instead.

---

## Key Takeaways

- Always **acknowledge the user** immediately when a ticket comes in
- Always **verify identity** before making any AD changes — never skip this step
- The **Unlock Account checkbox being checked** is the visual indicator of a locked account in AD
- **Do not close the ticket** until the user confirms successful login
- **Document every action** taken inside the ticket in real time — acknowledgment, identity verification, steps taken, and resolution
