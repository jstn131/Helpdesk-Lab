# Password Reset — Helpdesk SOP

**Category:** Active Directory — User Account Management  
**Ticket Type:** Incident / Service Request  
**Priority:** High  
**Environment:** Windows Server 2022, Active Directory, Jira  

---

## Overview

A password reset occurs when a user has forgotten their password and can no longer log into their account or workstation. This is one of the most common tickets a Tier 1 helpdesk technician will handle on a daily basis.

> **Note:** Password resets can be classified as either an Incident or a Service Request depending on the organization. Some classify it as an Incident since it is an unplanned disruption to the user's workflow. Others classify it as a Service Request since forgotten passwords are an expected, routine occurrence. In this lab it is treated as an Incident due to the unplanned nature of the disruption and the impact on the user's productivity.

> **Important:** A password reset is different from an account lockout. A password reset is when the user has forgotten their password entirely. An account lockout is when the user knows their password but has been locked out after too many failed attempts. These are two different procedures — do not confuse them.

---

## Scenario

**User:** John Smith (`john.smith@homelab.local`)  
**Department:** Finance  
**Issue:** User reports they have forgotten their password and are unable to log into CLIENT01. User has important deadlines, making this time sensitive.  
**Ticket:** KAN-X — *Password Reset Request - john.smith cannot log into workstation*  
**Priority:** High — unplanned disruption with productivity impact

<img width="2879" height="1559" alt="Screenshot 2026-05-17 002938" src="https://github.com/user-attachments/assets/be229927-9edb-47fd-ab0e-afb8d61846fa" />

---

## Resolution Steps

### Step 1 — Acknowledge the User

As soon as the ticket comes in, reply to the user immediately. Never let a user feel ignored, especially on a high priority ticket.

> *"Hello John, I am looking into your issue and we will get this resolved as quickly as possible. Please stand by."*

Move the ticket status from **To Do** to **In Progress** so other IT team members know this ticket is actively being worked and do not duplicate effort.

---

### Step 2 — Verify Identity

Before making any changes in Active Directory, verify the user's identity. This is a critical step — especially for password resets, since you are about to grant someone access to an account.

Ask the user a security question such as:

> *"Before we begin, I need to verify your identity. Could you please provide me with your Employee ID?"*

> ⚠️ Never reset a password without verifying identity first. An unauthorized person could be attempting to gain access to someone else's account.

Add an internal note to the ticket confirming identity was verified:

> **[Internal Note]** — "Identity verified via Employee ID. Proceeding with password reset."

---

### Step 3 — Locate the User in Active Directory

1. Ask the user what department they are in — this saves significant time in larger environments
2. On the Domain Controller, open **Active Directory Users and Computers**
3. Navigate to the correct OU — in this case `Finance → Finance-Users`
4. Locate **John Smith**

---

### Step 4 — Reset the Password

1. Right-click **John Smith** → **Reset Password**
2. Enter a temporary password — e.g. `Temp@123!`
3. Confirm the temporary password
4. Ensure **User must change password at next logon** is checked

<img width="1022" height="764" alt="Screenshot 2026-05-17 004209" src="https://github.com/user-attachments/assets/71556f10-98d0-4d93-816f-e27702c1d9cc" />

> ⚠️ Always check **User must change password at next logon**. This forces the user to create their own new password immediately upon login, ensuring you never know their final password.

---

### Step 5 — Communicate the Temporary Password

Add a public reply to the ticket:

> *"Hi John, your password has been reset. Please check your phone for the temporary password. You will be prompted to set a new password on your next login."*

Then **verbally communicate** the temporary password over the phone or in person:

> "Your temporary password is Temp@123! — you will be asked to set a new password when you log in."

> ⚠️ Never write the temporary password in the ticket or send it via email. Always communicate passwords verbally — phone call or in person only. This is best practice in all helpdesk environments.

Add an internal note confirming the password was communicated:

> **[Internal Note]** — "Temporary password communicated to user verbally via phone. Awaiting user confirmation of successful login."

---

### Step 6 — Confirm Resolution and Close Ticket

Wait for john.smith to confirm they were able to log in and set their new password successfully.

> ⚠️ Do not close the ticket until the user confirms successful login. If the user cannot log in with the temporary password, repeat Step 4.

Once confirmed, add a closing note and change the ticket status to **Closed**:

> *"User confirmed successful login and password change. Issue resolved via AD password reset. Ticket closed."*

<img width="1006" height="751" alt="Screenshot 2026-05-17 004705" src="https://github.com/user-attachments/assets/bc7a848c-f1b3-489a-8989-b250007bbd6f" />
 
<img width="2879" height="1552" alt="Screenshot 2026-05-17 005253" src="https://github.com/user-attachments/assets/579d20fc-30d4-4ded-8266-4fcf4616ca29" />


---

## Key Takeaways

- Always **acknowledge the user immediately** — never leave them waiting without a response
- Always **verify identity** before resetting any password — this protects both the user and the organization
- Always check **User must change password at next logon** — never let the temporary password become permanent
- Always **communicate the temporary password verbally** — never in writing or in the ticket
- Always **move the ticket to In Progress** when you begin working — so other technicians don't duplicate your work
- **Never close the ticket** until the user confirms successful login

---

## Password Reset vs Account Lockout — Key Distinction

| | Password Reset | Account Lockout |
|---|---|---|
| **Cause** | User forgot their password | Too many failed login attempts |
| **User knows password?** | No | Yes |
| **AD Action** | Right-click → Reset Password | Properties → Account → Uncheck Unlock Account |
| **Temporary password needed?** | Yes | No |
| **User must change password?** | Yes — check the box | No |
