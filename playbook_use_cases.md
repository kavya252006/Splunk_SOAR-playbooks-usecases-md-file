# Splunk SOAR — Playbook Use Cases Reference

> Platform: Splunk SOAR v8.5.0.248 | ~170 Playbooks | Community Repository

---

## Quick Reference Table

| # | Playbook Name | Category | What It Does |
|---|--------------|----------|-------------|
| 1 | Active_Directory_Disable_Account_Dispatch | Account Management | Disables an AD user account + generates report |
| 2 | Active_Directory_Enable_Account_Dispatch | Account Management | Enables/unlocks an AD user account + generates report |
| 3 | activedirectory_reset_password | Account Management | Resets compromised user's password (analyst approves first) |
| 4 | AD_LDAP_Account_Locking | Account Management | Locks account via LDAP connector |
| 5 | AD_LDAP_Account_Unlocking | Account Management | Unlocks account via LDAP connector |
| 6 | AD_LDAP_Entity_Attribute_Lookup | Account Management | Fetches user/device attributes & group memberships from LDAP |
| 7 | AWS_IAM_Account_Locking | Account Management | Disables an AWS IAM account (deletes login profile) |
| 8 | AWS_IAM_Account_Unlocking | Account Management | Re-enables an AWS IAM account |
| 9 | Azure_AD_Account_Locking | Account Management | Disables an Azure AD account |
| 10 | Azure_AD_Account_Unlocking | Account Management | Enables a disabled Azure AD account |
| 11 | Azure_AD_Graph_User_Attribute_Lookup | Account Management | Fetches user/device attributes from Azure AD |
| 12 | azure_new_user_census | Account Management | Weekly census of new Azure AD users |
| 13 | aws_disable_user_accounts | Account Management | Bulk-disables AWS IAM users (with allowlist check + analyst approval) |
| 14 | aws_find_inactive_users | Account Management | Finds AWS accounts unused for 90+ days |
| 15 | track_active_directory_admin_users | Account Management | Monitors AD admin group for unauthorized additions |
| 16 | CrowdStrike_OAuth_API_Device_Attribute_Lookup | Endpoint (EDR) | Looks up device attributes by hostname/IP in CrowdStrike |
| 17 | CrowdStrike_OAuth_API_Dynamic_Analysis | Endpoint (EDR) | Reputation analysis of URL or file hash via CrowdStrike |
| 18 | CrowdStrike_OAuth_API_Endpoint_Analysis | Endpoint (EDR) | Collects running processes & network connections from endpoint |
| 19 | CrowdStrike_OAuth_API_Executable_Denylisting | Endpoint (EDR) | Adds a custom IOC block for a file on a device |
| 20 | CrowdStrike_OAuth_API_File_Collection | Endpoint (EDR) | Collects a file from an endpoint to the SOAR File Vault |
| 21 | CrowdStrike_OAuth_API_File_Eviction | Endpoint (EDR) | Deletes a file from an endpoint |
| 22 | CrowdStrike_OAuth_API_File_Restore | Endpoint (EDR) | Restores a file from File Vault back to endpoint |
| 23 | CrowdStrike_OAuth_API_Get_Device_Info | Endpoint (EDR) | Resolves device ID ↔ hostname mapping |
| 24 | CrowdStrike_OAuth_API_Network_Isolation | Endpoint (EDR) | Quarantines/isolates a device in CrowdStrike |
| 25 | CrowdStrike_OAuth_API_Network_Restore | Endpoint (EDR) | Restores network access to a quarantined device |
| 26 | CrowdStrike_OAuth_API_Process_Termination | Endpoint (EDR) | Kills specific processes on a device |
| 27 | Crowdstrike_Endpoint_IOC_Enrichment | Endpoint (EDR) | Deep investigation of CrowdStrike device + related devices |
| 28 | Crowdstrike_Endpoint_Quarantine_Response | Endpoint (EDR) | Deep investigation + quarantine response |
| 29 | crowdstrike_malware_triage | Endpoint (EDR) | Triage & respond to CrowdStrike malicious executable detection |
| 30 | host_quarantine_crowdstrike | Endpoint (EDR) | Simple quarantine of an endpoint via CrowdStrike |
| 31 | delete_detected_files | Endpoint (EDR) | Deletes malicious files (webshells) from endpoints |
| 32 | terminate_spawned_processes | Endpoint (EDR) | Kills malicious spawned shell processes on endpoints |
| 33 | reinfected_endpoint_check | Endpoint (EDR) | Checks if an infected host is a new or repeat infection |
| 34 | ransomware_investigate_and_contain | Endpoint (EDR) | Investigates and contains ransomware on endpoints |
| 35 | ssh_endpoint_investigate | Endpoint (EDR) | Gathers system info from a Linux server via SSH |
| 36 | email_notification_for_malware | Endpoint (EDR) | Checks if a file is malware and if it exists on managed machines |
| 37 | G_Suite_for_Gmail_Message_Eviction | Email & Phishing | Deletes a specific email from a Gmail mailbox |
| 38 | G_Suite_for_Gmail_Search_and_Purge | Email & Phishing | Finds and deletes a malicious email across all Gmail mailboxes |
| 39 | MS_Graph_for_Office_365_Message_Eviction | Email & Phishing | Deletes a specific email from an O365 mailbox |
| 40 | MS_Graph_for_Office_365_Message_Restore | Email & Phishing | Restores a deleted email to an O365 mailbox |
| 41 | MS_Graph_for_Office_365_Search_and_Purge | Email & Phishing | Finds and deletes an email across all O365 mailboxes |
| 42 | MS_Graph_for_Office_365_Search_and_Restore | Email & Phishing | Finds and restores a purged email from O365 mailboxes |
| 43 | ReversingLabs_Reported_Email_Triage | Email & Phishing | Triages user-reported phishing emails from a dedicated M365 mailbox |
| 44 | mcafee_phishing_attachment_investigate | Email & Phishing | Investigates a suspicious phishing email attachment |
| 45 | phishme_email_investigate_and_respond | Email & Phishing | Blocks high-impact indicators from PhishMe phishing campaigns |
| 46 | Splunk_Automated_Email_Investigation | Email & Phishing | Analyzes .eml/.msg files for malicious content |
| 47 | Splunk_Message_Identifier_Activity_Analysis | Email & Phishing | Finds all Splunk records matching a specific email Message ID |
| 48 | Cisco_Umbrella_DNS_Denylisting | Network & Blocking | Blocks domains in Cisco Umbrella DNS |
| 49 | DNS_Denylisting_Dispatch | Network & Blocking | Routes domain indicators to DNS blocking playbooks |
| 50 | domain_block_umbrella | Network & Blocking | Blocks a single domain using Cisco Umbrella |
| 51 | domain_investigate | Network & Blocking | Investigates a domain using three reputation tools |
| 52 | Panorama_Outbound_Traffic_Filtering | Network & Blocking | Blocks URLs using Palo Alto Networks Firewall |
| 53 | URL_Outbound_Traffic_Filtering_Dispatch | Network & Blocking | Routes URL indicators to blocking playbooks |
| 54 | Zscaler_Outbound_Traffic_Filtering | Network & Blocking | Blocks URLs in ZScaler web proxy |
| 55 | zscaler_hunt_and_block_url | Network & Blocking | Finds internal users who visited a bad URL, then blocks it |
| 56 | zscaler_malicious_file_response | Network & Blocking | Responds to ZScaler malicious file alert |
| 57 | zscaler_patient_0_parse_email | Network & Blocking | Parses ZScaler Patient 0 alert emails into SOAR events |
| 58 | customer_firewall_request_parse_csv | Network & Blocking | Parses a CSV file of bulk firewall rule changes |
| 59 | customer_firewall_request_handle_artifact | Network & Blocking | Processes each firewall change request from parsed CSV |
| 60 | PhishTank_URL_Reputation_Analysis | Threat Intel & Enrichment | URL reputation check via PhishTank |
| 61 | ReversingLabs_TitaniumCloud_File_Reputation | Threat Intel & Enrichment | File hash reputation via ReversingLabs TitaniumCloud |
| 62 | ReversingLabs_TitaniumCloud_URL_Reputation | Threat Intel & Enrichment | URL reputation via ReversingLabs TitaniumCloud |
| 63 | ReversingLabs_TitaniumScale_File_Analysis | Threat Intel & Enrichment | File detonation/sandbox analysis via ReversingLabs |
| 64 | VirusTotal_v3_Dynamic_Analysis | Threat Intel & Enrichment | Detonates URL/file in VirusTotal sandbox |
| 65 | VirusTotal_v3_Identifier_Reputation_Analysis | Threat Intel & Enrichment | Multi-type reputation check (URL, IP, domain, hash) via VirusTotal |
| 66 | UrlScan_IO_Dynamic_Analysis | Threat Intel & Enrichment | URL detonation/analysis via urlscan.io |
| 67 | greynoise_gnql_enrichment | Threat Intel & Enrichment | Bulk query for malicious/compromised devices via GreyNoise |
| 68 | greynoise_ip_enrichment | Threat Intel & Enrichment | IP reputation check + auto severity assignment via GreyNoise |
| 69 | greynoise_on_poll_set_severity | Threat Intel & Enrichment | Sets event severity from GreyNoise on-poll classification |
| 70 | greynoise_update_severity_from_ip_reputation | Threat Intel & Enrichment | Updates severity based on GreyNoise malicious/benign verdict |
| 71 | Splunk_Attack_Analyzer_Dynamic_Analysis | Threat Intel & Enrichment | URL/file detonation using Splunk Attack Analyzer |
| 72 | Splunk_Identifier_Activity_Analysis | Threat Intel & Enrichment | Finds internal devices/users who interacted with a bad indicator |
| 73 | threat_intel_investigate | Threat Intel & Enrichment | Parent playbook for gathering threat intel across all sources |
| 74 | lets_encrypt_domain_investigate | Threat Intel & Enrichment | Investigates potentially malicious/phishing domains |
| 75 | trustar_network_enrichment | Threat Intel & Enrichment | Gathers IP/domain/URL intel from TruSTAR |
| 76 | url_investigate | Threat Intel & Enrichment | Full URL investigation with priority scoring and verdict |
| 77 | intelligence_management_enrich_indicators | Threat Intel & Enrichment | Enriches indicators using an intelligence management platform |
| 78 | Check_Point_EM_IOC_Enrichment_and_Triage | Threat Intel & Enrichment | Enriches IOCs using Check Point EM threat intelligence |
| 79 | Attribute_Lookup_Dispatch | Threat Intel & Enrichment | Routes entities to attribute lookup playbooks |
| 80 | Dynamic_Analysis_Dispatch | Threat Intel & Enrichment | Routes URLs/files to dynamic analysis playbooks |
| 81 | Identifier_Activity_Analysis_Dispatch | Threat Intel & Enrichment | Routes indicators to activity analysis playbooks |
| 82 | Identifier_Reputation_Analysis_Dispatch | Threat Intel & Enrichment | Routes indicators to reputation analysis playbooks |
| 83 | dispatch_input_playbooks | Threat Intel & Enrichment | Alternative dispatcher for routing indicators to input playbooks |
| 84 | Automated_Enrichment | Threat Intel & Enrichment | Kicks off full enrichment: reputation + attribute + ticket search |
| 85 | log4j_investigate | Vulnerability Response | Parent Log4j investigation playbook (CVE-2021-44228) |
| 86 | log4j_respond | Vulnerability Response | Response/remediation phase launched by log4j_investigate |
| 87 | internal_host_splunk_investigate_log4j | Vulnerability Response | Investigates Log4j exposure using existing Splunk data |
| 88 | internal_host_ssh_investigate | Vulnerability Response | Investigates Linux host for Log4j via SSH |
| 89 | internal_host_ssh_log4j_investigate | Vulnerability Response | Deep Log4j scan of Linux host via SSH |
| 90 | internal_host_ssh_log4j_respond | Vulnerability Response | Remediates Log4j on Linux hosts via SSH |
| 91 | internal_host_winrm_investigate | Vulnerability Response | Investigates Windows host for Log4j via WinRM |
| 92 | internal_host_winrm_log4j_investigate | Vulnerability Response | Scans Windows host for vulnerable Log4j class files |
| 93 | internal_host_winrm_log4j_respond | Vulnerability Response | Remediates Log4j on Windows hosts via WinRM |
| 94 | risk_notable_preprocess | SIEM/ES Integration | Prepares a Risk Notable for investigation |
| 95 | risk_notable_import_data | SIEM/ES Integration | Pulls all related events into the Risk Notable as artifacts |
| 96 | risk_notable_enrich | SIEM/ES Integration | Enriches all indicators in a Risk Notable automatically |
| 97 | risk_notable_investigate | SIEM/ES Integration | Updates Risk Investigation workbook tasks |
| 98 | risk_notable_protect_assets_and_users | SIEM/ES Integration | Matches event entities with Splunk ES asset/identity database |
| 99 | risk_notable_merge_events | SIEM/ES Integration | Finds related events and lets analyst decide what to merge |
| 100 | risk_notable_auto_merge | SIEM/ES Integration | Auto-merges duplicate Risk Notables for the same risk object |
| 101 | risk_notable_block_indicators | SIEM/ES Integration | Finds blocked-marked indicators and executes blocking playbooks |
| 102 | risk_notable_review_indicators | SIEM/ES Integration | Processes suspicious-marked indicators for analyst review |
| 103 | risk_notable_auto_investigate | SIEM/ES Integration | Auto-investigates notables above a defined risk threshold |
| 104 | risk_notable_auto_containment | SIEM/ES Integration | Auto-contains assets/identities with confirmed high risk |
| 105 | risk_notable_auto_undo_containment | SIEM/ES Integration | Reverses containment after resolution |
| 106 | risk_notable_mitigate | SIEM/ES Integration | Updates Risk Response workbook tasks |
| 107 | risk_notable_verdict | SIEM/ES Integration | Presents response playbook options to analyst for final decision |
| 108 | Mission_Control_Attribute_Lookup | SIEM/ES Integration | Launches attribute lookup playbooks within a response plan |
| 109 | Mission_Control_Automated_Enrichment | SIEM/ES Integration | Launches full enrichment playbooks within a response plan |
| 110 | Mission_Control_Identifier_Reputation_Analysis | SIEM/ES Integration | Launches reputation analysis playbooks within a response plan |
| 111 | Mission_Control_Related_Tickets_Search | SIEM/ES Integration | Launches related ticket search within a response plan |
| 112 | Splunk_Notable_Related_Tickets_Search | SIEM/ES Integration | Finds related Splunk notables for a user/device in last 24 hrs |
| 113 | create_ticket | Ticketing | Creates a ticket in any external case management system |
| 114 | Jira_Related_Tickets_Search | Ticketing | Finds related Jira tickets for a user/device in last 30 days |
| 115 | Related_Tickets_Search_Dispatch | Ticketing | Routes indicators to related ticket search playbooks |
| 116 | ServiceNow_Create_Incident | Ticketing | Creates a ServiceNow incident from SOAR automation output |
| 117 | ServiceNow_Create_Incident_Es | Ticketing | Creates a ServiceNow incident from an ES response plan |
| 118 | ServiceNow_Query_Incidents | Ticketing | Queries ServiceNow for incidents matching an affected entity |
| 119 | ServiceNow_Related_Tickets_Search | Ticketing | Finds related ServiceNow tickets in last 30 days |
| 120 | ServiceNow_Update_Incident | Ticketing | Updates an existing ServiceNow incident with new findings |
| 121 | ServiceNow_Update_Incident_Notes | Ticketing | Sends all investigation notes to a ServiceNow incident |
| 122 | alert_deescalation_for_test_machines | Severity Management | Lowers severity for alerts from known test/lab machine IPs |
| 123 | alert_escalation_for_attacked_executives | Severity Management | Escalates severity to HIGH/TLP:RED for executive-targeted attacks |
| 124 | reset_entity_risk | Severity Management | Resets risk score of an entity to zero (false positive cleanup) |
| 125 | rogue_wireless_access_point_remediate | Severity Management | Detects and removes rogue/unauthorized wireless access points |
| 126 | ec2_instance_investigation_and_notification | Cloud Security | Investigates a suspicious EC2 instance from AWS Security Hub |
| 127 | ec2_instance_isolation | Cloud Security | Isolates an EC2 instance by modifying its security group |
| 128 | gcp_unusual_serviceaccount_usage | Cloud Security | Investigates unusual GCP service account activity |
| 129 | Check_Point_EM_Credential_Leak_Validation | Cloud Security | Validates and recycles leaked credentials detected by Check Point |
| 130 | Check_Point_EM_Phishing_Takedown | Cloud Security | Automates phishing site takedown via Check Point EM |
| 131 | extrahop_detect_data_exfiltration | Network Monitoring | Investigates ExtraHop anomaly for potential data exfiltration |
| 132 | extrahop_externally_accessible_databases | Network Monitoring | Responds to ExtraHop alert for externally exposed internal DB |
| 133 | extrahop_new_dns_servers | Network Monitoring | Periodic check (every 30 min) for new/rogue DNS servers |
| 134 | dns_hijack_enrichment | Network Monitoring | Investigates DNS hijacking (Splunk Analytic Story) |
| 135 | corelight_investigate_dns_alert | Network Monitoring | Investigates Suricata/Corelight malicious DNS query alerts |
| 136 | endace_splunk_search_download_pcap | Network Monitoring | Downloads network PCAP via EndaceProbe for forensic analysis |
| 137 | nagios_service_monitor | Network Monitoring | Auto-responds to Nagios Linux service failure notifications |
| 138 | vectra_advanced_block_host | Network Monitoring | Blocks/unblocks IP on PAN Firewall from Vectra threat request |
| 139 | vectra_basic_block_host | Network Monitoring | Simple block/unblock of IP on PAN Firewall from Vectra |
| 140 | vectra_detection_notification | Network Monitoring | Sends notification email for a Vectra-detected threat |
| 141 | protectwise_investigate_and_respond | Network Monitoring | Investigates a security alert using ProtectWise network data |
| 142 | symantec_ioc_data_enhancement | Third-Party Tools | Detonates a file in Symantec Content Analysis + enriches IOCs |
| 143 | symantec_proxysg_unblock_request | Third-Party Tools | Processes website unblock requests for Symantec ProxySG |
| 144 | threatquotient_investigate_and_respond | Third-Party Tools | Enriches IP/URL indicators using ThreatQuotient |
| 145 | Commvault_Cloud_Disable_Data_Aging | Third-Party Tools | Disables data aging to protect backup data from purging |
| 146 | vmworld_c2_response | Third-Party Tools | Responds to a C2 alert in a VMware virtualized environment |
| 147 | vmworld_wannacry_response | Third-Party Tools | WannaCry response using VM snapshots in VMware environment |
| 148 | start_investigation | Workflow Management | Assigns user and opens the investigation workbook |
| 149 | user_approved_ticket_creation | Workflow Management | Analyst-approved ticket creation within a workbook |
| 150 | onboarding_demonstration | Workflow Management | Demo: enriches URLs/IPs/domains and updates event with context |
| 151 | test_connectivity | Utility | Tests connectivity to all configured SOAR assets |
| 152 | pin_to_hud_sample | Utility | Demo: shows how to update the SOAR HUD from a playbook |
| 153 | advanced_playbook_tutorial | Utility | Tutorial playbook showing editor features (not for production) |
| 154 | user_prompt_and_block_domain | Utility | Scores domain risk via DomainTools and blocks if high risk |
| 155 | Sub_Debug_Playbook | Utility | Internal debugging playbook |
| 156 | First_Test_Playbook_2 | Utility | Internal test playbook |
| 157 | Full_Block_Coverage_Playbook | Utility | Internal test/coverage playbook |

---

## Detailed Use Cases by Category

---

### A. Account Management
> **Goal:** Lock, unlock, disable, enable, reset, or audit user accounts across different identity platforms.

| Platform | Lock/Disable | Unlock/Enable | Attribute Lookup | Special |
|----------|-------------|---------------|-----------------|---------|
| Active Directory | Active_Directory_Disable_Account_Dispatch | Active_Directory_Enable_Account_Dispatch | AD_LDAP_Entity_Attribute_Lookup | activedirectory_reset_password |
| Microsoft LDAP | AD_LDAP_Account_Locking | AD_LDAP_Account_Unlocking | AD_LDAP_Entity_Attribute_Lookup | — |
| AWS IAM | AWS_IAM_Account_Locking, aws_disable_user_accounts | AWS_IAM_Account_Unlocking | — | aws_find_inactive_users |
| Azure AD | Azure_AD_Account_Locking | Azure_AD_Account_Unlocking | Azure_AD_Graph_User_Attribute_Lookup | azure_new_user_census |

**activedirectory_reset_password** — Resets a compromised account's password with analyst approval. Steps: analyst reviews → approves → strong password auto-generated → applied.

**aws_disable_user_accounts** — Disables a list of AWS IAM accounts after checking against an allowlist and getting analyst confirmation.

**aws_find_inactive_users** — Finds accounts not used in 90+ days for access review/cleanup.

**azure_new_user_census** — Weekly audit of new Azure AD user accounts for unauthorized additions.

**track_active_directory_admin_users** — Monitors the AD Administrators group and alerts when new users are added.

---

### B. Endpoint Detection & Response (EDR)
> **Goal:** Investigate, contain, clean up, or respond to threats on endpoints — primarily via CrowdStrike.

**Quick decision guide:**

| Situation | Playbook to Use |
|-----------|----------------|
| Need to quarantine/isolate an endpoint | CrowdStrike_OAuth_API_Network_Isolation / host_quarantine_crowdstrike |
| Restore a quarantined endpoint | CrowdStrike_OAuth_API_Network_Restore |
| Kill a malicious process | CrowdStrike_OAuth_API_Process_Termination |
| Delete a malicious file | CrowdStrike_OAuth_API_File_Eviction / delete_detected_files |
| Collect file for forensics | CrowdStrike_OAuth_API_File_Collection |
| Block a file (hash) | CrowdStrike_OAuth_API_Executable_Denylisting |
| Investigate what's running on an endpoint | CrowdStrike_OAuth_API_Endpoint_Analysis |
| Get device details (ID ↔ hostname) | CrowdStrike_OAuth_API_Get_Device_Info |
| Full endpoint investigation + quarantine | Crowdstrike_Endpoint_Quarantine_Response |
| Ransomware on endpoint | ransomware_investigate_and_contain |
| Malicious spawned shell processes | terminate_spawned_processes |
| Is the infected host a repeat offender? | reinfected_endpoint_check |

---

### C. Email Security & Phishing Response
> **Goal:** Remove malicious emails from mailboxes, investigate phishing, and block related indicators.

**Quick decision guide:**

| Situation | Playbook to Use |
|-----------|----------------|
| Delete email from one Gmail inbox | G_Suite_for_Gmail_Message_Eviction |
| Delete email from ALL Gmail inboxes | G_Suite_for_Gmail_Search_and_Purge |
| Delete email from one O365 inbox | MS_Graph_for_Office_365_Message_Eviction |
| Delete email from ALL O365 inboxes | MS_Graph_for_Office_365_Search_and_Purge |
| Restore an accidentally deleted O365 email | MS_Graph_for_Office_365_Message_Restore / Search_and_Restore |
| Investigate a reported phishing email | ReversingLabs_Reported_Email_Triage / mcafee_phishing_attachment_investigate |
| Block PhishMe-reported campaign indicators | phishme_email_investigate_and_respond |
| Analyze an .eml or .msg file | Splunk_Automated_Email_Investigation |
| Find which users received a specific email | Splunk_Message_Identifier_Activity_Analysis |

---

### D. Network Security & Traffic Blocking
> **Goal:** Block malicious domains, URLs, or IPs at the network layer across DNS, firewalls, and web proxies.

**Quick decision guide:**

| What to Block | Platform | Playbook |
|--------------|----------|---------|
| Domain (DNS level) | Cisco Umbrella | Cisco_Umbrella_DNS_Denylisting / domain_block_umbrella |
| URL (firewall) | Palo Alto Networks | Panorama_Outbound_Traffic_Filtering |
| URL (web proxy) | ZScaler | Zscaler_Outbound_Traffic_Filtering |
| IP (from Vectra alert) | Palo Alto Networks | vectra_advanced_block_host / vectra_basic_block_host |
| Firewall rule changes from CSV | Any | customer_firewall_request_parse_csv + handle_artifact |
| Auto-route domain indicators to blocking | Any | DNS_Denylisting_Dispatch |
| Auto-route URL indicators to blocking | Any | URL_Outbound_Traffic_Filtering_Dispatch |

**domain_investigate** — Before blocking a domain, use this to investigate it with three different reputation sources.

**zscaler_hunt_and_block_url** — Finds which internal users already visited a suspicious URL, then blocks it.

---

### E. Threat Intelligence & Enrichment
> **Goal:** Enrich indicators (IPs, domains, URLs, file hashes) with reputation data from multiple sources.

**By indicator type:**

| Indicator | Tool Options |
|-----------|-------------|
| File Hash | VirusTotal_v3_Dynamic_Analysis, ReversingLabs_TitaniumCloud_File_Reputation, ReversingLabs_TitaniumScale_File_Analysis |
| URL | PhishTank_URL_Reputation_Analysis, UrlScan_IO_Dynamic_Analysis, VirusTotal_v3_Identifier_Reputation_Analysis, url_investigate, Splunk_Attack_Analyzer_Dynamic_Analysis |
| Domain | lets_encrypt_domain_investigate, domain_investigate, VirusTotal_v3_Identifier_Reputation_Analysis |
| IP Address | greynoise_ip_enrichment, greynoise_gnql_enrichment, VirusTotal_v3_Identifier_Reputation_Analysis |
| Any/Multi | Automated_Enrichment, Attribute_Lookup_Dispatch, threat_intel_investigate, intelligence_management_enrich_indicators |

**Dispatcher playbooks** (auto-route indicators to the right playbook):
- `Attribute_Lookup_Dispatch` — routes to attribute lookup playbooks
- `Dynamic_Analysis_Dispatch` — routes to dynamic analysis/detonation playbooks
- `Identifier_Activity_Analysis_Dispatch` — routes to activity analysis playbooks
- `Identifier_Reputation_Analysis_Dispatch` — routes to reputation analysis playbooks
- `dispatch_input_playbooks` — alternative dispatcher for input playbooks
- `Automated_Enrichment` — kicks off all three: reputation + attribute + ticket search

**Splunk_Identifier_Activity_Analysis** — Asks Splunk who in your environment has already interacted with a bad indicator.

---

### F. Log4j Vulnerability Response (CVE-2021-44228)
> **Goal:** Detect, investigate, and remediate the Log4Shell vulnerability across Linux and Windows hosts.

**Recommended execution order:**

```
1. log4j_investigate          ← Start here (parent playbook)
      ├── internal_host_splunk_investigate_log4j   (uses Splunk data)
      ├── internal_host_ssh_investigate             (Linux - general check)
      ├── internal_host_ssh_log4j_investigate       (Linux - deep Log4j scan)
      ├── internal_host_winrm_investigate           (Windows - general check)
      └── internal_host_winrm_log4j_investigate     (Windows - deep Log4j scan)

2. log4j_respond              ← Launched automatically when risk is confirmed
      ├── internal_host_ssh_log4j_respond           (Linux remediation)
      └── internal_host_winrm_log4j_respond         (Windows remediation)
```

---

### G. Splunk Enterprise Security (Risk Notable) Integration
> **Goal:** Automate the full lifecycle of a Splunk ES Risk Notable — from preprocessing to verdict and containment.

**Standard Risk Notable lifecycle:**

```
risk_notable_preprocess
    → risk_notable_import_data
    → risk_notable_enrich
    → risk_notable_protect_assets_and_users
    → risk_notable_investigate
    → risk_notable_merge_events / risk_notable_auto_merge
    → risk_notable_block_indicators
    → risk_notable_auto_investigate (if score > threshold)
    → risk_notable_auto_containment (if confirmed threat)
    → risk_notable_mitigate
    → risk_notable_verdict          ← Analyst makes final decision
    → risk_notable_auto_undo_containment (after resolution)
```

**Mission Control playbooks** are wrapper orchestrators used within specific response plan phases:
- `Mission_Control_Automated_Enrichment` — enrichment phase
- `Mission_Control_Attribute_Lookup` — attribute lookup phase
- `Mission_Control_Identifier_Reputation_Analysis` — reputation phase
- `Mission_Control_Related_Tickets_Search` — ticket search phase

---

### H. Ticketing & Case Management
> **Goal:** Create, query, update, and link tickets in Jira or ServiceNow from SOAR workflows.

| Action | Jira | ServiceNow |
|--------|------|-----------|
| Create new ticket | create_ticket | ServiceNow_Create_Incident / ServiceNow_Create_Incident_Es |
| Find related tickets | Jira_Related_Tickets_Search | ServiceNow_Related_Tickets_Search / ServiceNow_Query_Incidents |
| Update existing ticket | — | ServiceNow_Update_Incident |
| Send investigation notes | — | ServiceNow_Update_Incident_Notes |
| Auto-route to right search | Related_Tickets_Search_Dispatch | Related_Tickets_Search_Dispatch |

---

### I. Cloud Security
> **Goal:** Investigate and respond to threats in AWS, Azure, and GCP environments.

**AWS:**
- `ec2_instance_investigation_and_notification` — Investigates a Security Hub finding for an exposed EC2 instance
- `ec2_instance_isolation` — Isolates an EC2 instance by modifying its security group to block all traffic

**GCP:**
- `gcp_unusual_serviceaccount_usage` — Investigates unusual service account activity in Google Cloud Platform

**Check Point (SaaS/Cloud Security):**
- `Check_Point_EM_Credential_Leak_Validation` — Validates and recycles leaked credentials automatically
- `Check_Point_EM_Phishing_Takedown` — Automates phishing site takedown via Check Point EM

---

### J. Network & Infrastructure Monitoring
> **Goal:** Monitor network traffic, detect anomalies, and respond to infrastructure threats.

| Tool | Playbook | What It Does |
|------|---------|-------------|
| ExtraHop | extrahop_detect_data_exfiltration | Investigates potential data exfiltration anomaly |
| ExtraHop | extrahop_externally_accessible_databases | Responds to internal DB accessed from outside |
| ExtraHop | extrahop_new_dns_servers | Periodic check for new/unauthorized DNS servers |
| Corelight/Suricata | corelight_investigate_dns_alert | Investigates suspicious DNS query alerts |
| EndaceProbe | endace_splunk_search_download_pcap | Downloads PCAP for forensic network analysis |
| Nagios | nagios_service_monitor | Auto-responds to Linux service failure alerts |
| Vectra AI | vectra_detection_notification | Sends alert notification for Vectra detections |
| Splunk | dns_hijack_enrichment | Investigates DNS hijacking detections from Splunk |

---

### K. Severity & Alert Management
> **Goal:** Automatically adjust event severity to reduce noise and prioritize what matters.

**alert_deescalation_for_test_machines**
- Checks if source IP is a known test machine → lowers severity to LOW / TLP:WHITE
- If unknown, prompts analyst to classify → saves answer for future use
- Prevents wasted time on test environment alerts

**alert_escalation_for_attacked_executives**
- Checks if affected user is in the AD "Executive" group via LDAP
- If yes → escalates severity to HIGH / TLP:RED for priority response

**reset_entity_risk**
- Resets an entity's risk score to zero by posting negating risk events
- Used for clearing false positive risk scores in Splunk ES

**rogue_wireless_access_point_remediate**
- Works with a Raspberry Pi 3 sensor to detect and remove unauthorized wireless access points from the network

---

### L. Third-Party Integrations
> **Goal:** Orchestrate responses using specialized security tools beyond the core stack.

| Tool | Playbook | What It Does |
|------|---------|-------------|
| Symantec Content Analysis | symantec_ioc_data_enhancement | Detonates file and enriches resulting IOCs |
| Symantec ProxySG | symantec_proxysg_unblock_request | Processes website unblock requests |
| ThreatQuotient | threatquotient_investigate_and_respond | Enriches IP/URL indicators from ThreatQuotient |
| Commvault | Commvault_Cloud_Disable_Data_Aging | Disables backup data aging to protect recovery data |
| ProtectWise | protectwise_investigate_and_respond | Investigates alerts with file hash + IP using ProtectWise |
| TruSTAR | trustar_network_enrichment | Gathers threat intel for IPs/domains/URLs from TruSTAR |
| VMware | vmworld_c2_response | Responds to a C2 alert in a VMware environment |
| VMware | vmworld_wannacry_response | WannaCry response using VM snapshot capability |

---

### M. Workflow & Utility
> **Goal:** Support investigation workflows, test setups, and demonstrate platform capabilities.

| Playbook | Purpose |
|---------|---------|
| start_investigation | Assigns user and opens the investigation workbook |
| user_approved_ticket_creation | Analyst-approved ticket creation within a workbook |
| onboarding_demonstration | Demo enrichment playbook for onboarding/training |
| test_connectivity | Verifies all SOAR assets/integrations are reachable |
| pin_to_hud_sample | Demo: how to surface data on the SOAR HUD |
| advanced_playbook_tutorial | Tutorial showing editor features (not for production) |
| user_prompt_and_block_domain | Scores domain via DomainTools → auto-blocks if high risk |
| Sub_Debug_Playbook | Internal debugging utility |
