# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 23 - Cyber Kill Chain : THM Lab

## 🔗 Cyber Kill Chain

الـ **Cyber Kill Chain** هو Framework طورته **Lockheed Martin** سنة 2011، مستوحى من مفهوم الـ Military Kill Chain.

الفكرة الأساسية هي فهم المراحل التي يمر بها المهاجم أثناء تنفيذ Cyber Attack، بحيث نقدر نكتشف الهجوم ونوقفه في أقرب مرحلة ممكنة.

### مراحل Cyber Kill Chain

```text
Reconnaissance
      ↓
Weaponization
      ↓
Delivery
      ↓
Exploitation
      ↓
Installation
      ↓
Command & Control
      ↓
Actions on Objectives
```

الهدف الأساسي كـ Defender هو:

> **Break the Kill Chain as early as possible.**

---

# 1️⃣ Reconnaissance

هي مرحلة **Research & Planning**.

المهاجم يجمع معلومات عن الـ Target قبل بدء الهجوم، مثل:

* Infrastructure
* Employees
* Email addresses
* Domains & Subdomains
* IP addresses
* Technologies
* Business processes
* Exposed services

### OSINT

**OSINT = Open-Source Intelligence**

وهو جمع المعلومات من مصادر متاحة للعامة.

أمثلة:

* Search Engines
* Social Media
* Forums & Blogs
* Public Records
* WHOIS
* Technical Data

### أنواع Reconnaissance

#### Passive Recon

لا يوجد Direct Interaction مع الـ Target.

أمثلة:

* WHOIS lookups
* Social Media research
* Public Records
* Breach data

> **Passive = No Direct Interaction**

#### Active Recon

يوجد Direct Interaction مع الـ Target.

أمثلة:

* Port Scanning
* Banner Grabbing
* Service Probing
* Social Engineering

> **Active = Direct Interaction**

### Email Harvesting

هو جمع Email Addresses من مصادر مختلفة.

يمكن استخدام هذه المعلومات في:

```text
Recon
   ↓
Email Harvesting
   ↓
Target Selection
   ↓
Phishing
```

### Recon Tools

* **theHarvester** → Emails, Names, Subdomains, IPs, URLs
* **Hunter.io** → Email/Contact Discovery
* **OSINT Framework** → Collection of OSINT tools and resources

### SOC Perspective

كـ SOC Analyst، فهم الـ Recon يساعدنا على ربط الأحداث.

مثلاً:

```text
Recon
 ↓
Email Harvesting
 ↓
Phishing
 ↓
Delivery
```

---

# 2️⃣ Weaponization

بعد جمع المعلومات، يبدأ المهاجم في تحويلها إلى **Actionable Attack Tools**.

هنا يتم تجهيز:

* Malware
* Exploit
* Payload

### Malware

برنامج مصمم لإحداث ضرر أو تعطيل النظام أو الحصول على Unauthorized Access.

### Vulnerability

ضعف أو ثغرة في Software أو System.

### Exploit

Code أو Program يستغل Vulnerability.

### Payload

Malicious Code يريد المهاجم تشغيله على النظام.

العلاقة:

```text
Vulnerability
      ↓
    Exploit
      ↓
   Payload
```

### أمثلة على Weaponization

#### Malicious Office Documents

يمكن وضع **Malicious Macros / VBA Scripts** داخل Microsoft Office Documents.

```text
Office Document
      ↓
Malicious Macro
      ↓
Malicious Activity
```

#### USB Malware

يمكن وضع Malware على USB drives وتوزيعها على الضحايا.

#### C2 Infrastructure

يمكن تجهيز Infrastructure للتواصل مع الأجهزة المصابة.

#### Backdoor

يمكن تجهيز Backdoor لتوفير طريقة للوصول إلى الجهاز.

#### Phishing Templates

يمكن إنشاء Phishing Templates أو OAuth Consent Apps تبدو Legitimate لخداع الضحية.

### أهم مصطلح

**Macros** = Automated Scripts داخل Microsoft Office Documents ويمكن إساءة استخدامها لتنفيذ Malicious Actions.

---

# 3️⃣ Delivery

بعد تجهيز الـ Payload، يحتاج المهاجم إلى **إيصاله إلى Target**.

> **Delivery = Transmitting the Payload to the Target**

### طرق Delivery

## Phishing Email

إرسال Email يحتوي على:

* Malicious Link
* Malicious Attachment

### Spear Phishing

Phishing موجه إلى شخص محدد.

```text
Recon
 ↓
Identify Employee
 ↓
Spear Phishing
```

## USB Drop

استخدام USB مصاب وإيصاله للضحية، مثل تركه في:

* Parking
* Coffee Shop
* Public Places

وقد يحاول المهاجم جعل الـ USB يبدو Legitimate.

## Watering Hole Attack

هجوم يستهدف مجموعة معينة عن طريق اختراق Website تقوم المجموعة بزيارته باستمرار.

```text
Target Group
      ↓
Frequently Visited Website
      ↓
Attacker Compromises Website
      ↓
Victim Visits Website
      ↓
Malicious Content
```

### Drive-by Download

يمكن أن يؤدي الدخول إلى موقع ضار أو مخترق إلى تنزيل Malware أو Malicious Application.

### الفرق

| Method            | Delivery            |
| ----------------- | ------------------- |
| Phishing          | Email               |
| Spear Phishing    | Targeted Email      |
| USB Drop          | USB                 |
| Watering Hole     | Compromised Website |
| Drive-by Download | Malicious Download  |

---

# 4️⃣ Exploitation

هي اللحظة التي يتم فيها **تنفيذ الـ Attacker's Code على الـ Target** واستغلال Vulnerability.

```text
Vulnerability
      ↓
    Exploit
      ↓
Code Execution
      ↓
Compromise
```

### طرق Exploitation

## Malicious Macro Execution

يمكن أن يتم إرسال Office Document عن طريق Phishing، وعند تشغيل الـ Macro يتم تنفيذ Malicious Code.

## Zero-Day Exploit

استغلال Vulnerability غير معروفة أو غير مُصلحة من الـ Vendor وقت الاستغلال.

> **Zero-Day = Unknown/Unpatched Vulnerability at the time of exploitation**

## Known CVEs

استغلال Vulnerabilities معروفة ومسجلة كـ CVEs، ولكن النظام لم يتم Patch له.

```text
Known Vulnerability
      ↓
CVE
      ↓
Patch Available
      ↓
No Patch
      ↓
Exploitation
```

### بعد Exploitation

قد يحاول المهاجم:

* Privilege Escalation
* Lateral Movement

### Signs of Exploitation

* Unexpected Process Spawns
* Registry Changes
* New Services
* Suspicious Command-Line Arguments

### أهم إجابة

> Cyber attack exploiting a software vulnerability unknown to the vendor = **Zero-Day Exploit**

---

# 5️⃣ Installation

بعد الحصول على Access، يريد المهاجم أن يحافظ على وجوده داخل النظام.

> **Persistence = Maintaining Access**

## Backdoor

الـ Backdoor هو Access Point يسمح للمهاجم بالوصول إلى النظام وتجاوز بعض Security Mechanisms.

```text
Initial Access
      ↓
Install Backdoor
      ↓
Persistent Access
```

## Persistent Backdoor

يسمح للمهاجم بالعودة إلى الجهاز حتى لو:

* فقد الاتصال
* تم اكتشاف الـ Initial Access
* تم حذف الـ Initial Access
* تم عمل Patch للـ Vulnerability

---

## طرق Persistence

### 1. Web Shell

Malicious Script على Web Server.

يمكن أن يكون مكتوبًا باستخدام:

* PHP
* ASP
* ASPX
* JSP

```text
Web Server
    ↓
Malicious Script
    ↓
Web Shell
    ↓
Attacker Access
```

### 2. Backdoor

يمكن تثبيت Backdoor على Victim Machine.

مثال:

**Meterpreter**

وهو Payload من Metasploit Framework يسمح للمهاجم بالتفاعل مع الجهاز عن بعد.

### 3. Windows Services

يمكن للمهاجم إنشاء أو تعديل Windows Services لتشغيل Malicious Payload.

MITRE ATT&CK:

> **T1543.003 — Windows Service**

يمكن أيضًا استخدام **Masquerading** لجعل الـ Malicious Service يبدو كأنه Legitimate Service.

### 4. Registry Run Keys / Startup Folder

يمكن إضافة Malicious Payload إلى Run Keys أو Startup Folder بحيث يتم تشغيله عند Login.

```text
User Login
     ↓
Run Keys / Startup Folder
     ↓
Malicious Payload Executes
```

MITRE ATT&CK:

> **T1547.001**

### 5. Timestomping

تعديل File Timestamps مثل:

* Modified
* Accessed
* Created

الهدف الأساسي:

> **Defense Evasion / Anti-Forensics**

مثلاً Malware تم إنشاؤه اليوم، لكن المهاجم يجعله يبدو وكأنه موجود من سنوات.

MITRE ATT&CK:

> **T1070.006 — Timestomp**

### SOC Detection

ابحث عن:

* New Services
* Registry Changes
* Suspicious Web Files
* Unknown Executables
* Timestamp Anomalies
* Persistence + Suspicious Network Connections

> **مهم:** Timestomping ليس Persistence بحد ذاته، وإنما يستخدم لإخفاء الآثار.

---

# 6️⃣ Command & Control — C2

بعد الحصول على Persistence، يحتاج المهاجم إلى التواصل مع الجهاز المصاب والتحكم فيه عن بُعد.

> **C2 = Command and Control**

```text
Attacker
    ↓
C2 Server
    ↕
Malware on Victim
```

يمكن للمهاجم إرسال Commands واستقبال Data من الجهاز.

## C2 Beaconing

الجهاز المصاب يتواصل مع C2 Server بشكل متكرر ومنتظم.

مثلاً:

```text
10:00 → C2 Request
10:05 → C2 Request
10:10 → C2 Request
10:15 → C2 Request
```

لذلك يسمى:

> **Beaconing**

## Common C2 Channels

### HTTP / HTTPS

* HTTP → Port 80
* HTTPS → Port 443

استخدام Web Traffic قد يساعد Malware على الاختلاط مع Legitimate Traffic.

### DNS C2

الجهاز المصاب يقوم بعمل Regular DNS Requests إلى DNS Server أو Domain تحت سيطرة المهاجم.

ويُعرف هذا النوع من C2 Communication باسم:

> **DNS Tunneling**

```text
Victim
  ↓
DNS Requests
  ↓
Attacker-Controlled DNS
  ↓
C2
```

### SOC Perspective

Regular DNS Requests إلى Suspicious Domain وبشكل دوري قد تكون Indicator of C2 Beaconing، لكن يجب تحليل:

* Domain
* Frequency
* Destination
* Process
* Network Traffic
* Endpoint Evidence

---

# 7️⃣ Actions on Objectives

آخر مرحلة هي تنفيذ **الهدف الحقيقي للهجوم**.

بعد الحصول على Hands-on-Keyboard Access يستطيع المهاجم:

### Credential Collection

جمع Credentials من المستخدمين.

### Privilege Escalation

الحصول على صلاحيات أعلى.

```text
Normal User
    ↓
Administrator
    ↓
Domain Administrator
```

### Internal Reconnaissance

استكشاف الأنظمة الداخلية والبحث عن:

* Vulnerabilities
* Valuable Systems
* Internal Applications

### Lateral Movement

التحرك بين الأجهزة والأنظمة داخل الشبكة.

```text
PC-01
 ↓
Server-01
 ↓
Server-02
```

### Data Collection & Exfiltration

جمع البيانات الحساسة وإخراجها خارج المؤسسة.

```text
Sensitive Data
      ↓
Collection
      ↓
Exfiltration
      ↓
Attacker
```

### Delete Backups / Shadow Copies

المهاجم قد يحذف Backups وShadow Copies لمنع Recovery.

### Shadow Copy

**Volume Shadow Copy Service (VSS)** هي تقنية في Microsoft Windows تستطيع إنشاء Backup Copies / Snapshots للملفات أو Volumes حتى أثناء استخدامها.

> **Answer: Volume Shadow Copy Service (VSS)**

### Data Destruction

المهاجم قد يقوم بـ:

* Overwriting Data
* Corrupting Data
* Deleting Backups

---

# ⚠️ Limitations of Traditional Cyber Kill Chain

هل Cyber Kill Chain كافية وحدها؟

> **No.**

هي Framework ممتازة لفهم Attack Flow، لكنها ليست مثالية للدفاع الحديث.

## 1. Old Model

الـ Traditional Cyber Kill Chain تم تطويرها في **2011**.

Cyber Threats تطورت بشكل كبير منذ ذلك الوقت.

## 2. Network Perimeter Focus

تم تصميمها بشكل أساسي مع التركيز على:

* Network Perimeter
* Malware Delivery
* External Threats

لكن Modern Attacks أكثر تعقيدًا.

## 3. Modern Adversaries Use Multiple TTPs

**TTP = Tactics, Techniques, and Procedures**

المهاجم يمكن أن يجمع:

```text
Phishing
+
Credential Theft
+
Privilege Escalation
+
Lateral Movement
+
Persistence
+
Data Exfiltration
```

## 4. Indicators Can Change

Threat Intelligence قد تعتمد على:

* IP Addresses
* Domains
* File Hashes

المهاجم يمكن أن يغير هذه Indicators.

مثلاً:

```text
Malware Hash
    ↓
Modified Malware
    ↓
New Hash
```

لذلك الاعتماد على Hashes أو IPs فقط غير كافٍ.

## 5. Insider Threats

الـ Traditional Kill Chain ليست مناسبة بشكل كامل لاكتشاف Insider Threats.

**Insider Threat:**

> Insider يستخدم الـ Authorized Access أو معرفته بالمؤسسة لإلحاق الضرر بها.

مثال:

```text
Employee
   ↓
Legitimate Access
   ↓
Misuse of Access
   ↓
Data Theft
```

هنا الشخص بالفعل داخل الـ Network ولا يحتاج إلى اختراق الـ Perimeter.

---

# 🔄 Cyber Kill Chain vs MITRE ATT&CK

لا نعتمد على Cyber Kill Chain وحدها.

يمكن دمجها مع:

* **MITRE ATT&CK**
* **Unified Kill Chain**
* SIEM
* EDR
* Threat Intelligence
* Network Monitoring

### Cyber Kill Chain

تساعدنا في فهم:

> **Where is the attacker in the attack lifecycle?**

### MITRE ATT&CK

تساعدنا في فهم:

> **What tactics and techniques is the adversary using?**

---

# 🧠 SOC Analyst Mindset

بدل ما أشوف الـ Alert كحدث منفصل:

```text
Alert → Close
```

أبدأ أفكر:

```text
What happened?
      ↓
Which Kill Chain phase?
      ↓
What happened before?
      ↓
What happened after?
      ↓
Which MITRE ATT&CK Technique?
      ↓
How can I break the attack chain?
```

مثال:

```text
Phishing Email
      ↓
Delivery

Malicious Process
      ↓
Exploitation

New Persistence Mechanism
      ↓
Installation

Suspicious Outbound Connection
      ↓
C2

Data Exfiltration
      ↓
Actions on Objectives
```

هنا أنا لا أرى 5 Alerts منفصلة.

أنا أرى:

> **Attack Story**

---

# 🎯 أهم ما استفدناه من Cyber Kill Chain

### 1️⃣ الـ Attack عبارة عن سلسلة

الهجوم ليس Event واحد، وإنما مجموعة مراحل مترابطة.

### 2️⃣ Early Detection مهم جدًا

كلما اكتشفنا المهاجم مبكرًا، كان إيقافه أسهل.

> **Break the Kill Chain**

### 3️⃣ Alert لوحده لا يكفي

لازم نربط الـ Events ببعض ونفهم الـ Attack Chain.

### 4️⃣ كل مرحلة لها Indicators

مثلاً:

```text
Recon → Scanning / Enumeration
Delivery → Phishing
Exploitation → Suspicious Execution
Installation → Persistence
C2 → Beaconing
Objectives → Data Theft / Destruction
```

### 5️⃣ Cyber Kill Chain ليست كافية وحدها

نستخدمها مع:

> **MITRE ATT&CK + Unified Kill Chain + SIEM + EDR + Threat Intelligence**

---

# 📝 Final Cheat Sheet

```text
1. Reconnaissance
   → Gather information about the target.

2. Weaponization
   → Prepare Malware / Exploit / Payload.

3. Delivery
   → Deliver the payload to the victim.

4. Exploitation
   → Exploit a vulnerability and execute code.

5. Installation
   → Establish persistence / maintain access.

6. Command & Control
   → Communicate with and control the compromised host.

7. Actions on Objectives
   → Achieve the attacker's final goal.
```

### أهم Terms في الروم

| Term             | Meaning                                        |
| ---------------- | ---------------------------------------------- |
| OSINT            | Open-Source Intelligence                       |
| Passive Recon    | Recon without direct interaction               |
| Active Recon     | Recon with direct interaction                  |
| Macros           | Automated Office scripts                       |
| Watering Hole    | Compromised website targeting a specific group |
| Zero-Day         | Unknown/unpatched vulnerability                |
| Backdoor         | Unauthorized access point                      |
| Persistence      | Maintaining access                             |
| Web Shell        | Malicious web script used to maintain access   |
| Timestomping     | Modifying file timestamps                      |
| C2               | Command and Control                            |
| Beaconing        | Repeated communication with C2                 |
| DNS Tunneling    | Using DNS as a C2 channel                      |
| VSS              | Windows Volume Shadow Copy Service             |
| TTP              | Tactics, Techniques, Procedures                |
| Lateral Movement | Moving between systems                         |
| Exfiltration     | Stealing/transferring data outside             |

# 💡 Day 23 — What I Learned

> **Cyber Kill Chain taught me to stop looking at security alerts as isolated events and start viewing them as connected stages of an attack.**

كـ SOC Analyst، أهم Skill خرجنا بيها من الروم هي:

> **Identify the attack phase → correlate the evidence → understand the adversary's behavior → detect early → break the Kill Chain.**
