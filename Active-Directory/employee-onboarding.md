# New Employee Onboarding — Helpdesk SOP

**Category:** Active Directory — User Account Management  
**Ticket Type:** Service Request  
**Priority:** Medium  
**Environment:** Windows Server 2022, Active Directory, Jira  

---

## Overview

New employee onboarding is one of the most common Service Requests a Tier 1 helpdesk technician handles. When a new employee joins the company, IT is responsible for creating their domain account, placing them in the correct Organizational Unit, adding them to the appropriate Security Group, and securely communicating their credentials before their first day.

> **Note:** This is a Service Request, not an Incident. No service has been disrupted — this is a planned, expected request fulfilled on behalf of a new employee.

---

## Scenario

**New Employee:** Sarah Johnson  
**Department:** Finance  
**Request:** HR has submitted a ticket requesting Sarah's domain account be created and configured before her first day on Monday.  
**Ticket:** KAN-X — *New Employee Onboarding - sarah.johnson Finance Department*  
**Priority:** Medium — planned request with a known deadline

<img width="2862" height="1558" alt="Screenshot 2026-05-18 193721" src="https://github.com/user-attachments/assets/a22ee6ba-0219-4b7c-99e4-3cc29dafccae" />

---

## Resolution Steps

### Step 1 — Acknowledge the Ticket

As soon as the ticket comes in, reply to acknowledge it and let the requester know it is being worked on.

> *"Hi, I've received the onboarding request for Sarah Johnson and will get her account set up right away. I'll update this ticket once everything is configured."*

Assign the ticket to yourself and move it from **To Do** to **In Progress** so other IT team members know this ticket is actively being worked and do not duplicate effort.

---

### Step 2 — Review the Ticket Before Asking Questions

Before reaching out for more information, read the ticket description carefully. In this case the ticket already tells us:

- New employee name — Sarah Johnson
- Department — Finance
- Start date — Monday

Because the ticket contains all the information needed, there is no need to ask follow up questions. If a ticket comes in with just a name and no other context — no department, no start date — then you would need to ask for more details before proceeding.

> **Good habit:** Always read the full ticket before asking questions. Asking for information that is already in the ticket wastes everyone's time.

---

### Step 3 — Create the User Account in Active Directory

1. On the Domain Controller, open **Server Manager → Tools → Active Directory Users and Computers**
2. Navigate to the correct OU — in this case Finance → Finance-Users
3. Right-click **Finance-Users** → **New** → **User**

<img width="1019" height="768" alt="Screenshot 2026-05-18 195325" src="https://github.com/user-attachments/assets/d0a8add2-1b51-408a-9d8a-9a22afa7d670" />


4. Fill in the user information in the New Object — User prompt:
   - **First name:** Sarah
   - **Last name:** Johnson
   - **User logon name:** `sarah.johnson` — naming convention in most environments is first.last, f.last, or first.l. Use whatever your organization's standard is.

<img width="1018" height="764" alt="Screenshot 2026-05-18 195652" src="https://github.com/user-attachments/assets/07f51a05-0353-410e-8b75-4424354e1686" />


5. Click **Next** to proceed to the password section
6. Set a temporary password — e.g. `Temp@123!`
7. Ensure **User must change password at next logon** is checked

<img width="1022" height="770" alt="Screenshot 2026-05-18 195939" src="https://github.com/user-attachments/assets/bb6ca893-57d8-43d9-bf23-e90398da6fb2" />


> ⚠️ Always check **User must change password at next logon**. This forces Sarah to create her own password on first login. Never let a temporary password become permanent — this is a security risk.

8. Click **Finish** to create the account

---

### Step 4 — Add Sarah to the Correct Security Group

OU placement controls which GPOs apply to Sarah. Security Group membership controls which resources she can access — such as shared folders and drives. Both steps are required.

There are two ways to add a user to a Security Group:

**Method 1 — Through the Security Group**
1. Locate the **Finance-Team** Security Group in AD
2. Right-click → **Properties** → **Members** tab → **Add**
3. Type `sarah.johnson` and click **OK**
4. Click **Apply** → **OK**

<img width="1022" height="769" alt="Screenshot 2026-05-18 200608" src="https://github.com/user-attachments/assets/0e1e836a-f5e7-42e5-8bfb-396b476e0759" />
 

**Method 2 — Through the User**
1. Right-click **Sarah Johnson** → **Add to a group**
2. Type `Finance-Team` and click **OK**

> **Note:** Either method works. Method 1 is useful when adding multiple users to a group at once. Method 2 is faster for a single user.

---

### Step 5 — Communicate Credentials Securely

Once the account is fully configured, Sarah's credentials need to be communicated to her securely:

- **Username** → communicate via ticket or email
- **Temporary password** → communicate verbally via phone call or in person only — never in writing

> ⚠️ In an onboarding scenario, Sarah hasn't started yet so you may not be able to reach her directly. In that case, coordinate with HR or her manager to ensure credentials are delivered securely before her first day.

Add a public reply to the ticket:

> *"Sarah's account has been created and configured. Her username has been included below. Her temporary password will be communicated via phone or delivered in person before her first day. She will be prompted to set a new password on first login."*

Add an internal note documenting what was done:

> **[Internal Note]** — "Created sarah.johnson in Finance-Users OU. Added to Finance-Team Security Group. Temporary password communicated via [phone/in person]. User must change password at next logon is enabled."

---

### Step 6 — Resolve the Ticket

Move the ticket from **In Progress** to **Resolved** once the account is fully configured and credentials have been communicated.

> ⚠️ Do not move to **Closed** yet. The ticket should remain in Resolved until Sarah logs in successfully on her first day and confirms everything is working. Once confirmed, close the ticket with a final note.

<img width="2879" height="1553" alt="Screenshot 2026-05-18 202914" src="https://github.com/user-attachments/assets/63d23e81-4c3e-4d46-bc9c-3de67b2302e6" />


Final closing note once Sarah confirms:

> *"New employee Sarah Johnson confirmed successful login on first day. Account onboarding complete. Ticket closed."*

---

## Important Distinctions

**OU Placement vs Security Group Membership — These are not the same thing**

| | OU Placement | Security Group |
|---|---|---|
| **Controls** | Which GPOs apply to the user | Which resources the user can access |
| **Example** | Finance-Users OU → Finance GPOs apply | Finance-Team → access to Finance shared folder |
| **Both required?** | Yes — skipping either one will cause access issues |
