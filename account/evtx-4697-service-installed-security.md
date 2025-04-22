# Security/4697: A Service Was Installed in the System

This event is logged to the **Security** log and indicates that a **new service was installed** on the system. It is commonly used to detect potential **persistence mechanisms** deployed by attackers, or administrative installation of services. This event is generated **only if auditing for system events is enabled**.

> [!NOTE]  
> This event complements **System Event ID 7045**, but is found in the **Security.evtx** log and includes richer audit-related metadata.

---

### 🔍 Behavioral Indications
- [x] **Persistence** (MITRE ATT&CK T1543.003 – Create or Modify System Process: Windows Service)

---

### 📈 Analysis Value
- [x] **Service Name** – Name of the new service  
- [x] **Image Path** – Location of the service executable  
- [x] **Start Type** – Startup configuration  
- [x] **Service Type** – Defines how the service runs  
- [x] **User Context** – Account context under which the service will run  
- [x] **Initiating Account** – The user who installed the service

---

## 🖥️ Operating System Availability
- [x] Windows 11  
- [x] Windows 10  
- [x] Windows Server 2016+  
- [x] Windows Server 2008 R2  

---

## 📁 Artifact Location(s)
- `%SystemRoot%\System32\Winevt\Logs\Security.evtx`

---

## 📖 Artifact Interpretation

| Field Name | Interpretation |
|------------|----------------|
| **Service Name** | Short name of the installed service |
| **Display Name** | Friendly name shown in services.msc |
| **Image Path** | Full path to the service executable |
| **Service Type** | E.g., Win32OwnProcess, Win32ShareProcess |
| **Start Type** | Auto, Manual, Disabled |
| **Account Name** | The account under which the service runs |
| **Subject** | The user who created the service |

---

> [!NOTE]  
> Unlike 7045, this event also reflects auditing and privilege usage — useful for tracing unauthorized service creation.

---

### 🧾 EventData Fields from XML:

| XML Path | Interpretation |
|----------|----------------|
| `EventData/ServiceName` | Internal short name of the service |
| `EventData/DisplayName` | User-facing service name |
| `EventData/ServiceFileName` | Path to the service binary |
| `EventData/ServiceType` | Indicates type of service (e.g., own/shared) |
| `EventData/StartType` | Startup mode (2 = auto, 3 = manual, 4 = disabled) |
| `EventData/AccountName` | Logon account used to run the service |
| `EventData/SubjectUserSid` | SID of account that installed the service |
| `EventData/SubjectUserName` | Username of the installer |
| `EventData/SubjectDomainName` | Domain of the installer |
| `EventData/SubjectLogonId` | Logon session ID of the installer |

---

## 🔒 Security Monitoring Recommendations
- Alert on unknown or unsigned services being installed
- Review services set to auto-start, especially under non-`LocalSystem` accounts
- Investigate any service creation events by low-privileged users or outside maintenance windows
