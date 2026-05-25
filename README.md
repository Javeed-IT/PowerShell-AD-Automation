# PowerShell AD Automation Lab

## Overview
A collection of PowerShell scripts built to automate 
common Active Directory tasks in an enterprise environment.
Built and tested against a live Windows Server domain 
(ITSERVICES) running in Parallels Desktop on macOS.

## Technologies Used
- PowerShell 5.1
- Active Directory Module for Windows PowerShell
- Windows Server (Parallels VM)
- Domain: ITSERVICES.LOCAL

## Scripts

### 1. New-BulkUsers.ps1
Reads a CSV file and automatically provisions multiple 
AD user accounts in one run.

**What it does:**
- Reads user data from new-users.csv
- Builds username from first initial + last name
- Places each user in the correct OU by department
- Sets default password with forced change at logon
- Confirms each creation in console

**Real world use:** HR sends a spreadsheet of new starters.
Instead of creating 20 users manually, one script handles 
all of them in seconds.

**Result:** 5 users created across 3 OUs in under 5 seconds

---

### 2. Reset-UserPassword.ps1
Automates the most common helpdesk task — password resets.

**What it does:**
- Accepts a username as input
- Resets password to temporary value
- Unlocks the account
- Forces password change at next logon
- Writes timestamped entry to audit log

**Real world use:** User calls helpdesk locked out.
One command resets, unlocks, and logs — fully auditable
for ISO 27001 compliance.

**Audit log sample:**
2026-05-25 00:41:37 - Password reset completed for: sahmed
2026-05-25 00:49:17 - Password reset completed for: jwilson
2026-05-25 00:49:43 - Password reset completed for: ppatel

---

### 3. Invoke-DeviceOnboarding.ps1
Automates device onboarding when a new PC joins the domain.

**What it does:**
- Verifies computer exists in AD
- Verifies assigned user exists in AD
- Moves computer to correct OU based on department
- Logs full onboarding record with timestamp

**Real world use:** New employee starts Monday.
IT runs this script — device is moved to the correct OU,
assigned to the correct user, and the action is logged.

**Result:** CLIENTPC moved from Workstations to 
Finance Team OU and logged in under 3 seconds.

---

## Screenshots
[See /screenshots folder]

## Key Learnings
- PowerShell follows Verb-Noun syntax for every command
- Mandatory parameters make scripts interactive and safe
- Audit logging is essential for compliance — every 
  action should be timestamped and recorded
- Running scripts requires admin privileges in AD
  environments — always run as Domain Admin for 
  user/computer management tasks

## Next Steps
- Add email notification on password reset
- Add error handling for duplicate usernames
- Build a GUI wrapper using Windows Forms

