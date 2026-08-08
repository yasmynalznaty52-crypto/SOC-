<div align="center">

# بسم الله الرحمن الرحيم

# Day 16 — Defensible Network Concepts & Data Centralization

</div>

---

# 🛡️ Defensible Network Concepts Summary

الـ **Defensible Network** مش معناها شبكة مستحيل تتخترق، لكن معناها شبكة معمولة بطريقة تخلينا نقدر:

* نشوف اللي بيحصل فيها **Visibility**
* نكتشف الهجمات **Detection**
* نمنع أكبر قدر ممكن من النشاط الخبيث **Prevention**
* ونتعامل مع اللي قدر يعدي وسائل الحماية **Investigation & Response**

---

## 🌐 1. Network Data Monitoring

لازم نراقب الـ **Network Traffic**، لكن مش جزء واحد من الشبكة فقط.

### Traffic to/from the Internet

لازم نراقب الـ traffic:

* الداخل من الإنترنت إلى الشبكة.
* الخارج من الشبكة إلى الإنترنت.

لأن الـ attacker ممكن يحاول يدخل من الإنترنت، أو جهاز compromised داخل الشبكة ممكن يتصل بـ:

* C2 Server
* Malicious Website
* Attacker Infrastructure

---

### Internal Network Traffic

مش كفاية نراقب:

```text
Internet ↔ Company Network
```

لازم نراقب كمان:

```text
Internal Network
       ↕
Internal Network
```

وده يسمى غالبًا **East-West Traffic**.

وده مهم جدًا لاكتشاف **Lateral Movement**.

مثال:

```text
Compromised PC
      ↓
File Server
      ↓
Domain Controller
```

لو بنراقب الـ Internet Traffic فقط، ممكن الـ attacker يتحرك داخل الشبكة وإحنا مش شايفينه.

---

### ☁️ Cloud Traffic Monitoring

البيئة الحديثة مش كلها On-Premises.

عندنا Cloud Environments زي AWS، وبالتالي لازم نراقب الـ traffic داخل الـ Cloud كمان.

مثال:

```text
AWS VPC
 ├── Server A
 ├── Server B
 └── Database
```

لازم نقدر نعرف:

* مين اتصل بمين؟
* مصدر الاتصال إيه؟
* وجهته إيه؟
* إمتى حصل الاتصال؟
* وإيه نوع الـ traffic؟

ومن أمثلة البيانات المستخدمة:

**AWS VPC Logs**

---

# 2. Layer 7 Transaction Data

الـ Layer 7 هي **Application Layer**.

مش عايزين نعرف فقط:

```text
10.0.0.5 → 10.0.0.10
TCP / 443
```

لكن بالنسبة للـ **Critical Traffic**، نحتاج تفاصيل على مستوى الـ Application.

مثلًا:

```text
Client
   ↓
HTTP Request
   ↓
/admin/login
```

أو:

```text
DNS Query
   ↓
suspicious-domain.com
```

وده بيدينا **Context** أكبر عن اللي حصل.

ومش لازم نجمع كل تفاصيل Layer 7 لكل Traffic، لأن ده ممكن ينتج كمية ضخمة جدًا من البيانات، لذلك نركز بشكل أكبر على **Critical Traffic**.

---

# 💻 3. Endpoint & Application Data Monitoring

الـ Network Monitoring لوحده مش كفاية.

لازم نعرف كمان:

> **إيه اللي حصل داخل الجهاز نفسه؟**

مثال:

الـ Network ممكن تقول:

```text
PC-01 → Suspicious IP
```

لكن الـ Endpoint ممكن يقول:

```text
WINWORD.exe
      ↓
PowerShell.exe
      ↓
Suspicious Process
      ↓
Connection to Suspicious IP
```

الـ Network أخبرتنا أن الاتصال حصل، بينما الـ Endpoint أعطانا **مين البرنامج اللي عمل الاتصال وإيه اللي حصل على الجهاز**.

---

# 📝 4. Critical Log Collection

لازم نجمع الـ important logs من:

### Desktops

مثل:

* Login Events
* Security Events
* Process Creation
* PowerShell Activity

### Servers

مثل:

* Web Servers
* Database Servers
* File Servers
* Domain Controllers

### Appliances

مثل:

* Firewalls
* IDS/IPS
* VPN
* Proxies
* Network Appliances

الفكرة:

> كل جهاز مهم في الـ Environment لازم يكون عندنا منه الـ Logs التي تساعدنا في الـ Detection والتحقيق.

---

# ⚙️ 5. Configuration & Baseline Monitoring

مش كفاية نراقب الـ Events فقط.

لازم نراقب **Configuration Changes** أيضًا.

مثلاً Server كان:

```text
Firewall Enabled
Port 22 Restricted
User X Disabled
```

وفجأة أصبح:

```text
Firewall Disabled
Port 22 Exposed
New Admin Account
```

التغييرات دي ممكن تكون علامة على:

* Compromise
* Malicious Activity
* Misconfiguration

---

## ما هو الـ Baseline؟

الـ **Baseline** هو الشكل الطبيعي أو المتوقع للنظام.

مثلاً:

```text
Normal Server
 ├── CPU: 20%
 ├── Connections: 50
 ├── Processes: 100
 └── Open Ports: 3
```

لو فجأة حصل:

```text
5000 Connections
New Service
New Admin Account
Unknown Process
```

يبقى فيه **Deviation from the Baseline** يستحق التحقيق.

ببساطة:

> **Baseline = What Normal Looks Like**

---

# 🩹 6. Vulnerability Information

محتاجين نعرف كمان الـ **Vulnerabilities** الموجودة في أنظمتنا.

مثلاً:

```text
Server-01
   ↓
Internet-Facing
   ↓
Critical Vulnerability
```

لو ظهر Alert على نفس الـ Server، معرفة الـ vulnerability الموجودة عليه تساعد الـ SOC Analyst في تحديد **Risk & Priority**.

مثال:

```text
Alert
  +
Internet-Facing Server
  +
Known Critical Vulnerability
  ↓
High Priority Investigation
```

---

# 🔐 7. Access & Audit Logs

لازم نعرف مين استخدم الـ Applications والـ Cloud Services وإيه اللي عمله.

مثال:

```text
User
 ↓
Login
 ↓
Access Database
 ↓
Download Large Amount of Data
```

وفي الـ Cloud:

```text
User
 ↓
AWS
 ↓
Create IAM User
 ↓
Grant Administrator Privileges
```

دي كلها Events مهمة للـ Security Monitoring.

---

# 🧠 Network Monitoring vs Endpoint Monitoring

الكتاب بيقسم الموضوع إلى **Campين أساسيين**:

## 1️⃣ Network Security Monitoring — Data in Motion

بنراقب البيانات وهي بتتحرك على الشبكة.

```text
PC ─────→ Server
       Traffic
```

نهتم بـ:

* Network Traffic
* NetFlow
* DNS
* HTTP
* Network Connections
* Cloud Network Logs

والهدف:

> نفهم **إيه نوع الـ Traffic الموجود على الشبكة** ونكتشف النشاط المشبوه.

---

## 2️⃣ Continuous Security Monitoring — Data at Rest

بنراقب المعلومات الناتجة عن النشاط على الـ Endpoints.

مثل:

* Processes
* Files
* Users
* Services
* Security Events
* Application Logs
* Configuration Changes

والهدف:

> نعرف **إيه اللي حصل داخل الجهاز نفسه**.

---

# 🔥 ليه الاتنين لازم يشتغلوا مع بعض؟

تخيلي Attack بالشكل ده:

```text
Attacker
   ↓
User PC
   ↓
PowerShell
   ↓
C2 Server
```

الـ **Network Monitoring** ممكن يقول:

```text
User PC
   ↓
Connected to
   ↓
Suspicious IP
```

لكن الـ **Endpoint Monitoring** يقول:

```text
WINWORD.exe
   ↓
PowerShell.exe
   ↓
Suspicious Process
   ↓
Connected to Suspicious IP
```

إذن:

> **Network tells us what happened on the network.**

بينما:

> **Endpoint tells us what happened on the machine.**

والاتنين مع بعض بيدونا صورة أوضح للـ Attack.

---

# 🛡️ Prevention Is Not Enough

الهدف من الـ Network Monitoring هو إننا نفهم الـ Traffic ونقدر نحط **Preventive Controls** في أماكن استراتيجية.

مثلاً:

```text
Internet
   ↓
Firewall / IDS / IPS
   ↓
Internal Network
   ↓
Endpoints
```

وده يساعدنا نكتشف ونمنع أكبر قدر ممكن من الـ malicious traffic.

لكن:

> **Not all malicious traffic can be blocked.**

الـ attacker ممكن يستخدم:

* Compromised Accounts
* Legitimate Services
* Encrypted Traffic
* Vulnerabilities
* Cloud Credentials
* Lateral Movement

عشان كده الـ Prevention لوحده مش كفاية.

لازم يكون عندنا:

```text
Internal NSM
     +
Cloud Monitoring
     +
Endpoint Monitoring
     ↓
Detection & Investigation
```

وده هو مفهوم **Defense in Depth**.

---

# 📊 Data Centralization Summary

بعد ما عرفنا **إيه البيانات اللي لازم نراقبها**، بيظهر سؤال مهم:

> **هنجمع البيانات دي كلها فين؟**

الإجابة الأساسية:

# SIEM

الهدف إن الـ Monitoring Data يتم **Centralized** في الـ SIEM.

بدل:

```text
Firewall → System 1
Endpoint → System 2
Cloud → System 3
Network → System 4
Server → System 5
```

نحاول نوصلها كلها إلى:

```text
Firewall ───┐
Endpoint ───┤
Network ────┤
Servers ────┼──→ SIEM
Cloud ──────┘
```

---

# ⭐ Why Data Centralization Is Crucial?

الـ SOC Analyst شغله الأساسي هو:

> **Reading and interpreting data**

يعني بيقرأ الـ Events والـ Logs ويحاول يفهم:

* إيه اللي حصل؟
* إمتى حصل؟
* مين عمله؟
* حصل على أنهي جهاز؟
* هل فيه أجهزة أخرى اتأثرت؟
* هل ده Activity طبيعي أم Attack؟

عشان كده لازم الـ Data تكون:

**Centralized + Easily Available + Rich in Context**

---

# ⚠️ مش كل Tool بتطلع Logs جاهزة

مش كل Security Tool بتنتج البيانات بنفس الشكل.

ممكن يكون عندنا:

```text
Network Traffic
NetFlow
Endpoint Logs
Cloud Logs
Application Logs
Binary Data
```

وبعض الـ Tools ممكن ما تطلعش البيانات في صورة Logs جاهزة للـ SIEM.

لذلك أحيانًا نحتاج **Processing / Conversion** قبل إرسال البيانات.

---

# 😩 ليه Multiple Systems مشكلة؟

لو ماعملناش Centralization، هنضطر نستخدم أنظمة متعددة:

```text
SIEM
 ↓
EDR Console
 ↓
Firewall Console
 ↓
Cloud Console
 ↓
Network Console
```

وده:

### Painful

المحلل يضطر يتنقل بين أنظمة كثيرة.

### Fault-prone

كل ما زادت العمليات اليدوية، زادت احتمالية حدوث أخطاء أثناء:

* قراءة الـ Events
* مقارنة الـ Timestamps
* ربط الـ IPs
* Correlating Events

### Inefficient

وقت المحلل يضيع في جمع البيانات بدل ما يستخدمه في:

**Analysis & Investigation**

---

# 🔄 دور الـ Log Collection Agents

الـ **Log Agent** يساعدنا في جمع البيانات وإرسالها للـ SIEM.

مثلاً:

```text
Endpoint
   ↓
Log Collection Agent
   ↓
Logs
   ↓
SIEM
```

الـ Agent ممكن يساعد في:

* Picking up log files
* Shipping logs
* Processing certain formats
* Converting some binary data

---

# 📥 SIEMs Take Logs as Input

دي نقطة مهمة جدًا:

> **SIEMs generally take logs as input.**

لذلك لو عندنا Data مش في صورة Log مناسبة، ممكن نحتاج:

```text
Raw Data
   ↓
Extraction
   ↓
Processing / Conversion
   ↓
Logs
   ↓
SIEM
```

وده اللي شفناه قبل كده مع:

* Network Traffic
* NetFlow
* PCAP
* Binary Data

---

# 🔎 إيه اللي نستفيده لما البيانات تكون Centralized؟

لما الـ Security Data كلها تكون في الـ SIEM، نقدر نعمل:

### Search 🔎

نبحث في مصادر متعددة من مكان واحد.

### Visualization 📊

نعمل Dashboards ونشوف Trends وAnomalies.

### Correlation 🔗

نربط Events من مصادر مختلفة.

مثلاً:

```text
Failed Login
     +
Successful Login
     +
PowerShell Execution
     +
Suspicious Network Connection
     ↓
Possible Compromise
```

### Alerting 🚨

نعمل Rules تقول:

```text
Event A
  +
Event B
  +
Event C
  ↓
ALERT
```

---

# 🧩 Context Is Critical

الهدف مش إننا نجمع أكبر عدد ممكن من الـ Logs وخلاص.

المهم إن البيانات يكون فيها **Context كافي**.

مثلاً بدل ما يكون عندنا:

```text
PC-01 connected to 8.8.8.8
```

نقدر يكون عندنا:

```text
User Login
    ↓
PowerShell Execution
    ↓
Suspicious Process
    ↓
Network Connection
    ↓
Credential Access
```

دلوقتي الـ Analyst يقدر يشوف الـ **Attack Chain** ويفهم القصة بشكل أفضل.

---

# 🔗 الصورة النهائية

كل المفاهيم اللي أخدناها بتتجمع كده:

```text
             Defensible Network
                    ↓
             Monitor Everything
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
     Network      Endpoint     Cloud
        ↓           ↓           ↓
        └───────────┼───────────┘
                    ↓
             Data Collection
                    ↓
          Processing / Conversion
                    ↓
                   SIEM
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
      Search    Correlation   Alerting
        │           │           │
        └───────────┼───────────┘
                    ↓
            SOC Investigation
```

# 🎯 الخلاصة

الفكرة الكبيرة في الجزئين دول:

> **لازم أشوف الـ Network والـ Endpoint والـ Cloud، وبعد كده أجمع البيانات دي في مكان مركزي زي الـ SIEM، عشان أقدر أعمل Search وCorrelation وDetection وأحقق في الـ Attacks بشكل أفضل.**

يعني الـ Blue Team مش بيشتغل كده:

**Prevent → خلاص.**

لكن:

**Monitor → Collect → Centralize → Detect → Investigate**

وده جوهر فكرة الـ **Defensible Network**.
