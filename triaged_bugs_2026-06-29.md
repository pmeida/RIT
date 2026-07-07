# RIT Triage Tracker — Week of 2026-06-29

Bugs triaged by Jakub Hadvig (Triage Monitor). At end of week, unassign any that haven't moved past New.

## Triaged This Week

| Key | Summary | Priority | Assignee | Status at triage |
|-----|---------|----------|----------|-----------------|
| OCPBUGS-84513 | terminationMessagePolicy in openshift-cluster-version | Normal | Pratik Mahajan | New |
| OCPBUGS-84517 | terminationMessagePolicy in openshift-marketplace | Normal | Jefferson Ramos | New |
| OCPBUGS-84518 | terminationMessagePolicy in openshift-operators | Normal | Rachel Ryan | New |
| OCPBUGS-84521 | terminationMessagePolicy in openshift-cluster-machine-approver | Normal | Matthew Booth | New |
| OCPBUGS-84569 | exclude-from-external-load-balancers label broken for masters | Major | Matthew Booth | New |
| OCPBUGS-92181 | Non-admin users can't access Console after 4.21.5 upgrade | Major | Stefano Nardo | New |
| OCPBUGS-11622 | CVO: minimize wildcard/privilege in roles | Major | Martin Simka | New |
| OCPBUGS-91668 | vSphere MachinePool: MachineSets reference non-existent RHCOS template | Major | Ankita Thomas | New |
| OCPBUGS-84957 | CRD ownership conflict MetalLB/Network Operator | Normal | Stanislav Jakuschevskij | New |
| OCPBUGS-81679 | Console slow (Dashboards/ODF pages) | Normal | Stefano Nardo | New |
| OCPBUGS-82365 | Console pods restarting, random user logouts | Normal | Stefano Nardo | New |
| OCPBUGS-78355 | opm ~560% CPU spike → Node NotReady | Critical | Ankita Thomas | New |
| OCPBUGS-78095 | redhat-operators startup probe timeout | Major | Ankita Thomas | New |
| OCPBUGS-79668 | Continual image pulls ~543GB/day bandwidth | Major | Ankita Thomas | New |
| OCPBUGS-83799 | Workloads sidebar ordering (DC disabled) | Normal | Jakub Hadvig | New |
| OCPBUGS-54982 | Login failing on Windows Edge | Minor | Jakub Hadvig | New |
| OCPBUGS-90834 | vSphere connection details empty in Console | Normal | Jakub Hadvig | New |
| OCPBUGS-82111 | Console stuck on white screen | Major | Jakub Hadvig | New |
| OCPBUGS-52186 | Project overview not showing resource usage | Normal | Rachel Ryan | New (was ASSIGNED/Rastislav) |
| OCPBUGS-69643 | Console not displaying CPU/Memory/FS usage | Normal | Rachel Ryan | New (was ASSIGNED/Rastislav) |
| OCPBUGS-50016 | Strange formatting of '9' in console logs | Minor | Martin Simka | New (was ASSIGNED/Jackson) |
| OCPBUGS-61694 | Topology view broken with Knative resources | Normal | Stanislav Jakuschevskij | New (was ASSIGNED/Vikram) |
| OCPBUGS-78475 | Can't paste in pod terminal on Firefox | Normal | Martin Simka | New (was ASSIGNED/Cyril) |
| OCPBUGS-27745 | Additional console route not working | Critical | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-16633 | Console session deleted before inactivityTimeout | Major | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-65732 | CPMS ClusterOperator degraded — vSphere connection form | Major | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-55459 | Intermittent UI issues after 4.17 update | Major | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-70112 | Security vulns in RHACM (ICICI Bank) | Major | Jakub Hadvig | New |
| OCPBUGS-56219 | Console Overview exhausting browser memory | Normal | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-14473 | Overview page "cannot read properties" error | Normal | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-35735 | Version Number Disclosed | Minor | Jakub Hadvig | New (was ASSIGNED) |
| OCPBUGS-85793 | Warning "dataDisks" vSphere install from ACM | Minor | Rachel Ryan | New |
| OCPBUGS-8252 | CVO multi-arch transition feedback | Minor | Martin Simka | New |
| OCPBUGS-51181 | OSUS no "enable monitoring" option | Minor | Stanislav Jakuschevskij | New |
| OCPBUGS-54864 | Too many unwanted CVO logs | Minor | Jefferson Ramos | New |
| OCPBUGS-81471 | OSUS graph_builder distracting error message | Minor | Ankita Thomas | New |
| OCPBUGS-92240 | Console missing translations after 4.21.5 upgrade | Minor | Matthew Booth | New |
| OCPBUGS-58399 | Machine API doesn't use new vCenter creds | Normal | Matthew Booth | New |
| OCPBUGS-93314 | CCO enhancements for restricted AWS | Normal | Jefferson Ramos | New |
| OCPBUGS-56742 | DNS queries from OSUS | Normal | Martin Simka | New |
| OCPBUGS-1694 | CVO doesn't trust Ingress Default CA | Normal | Martin Simka | New |
| OCPBUGS-39539 | CVO wedges with rogue owner references | Normal | Martin Simka | New |
| OCPBUGS-17664 | CCO AccessDenied due to SCP | Normal | Rachel Ryan | New |
| OCPBUGS-62819 | Azure LB '-internal' with Hive | Normal | Rachel Ryan | New |
| OCPBUGS-91675 | CVE-2026-42043 Axios NO_PROXY bypass [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91676 | CVE-2026-42033 Axios HTTP Transport Hijacking [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91683 | CVE-2026-12143 form-data CRLF injection [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91720 | CVE-2026-48779 ws DoS memory exhaustion [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91724 | CVE-2026-6734 undici Socks5 routing [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91725 | CVE-2026-9697 undici MitM SOCKS5 [5.0] | Critical | Jakub Hadvig | New |
| OCPBUGS-91728 | CVE-2026-12151 undici DoS WebSocket [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-91731 | CVE-2026-45736 ws uninitialized memory [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-92088 | CVE-2026-44990 sanitize-html XSS [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-93952 | CVE-2026-56876 extract-zip arbitrary file write [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-94055 | CVE-2026-13676 fast-uri Unicode hostname bypass [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-94130 | CVE-2026-45822 decode-uri-component DoS [5.0] | Critical | Jefferson Ramos | New |
| OCPBUGS-94168 | CVE-2026-13149 brace-expansion DoS [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-95473 | CVE-2026-53488 containerd host-root exec [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-96717 | CVE-2026-44240 basic-ftp DoS [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-96734 | CVE-2026-41242 protobufjs ACE [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-96736 | CVE-2026-6322 fast-uri authority bypass [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-96750 | CVE-2026-42306 Moby host file overwrite [5.0] | Critical | Stefano Nardo | New |
| OCPBUGS-93196 | CVE-2026-42504 Golang MIME DoS (GCP CCM) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-93197 | CVE-2026-42504 Golang MIME DoS (Azure CCM) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-93205 | CVE-2026-42504 Golang MIME DoS (AWS CCM) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-93584 | CVE-2026-39835 crypto/ssh DoS (Azure service) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-93585 | CVE-2026-39835 crypto/ssh DoS (Azure CAPI) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-93595 | CVE-2026-39835 crypto/ssh DoS (CAPI op) [5.0] | Critical | Martin Simka | New |
| OCPBUGS-92059 | ARO/Hive OpenSSL CVEs FedRAMP compliance | Critical | Ankita Thomas | New |
| OCPBUGS-93607 | CVE-2026-39835 crypto/ssh DoS (Azure MAPI) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-93608 | CVE-2026-39835 crypto/ssh DoS (MAPI op) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-93859 | CVE-2026-25681 x/net XSS (AWS CAPI) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-93903 | CVE-2026-27145 crypto/x509 DoS (AWS CCM) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-93907 | CVE-2026-27145 crypto/x509 DoS (GCP CCM) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-93908 | CVE-2026-27145 crypto/x509 DoS (Azure CCM) [5.0] | Critical | Ankita Thomas | New |
| OCPBUGS-95028 | CVE-2026-25681 x/net XSS (AWS CAPI) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95029 | CVE-2026-25681 x/net XSS (GCP MAPI) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95233 | CVE-2026-41567 Moby ACE (GCP CAPI) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95234 | CVE-2026-41567 Moby ACE (Azure CAPI) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95485 | CVE-2026-46597 crypto/ssh AES-GCM DoS (Azure CAPI) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95487 | CVE-2026-46597 crypto/ssh AES-GCM DoS (CAPI op) [5.0] | Critical | Matthew Booth | New |
| OCPBUGS-95505 | CVE-2026-46597 crypto/ssh AES-GCM DoS (Azure service) [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-95506 | CVE-2026-46597 crypto/ssh AES-GCM DoS (Azure ACR) [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-95517 | CVE-2026-46597 crypto/ssh AES-GCM DoS (MAPI op) [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-95521 | CVE-2026-46597 crypto/ssh AES-GCM DoS (Azure MAPI) [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-95585 | CVE-2026-39828 crypto/ssh unauthorized cmd exec [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-96693 | CVE-2026-27136 x/net XSS (Azure CAPI) [5.0] | Critical | Rachel Ryan | New |
| OCPBUGS-96694 | CVE-2026-27136 x/net XSS (CAPI op) [5.0] | Critical | Stanislav Jakuschevskij | New |
| OCPBUGS-96695 | CVE-2026-27136 x/net XSS (CPMS) [5.0] | Critical | Stanislav Jakuschevskij | New |
| OCPBUGS-96715 | CVE-2026-25681 x/net XSS (MAPI op) [5.0] | Critical | Stanislav Jakuschevskij | New |
| OCPBUGS-96716 | CVE-2026-39831 crypto/ssh security key bypass [5.0] | Critical | Stanislav Jakuschevskij | New |
| OCPBUGS-96761 | CVE-2026-42306 Moby host file overwrite (AWS CAPI) [5.0] | Critical | Stanislav Jakuschevskij | New |
| OCPBUGS-96782 | CVE-2026-39830 crypto/ssh DoS resource leak [5.0] | Critical | Stanislav Jakuschevskij | New |

## Assignment Distribution (Green Pod Engineers)

| Engineer | Bugs assigned | Keys |
|----------|--------------|------|
| Ankita Thomas | 14 | OCPBUGS-78355, OCPBUGS-78095, OCPBUGS-79668, OCPBUGS-81471, OCPBUGS-78995, OCPBUGS-63649, OCPBUGS-29833, OCPBUGS-92059, OCPBUGS-93607, OCPBUGS-93608, OCPBUGS-93859, OCPBUGS-93903, OCPBUGS-93907, OCPBUGS-93908 |
| Jakub Hadvig | 18 | OCPBUGS-83799, OCPBUGS-54982, OCPBUGS-90834, OCPBUGS-82111, OCPBUGS-27745, OCPBUGS-16633, OCPBUGS-65732, OCPBUGS-55459, OCPBUGS-70112, OCPBUGS-56219, OCPBUGS-14473, OCPBUGS-35735, OCPBUGS-91675, OCPBUGS-91676, OCPBUGS-91683, OCPBUGS-91720, OCPBUGS-91724, OCPBUGS-91725 |
| Jefferson Ramos | 12 | OCPBUGS-84517, OCPBUGS-93314, OCPBUGS-84513, OCPBUGS-54864, OCPBUGS-58468, OCPBUGS-71237, OCPBUGS-91728, OCPBUGS-91731, OCPBUGS-92088, OCPBUGS-93952, OCPBUGS-94055, OCPBUGS-94130 |
| Martin Simka | 15 | OCPBUGS-11622, OCPBUGS-1694, OCPBUGS-39539, OCPBUGS-8252, OCPBUGS-50016, OCPBUGS-78475, OCPBUGS-43798, OCPBUGS-79063, OCPBUGS-93196, OCPBUGS-93197, OCPBUGS-93205, OCPBUGS-93584, OCPBUGS-93585, OCPBUGS-93595, |
| Matthew Booth | 13 | OCPBUGS-84521, OCPBUGS-84569, OCPBUGS-58399, OCPBUGS-92240, OCPBUGS-60085, OCPBUGS-57437, OCPBUGS-62985, OCPBUGS-95028, OCPBUGS-95029, OCPBUGS-95233, OCPBUGS-95234, OCPBUGS-95485, OCPBUGS-95487 |
| ~~Pratik Mahajan~~ | ~~PTO~~ | |
| Rachel Ryan | 15 | OCPBUGS-84518, OCPBUGS-17664, OCPBUGS-62819, OCPBUGS-85793, OCPBUGS-52186, OCPBUGS-69643, OCPBUGS-42785, OCPBUGS-95505, OCPBUGS-95506, OCPBUGS-95517, OCPBUGS-95521, OCPBUGS-95585, OCPBUGS-96693, |
| Stanislav Jakuschevskij | 15 | OCPBUGS-84957, OCPBUGS-91668, OCPBUGS-56742, OCPBUGS-51181, OCPBUGS-61694, OCPBUGS-81513, OCPBUGS-81514, OCPBUGS-78775, OCPBUGS-96694, OCPBUGS-96695, OCPBUGS-96715, OCPBUGS-96716, OCPBUGS-96761, OCPBUGS-96782, |
| Stefano Nardo | 13 | OCPBUGS-92181, OCPBUGS-81679, OCPBUGS-82365, OCPBUGS-48395, OCPBUGS-84497, OCPBUGS-42628, OCPBUGS-81511, OCPBUGS-94168, OCPBUGS-95473, OCPBUGS-96717, OCPBUGS-96734, OCPBUGS-96736, OCPBUGS-96750 |

## Closed This Week

| Key | Summary | Resolution |
|-----|---------|------------|
| OCPBUGS-19413 | Fix demo dynamic plugin dev mode cypress tests | Obsolete |
| OCPBUGS-23712 | 4.15 SAST scan — console-container | Obsolete |
| OCPBUGS-24605 | 4.14 SAST scan — console-container | Obsolete |
| OCPBUGS-24703 | 4.13 SAST scan — console-operator-container | Obsolete |
| OCPBUGS-27448 | 4.16 SAST scan — console-container | Obsolete |
| OCPBUGS-28067 | 4.13 SAST scan — console-container | Obsolete |
| OCPBUGS-28112 | 4.14 SAST scan — console-operator-container | Obsolete |
| OCPBUGS-28423 | 4.12 SAST scan — console-operator-container | Obsolete |
| OCPBUGS-28463 | 4.12 SAST scan — console-container | Obsolete |
| OCPBUGS-39580 | console operator unexpected state transitions (vSphere DNS) | Obsolete |
| OCPBUGS-35051 | SNO upgrade failed — console operator timeout | Closed (old OCP version) |
| OCPBUGS-48702 | Username replaced by User ID after upgrade | Closed (duplicate) |
| OCPBUGS-54623 | AWS security group rules not deleted with LB service | Closed (old OCP version) |
| OCPBUGS-67222 | Can't restore VolumeSnapshot as new PVC from UI | Closed (not a bug) |
