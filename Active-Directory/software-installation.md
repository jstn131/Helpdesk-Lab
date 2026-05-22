# Software Installation — Helpdesk SOP

**Category:** Software Deployment  
**Ticket Type:** Service Request  
**Priority:** Low  
**Environment:** Windows Server 2022, Active Directory, Jira, RDP  

---

## Overview

Software installation requests are one of the most common Service Requests a Tier 1 helpdesk technician handles. When a user requests a new application, IT is responsible for verifying the software is approved, confirming the machine meets system requirements, remotely installing the software on the user's machine, and confirming it works before closing the ticket.

> **Note:** This is a Service Request, not an Incident. The user is requesting something new — no service has been disrupted.

---

## Scenario

**User:** John Smith (`john.smith@homelab.local`)  
**Department:** Finance  
**Request:** User is requesting Notepad++ to be installed on CLIENT01 for daily work use.  
**Ticket:** KAN-X — *Software Installation Request - john.smith requesting Notepad++*  
**Priority:** Low — routine software request with no productivity impact

<img width="2878" height="1554" alt="Screenshot 2026-05-22 145931" src="https://github.com/user-attachments/assets/61a8d0dd-427d-40a8-abda-d29e1d034430" />

---

## Resolution Steps

### Step 1 — Acknowledge the Ticket

As soon as the ticket comes in, acknowledge the user and let them know it is being worked on.

> *"Hi John, I've received your request for Notepad++ and will get this installed for you shortly. Please stand by."*

Assign the ticket to yourself and move it from **To Do** to **In Progress** so other IT team members know this ticket is actively being worked and do not duplicate effort.

---

### Step 2 — Verify Software Approval and System Requirements

Before installing anything, two checks must happen:

**Check 1 — Is the software approved?**
Most enterprise environments maintain an approved software list. Only software on this list should be installed on company machines. Notepad++ is a widely trusted, open source text editor that is commonly approved in enterprise environments.

**Check 2 — Does the machine meet system requirements?**
Notepad++ is a lightweight application that runs on any modern Windows machine. CLIENT01 meets the system requirements with no concerns.

> ⚠️ Never install unapproved software on a company machine. If a user requests software that is not on the approved list, the request must be escalated for review before proceeding.

---

### Step 3 — Obtain the Installer

In a real helpdesk environment, software installers are sourced from the company's approved software repository or a centralized network share maintained by IT — not downloaded directly from the internet on the fly. The technician accesses this repository from within the remote session and runs the installer directly on the user's machine.

In this lab, the installer is placed in the **Finance-Folder shared drive** (`\\WIN-1FGEG1FMJLD\Finance-Folder`) so it can be accessed from CLIENT01 during the remote session.

---

### Step 4 — Remote Into the User's Machine

Since you are installing software on the user's machine — not your own — you need to remote in via RDP.

1. On the Domain Controller, open **Remote Desktop Connection** from the Windows taskbar
2. Enter the client machine name or IP address:
   - Machine name: `CLIENT01.homelab.local`
   - Or IP address: `192.168.10.2`

<img width="1018" height="765" alt="Screenshot 2026-05-22 151528" src="https://github.com/user-attachments/assets/024342c4-a23e-4904-a63d-dc6b9cb84d9a" />

3. Enter domain admin credentials when prompted
4. The user will receive a notification that an administrator is connecting — they will be signed out of their session
5. Once connected, confirm you are on the correct machine by checking the machine name displayed at the top of the RDP window

<img width="1021" height="770" alt="Screenshot 2026-05-22 152503" src="https://github.com/user-attachments/assets/64f2a1fc-2dc2-40c2-886c-9552ab6d4f9b" />

---

### Step 5 — Install the Software

From within the RDP session on CLIENT01:

1. Open **File Explorer** and navigate to the shared drive:
   ```
   \\WIN-1FGEG1FMJLD\Finance-Folder
   ```
2. Locate the Notepad++ installer
3. Run the installer and follow the installation prompts
4. Once installation is complete, open Notepad++ to verify it launches correctly

> ⚠️ Always verify the software opens and works correctly before disconnecting. Do not close the ticket based on installation alone — confirm it actually runs.

---

### Step 6 — Disconnect and Notify the User

Once the installation is verified:

1. Disconnect the RDP session
2. Add a public reply to the Jira ticket notifying john.smith:

> *"Hi John, Notepad++ has been successfully installed on your machine. Please log back in and confirm you are able to open the application. Let me know once confirmed and I'll close out this ticket."*

Add an internal note documenting what was done:

> **[Internal Note]** — "Notepad++ installed on CLIENT01 via RDP. Installation verified — application opens correctly. Awaiting user confirmation."

---

### Step 7 — Confirm and Close Ticket

Wait for john.smith to confirm Notepad++ is working on his end before closing the ticket.

> ⚠️ Do not close the ticket until the user confirms. If the user reports any issues after installation, reopen and troubleshoot before closing.

Once confirmed, add a closing note and move the ticket to **Closed**:

> *"User confirmed Notepad++ is working correctly. Software installation complete. Ticket closed."*

<img width="2879" height="1554" alt="image" src="https://github.com/user-attachments/assets/6b584ee8-464d-4e57-880d-35cd4b164240" />

---

## Key Takeaways

- Software installation is a **Service Request**, not an Incident
- Always **verify software is approved** before installing anything on a company machine
- Always **check system requirements** before proceeding
- Always **remote in via RDP** — you are installing on the user's machine, not your own
- Always **verify the software opens correctly** before disconnecting
- Always **wait for user confirmation** before closing the ticket
- Never install software that is not on the company's approved software list without escalating first
