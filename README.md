# Security-Investigation-Report
# Banking SOC Investigation – Failed Authentication Analysis

## Project Overview

This project is a simulated **Banking SOC investigation** performed using **Splunk Enterprise** and the official **Splunk Boss of the SOC (BOTS) v3** dataset.

The investigation focused on Windows failed authentication events (Event ID 4625), with the goal of identifying potential brute-force activity, misuse of default accounts, and mapping the observed behaviour to the **MITRE ATT&CK** framework.

## Tools & Technologies

- Splunk Enterprise
- Splunk BOTS v3 Dataset
- Windows Security Event Logs
- MITRE ATT&CK Framework

## Investigation Summary

| Item                            | Result                                      |
|--------------------------------|---------------------------------------------|
| Total Failed Logon Events      | 5                                           |
| Most Notable Targeted Account  | Guest                                       |
| Failure Reason                 | Account currently disabled                  |
| Logon Type                     | 3 (Network Logon)                           |
| Source IP Address              | Not recorded                                |
| Privileged Accounts Targeted   | None                                        |
| Evidence of Successful Brute Force | Not observed                            |

## MITRE ATT&CK Mapping

| Observed Activity                          | Technique Name              | ID       | Tactic                  |
|-------------------------------------------|-----------------------------|----------|-------------------------|
| Failed authentication attempts            | Brute Force                 | T1110    | Credential Access       |
| Attempt to log on with Guest account      | Valid Accounts              | T1078    | Defense Evasion / Persistence |
| Network logon (Type 3)                    | External Remote Services    | T1133    | Initial Access          |

## Investigation Phases & Screenshots

### Phase 1: Initial Triage

**Total Failed Logons**

![Failed Logon Count](screenshots/01-failed-logon-count.png)

**Failed Logons Table**

![Failed Logon Table](screenshots/02-failed-logon-table.png)

**Failed Logons Over Time**

![Timechart](screenshots/03-timechart.png)

### Phase 2: Deep Investigation

**Detailed Event View (Guest Account)**

![Guest Account Event](screenshots/04-guest-account-event.png)

**Account & Failure Analysis**

![Account Analysis](screenshots/05-account-analysis.png)

**Overall Risk Level:** Low

## Recommendations

- Keep the Guest account disabled on all systems
- Create detection rules for failed logons against default accounts
- Ensure Source Network Address is captured in authentication logs
- Correlate failed and successful logons in future investigations

## How to Recreate This Investigation

1. Install Splunk Enterprise
2. Download and install the BOTS v3 dataset
3. Search using:

```spl
index=botsv3 EventCode=4625
