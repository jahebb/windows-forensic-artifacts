# Security/7045: A Service Was Installed on the System

This event, logged to the **System** channel, indicates that a **new Windows service** was installed on the system. This may represent legitimate administrative activity or the use of Windows services for persistence by a threat actor.

> [!NOTE]  
> In **Windows XP**, there is no direct equivalent for this event ID in the System log.

---

### 🔍 Behavioral Indications
- [x] **Persistence** (MITRE ATT&CK T1543.003 – Create or Modify System Process: Windows Service)

---

### 📈 Analysis Value
- [x] **Service Name** – Identifier used to start/stop the service  
- [x] **Image Path** – Full path to the service executable  
- [x] **Start Type** – Auto, Manual, Disabled, or Delayed  
- [x] **Service Type** – Type of service (e.g., own process, shared process)  
- [x] **Account** – Account used to run the service  

---

## 🖥️ Operating System Availability
- [x] Windows 11  
- [x] Windows 10  
- [x] Windows Server 2016+  
- [x] Windows Server 2008 R2  

---

## 📁 Artifact Location(s)
- `%SystemRoot%\System32\Winevt\Logs\System.evtx`

---

## 📖 Artifact Interpretation

| Field Name | Interpretation |
|------------|----------------|
| **Service Name** | Short name identifier used to manage the service |
| **Image Path** | Executable path of the service being registered |
| **Service Type** | Whether it runs in its own process or shared |
| **Start Type** | Startup configuration: 2 = Auto, 3 = Manual, 4 = Disabled |
| **Account Name** | Account under which the service will run |
| **Subject** | The user account that initiated the installation |

> [!NOTE]  
> You can view these fields in the Event Viewer or extract them from the **XML representation** for structured parsing.

---

### 🧾 EventData Fields from XML:

| XML Path | Interpretation |
|----------|----------------|
| `EventData/ServiceName` | Internal short name of the service |
| `EventData/ImagePath` | Full executable path |
| `EventData/ServiceType` | Type of service (own/shared/driver/etc.) |
| `EventData/StartType` | Startup mode (auto/manual/disabled) |
| `EventData/AccountName` | Account used to run the service |
| `EventData/SubjectUserSid` | SID of user who installed the service |
| `EventData/SubjectUserName` | Username of installer |
| `EventData/SubjectDomainName` | Domain of installer |
| `EventData/SubjectLogonId` | Logon session ID |

