# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Event Log Flow

بصي للصورة الكبيرة الأول:

```text
Network Events ───┐
                  ├──→ Logs ──→ SIEM ──→ Analytics
Endpoint Events ──┘                  ↓
                                  ALERT
                                    ↓
                               Triage Queue
                                    ↓
                              SOC Analyst
                                    ↓
                         Incident Management
```

يعني السلسلة الأساسية:

> **Event → Log → SIEM → Detection → Alert → Triage → Incident Management**

خلينا نفكها واحدة واحدة.

---

# 1. Events Occur

كل حاجة بتبدأ بـ **Event**.

والـ Events ممكن تحصل من مصادر مختلفة، ومن أهمها في السلايد:

## Network Events

أحداث بتحصل على مستوى الشبكة، زي:

```text
Client → Server
DNS Query
HTTP Request
Network Connection
Firewall Event
VPN Login
```

مثلاً:

```text
10.0.0.5 → 185.x.x.x:443
```

ده **Network Event**.

---

## Endpoint Events

الأحداث اللي بتحصل على الأجهزة نفسها.

مثلاً:

```text
User Login
Process Creation
PowerShell Execution
File Creation
Service Started
Registry Modification
```

مثال:

```text
powershell.exe
      ↓
Process Created
```

ده **Endpoint Event**.

---

# 2. Events Become Logs

إحنا قلنا قبل كده إن الـ Event هو:

> **Any observable occurrence**

لكن الـ SIEM محتاج بيانات منظمة يقدر يتعامل معاها.

فالأحداث بتتسجل في صورة **Logs**.

مثلاً:

```text
Event:
User opened PowerShell
```

يتسجل كـ Log يحتوي على معلومات زي:

```text
Timestamp
User
Process
Command
Host
IP
```

ونفس الفكرة بالنسبة للـ Network Events.

---

# 3. Centralization

بعد كده الـ Logs من المصادر المختلفة يتم **Centralized**.

يعني:

```text
Network Logs ────┐
                 │
Endpoint Logs ───┼──→ SIEM
                 │
Cloud Logs ──────┘
```

وده بيرجعنا للسلايد اللي فات:

> **Centralization of data is crucial.**

بدل ما كل البيانات تكون موزعة في عشرات الأنظمة، بنحاول نوصلها لمكان مركزي.

---

# 4. SIEM

وهنا بيبدأ الدور الحقيقي للـ **SIEM**.

الكتاب بيقول إن الـ SIEM متخصص في:

> **Mass parsing, enriching, and inspecting of log data**

يعني عنده 3 أدوار مهمة جدًا:

### Parsing

يفهم الـ Logs ويحولها من Text/Raw Data إلى Fields منظمة.

مثلاً:

```text
Raw Log
   ↓
Parsing
   ↓
Source IP
Destination IP
User
Process
Timestamp
Action
```

---

### Enrichment

دي مهمة جدًا.

الـ SIEM ممكن يضيف معلومات إضافية للـ Event تساعد في فهمه.

مثلاً عندنا:

```text
Destination IP:
185.x.x.x
```

الـ SIEM ممكن يضيف:

```text
Threat Intelligence:
Known Malicious IP

Country:
Russia

ASN:
XXXXX

Reputation:
Malicious
```

فبدل ما عندنا Event ناقص، بقى عندنا Event فيه **Context أكبر**.

وده هو معنى:

> **Enrichment**

---

### Inspection / Analysis

الـ SIEM يبدأ يفحص البيانات ويشوف:

> هل الـ Event ده طبيعي؟ ولا فيه حاجة suspicious؟

وهنا ندخل على الـ **Analytics Rules**.

---

# 5. Analytics Rules

السلايد بيقول:

> **Analytics = rules for detection conditions of interest**

يعني الـ SIEM عنده Rules بتقول:

> لو شفت Pattern معين → اعتبره Interesting.

مثلاً Rule:

```text
5 Failed Logins
      +
1 Successful Login
      ↓
ALERT
```

أو:

```text
PowerShell
      +
Encoded Command
      +
External Connection
      ↓
ALERT
```

أو:

```text
Endpoint
      ↓
Connection to Known Malicious IP
      ↓
ALERT
```

---

# 6. مش كل Event يبقى Alert

دي نقطة مهمة جدًا.

عندنا مثلًا:

```text
1,000,000 Events
```

الـ SIEM مش هيطلع:

```text
1,000,000 Alerts
```

وإلا الـ SOC Analyst هينتحر.

الـ SIEM بيعمل Filtering وAnalysis.

مثلاً:

```text
1,000,000 Events
       ↓
Analytics Rules
       ↓
1,000 Interesting Events
       ↓
Alerts
```

يعني:

> **Event of interest → Alert**

---

# 7. Elevate Event to Alert

دي جملة مهمة في السلايد:

> **Once an event of interest is identified, that individual log can be elevated to an alert.**

يعني الـ Event في البداية مجرد Log.

لكن لما الـ SIEM يحدد إنه **Interesting / Suspicious**:

```text
EVENT
  ↓
Detection Rule Matches
  ↓
ALERT
```

فممكن نقول إن الـ Alert هو:

> **An Event that has been identified as interesting enough to require attention.**

لكن لسه مش Incident.

---

# 8. الـ Alert بياخد معاه Additional Information

السلايد بيقول:

> **that log is typically then sent with any additional info that helped identify it as potentially evil**

يعني لما الـ Event يتحول إلى Alert، مش بنبعت الـ Log الخام بس.

بنرسل معاه الـ **Context** اللي ساعدنا نعتبره suspicious.

مثلاً:

```text
Alert:
Suspicious Network Connection

Source:
10.0.0.5

Destination:
185.x.x.x

Process:
powershell.exe

User:
user1

Threat Intelligence:
Known Malicious IP

Detection Rule:
Suspicious PowerShell C2
```

كده الـ Analyst عنده معلومات أكتر يبدأ بيها التحقيق.

---

# 9. Triage Queue

بعد ما الـ Alert يتعمل، بيتحط في:

> **Triage Queue**

يعني قائمة الـ Alerts اللي محتاجة Analyst Review.

مثلاً:

```text
┌───────────────────────────────┐
│       Triage Queue             │
├───────────────────────────────┤
│ Critical - Malware            │
│ High - Suspicious Login       │
│ Medium - PowerShell           │
│ Low - Policy Violation        │
└───────────────────────────────┘
```

الـ SOC Analyst يبدأ ياخد الـ Alerts من الـ Queue ويعمل عليها **Triage**.

---

# 10. Triage

الـ **Triage** يعني إن الـ Analyst يحاول يحدد:

> **هل الـ Alert ده حقيقي ومهم؟ ولا False Positive؟**

بيسأل:

* إيه اللي حصل؟
* مين المستخدم؟
* إيه الجهاز؟
* إمتى حصل؟
* هل الـ IP malicious؟
* إيه الـ Process؟
* هل فيه Events أخرى مرتبطة؟
* هل ده behavior طبيعي؟
* هل فيه Evidence على compromise؟

---

# لو False Positive

مثلاً:

```text
Alert
 ↓
Investigation
 ↓
Legitimate Activity
 ↓
False Positive
```

خلاص، مش Incident.

---

# لو True Positive

لو الـ Analyst اكتشف:

```text
Alert
 ↓
Investigation
 ↓
Malicious Activity Confirmed
```

يبقى عندنا:

# Incident

وهنا ممكن الـ Alert يتبعت إلى:

> **Incident Management System**

---

# 11. Incident Management System

ده النظام اللي بنستخدمه لإدارة الـ Incident بعد ما نتأكد إن الموضوع حقيقي.

يعني بدل ما يفضل الموضوع مجرد Alert في الـ SIEM، يبدأ يبقى **Incident له Case / Ticket**.

مثلاً:

```text
SIEM Alert
    ↓
Triage
    ↓
Confirmed Incident
    ↓
Incident Management System
    ↓
Investigation / Response
    ↓
Resolution
```

ممكن يتم تسجيل:

* Incident Description
* Affected Systems
* Users
* Indicators
* Timeline
* Investigation Notes
* Actions Taken
* Evidence
* Status
* Resolution

---

# مثال كامل من البداية للنهاية

خلينا ناخد Scenario حقيقي:

## Step 1 — Endpoint Event

User فتح ملف Word malicious.

```text
WINWORD.EXE
     ↓
PowerShell.exe
```

ده:

**Endpoint Event**

---

## Step 2 — Network Event

PowerShell بدأ اتصال بـ:

```text
185.x.x.x:443
```

ده:

**Network Event**

---

## Step 3 — Logs

الاتنين اتسجلوا:

```text
Endpoint Log
+
Network Log
```

---

## Step 4 — SIEM

الـ Logs دخلت الـ SIEM.

الـ SIEM عمل:

```text
Parsing
+
Enrichment
+
Correlation
```

---

## Step 5 — Analytics Rule

الـ SIEM عنده Rule:

```text
Office Application
      ↓
PowerShell
      +
External Network Connection
      ↓
Suspicious Behavior
```

الـ Rule Match حصل.

---

## Step 6 — Alert

الـ Event يتم **elevated to Alert**:

```text
Suspicious PowerShell Activity
```

ومعه Context:

```text
User: user1
Host: PC-01
Process: powershell.exe
Parent: WINWORD.EXE
Destination: 185.x.x.x
Threat Intel: Malicious
```

---

## Step 7 — Triage

الـ SOC Analyst يراجع:

```text
Who?
What?
When?
Where?
How?
```

ويكتشف إن الـ IP malicious والـ PowerShell فعلاً نفذ payload.

---

## Step 8 — Incident

يبقى:

```text
Confirmed Malicious
        ↓
INCIDENT
```

ويتم إرساله إلى:

**Incident Management System**

علشان يبدأ الـ Investigation وResponse.

---

# اربطي السلايد بكل اللي أخدناه

السلايدات السابقة كانت بتشرح كل جزء لوحده.

دلوقتي ده بيجمعهم:

```text
             NETWORK
                │
             EVENTS
                │
                ├──────────┐
                │          │
                ↓          ↓
              LOGS       ENDPOINT
                │          │
                │        EVENTS
                │          │
                └────┬─────┘
                     ↓
                   SIEM
                     ↓
            Parsing / Enrichment
                     ↓
              Analytics Rules
                     ↓
              Interesting Event
                     ↓
                   ALERT
                     ↓
              Triage Queue
                     ↓
              SOC Analyst
                     ↓
            ┌────────┴────────┐
            ↓                 ↓
      False Positive     Confirmed
            ↓                 ↓
          Close            INCIDENT
                              ↓
                    Incident Management
```

# أهم حاجة تطلعي بيها

السلايد ده عايزك تفهمي إن الـ SOC **مش بيبدأ بالـ Alert**.

الـ Alert له رحلة كاملة:

> **Events happen → Events become Logs → Logs are centralized → SIEM parses/enriches them → Analytics Rules detect interesting activity → Event becomes Alert → Analyst performs Triage → Confirmed malicious activity becomes an Incident → Incident Management takes over.**

وبالتالي احفظي الـ Flow ده كويس جدًا:

### **Event → Log → SIEM → Enrichment/Analytics → Alert → Triage → Incident Management**

---

# Alert Collection

أول حاجة لازم تثبتيها:

> **Log ≠ Event ≠ Alert**

الـ **Log** هو طريقة تسجيل/تمثيل البيانات.

أما الـ **Event أو Alert** فهو **إيه اللي الـ Log بيمثله**.

يعني ممكن يكون عندي:

```text
Log
 ↓
represents an Event
```

أو:

```text
Log
 ↓
represents an Alert
```

وده بالضبط اللي السلايد بيتكلم عنه.

---

# 1. Event Log vs Alert Log

إحنا قبل كده شفنا Event Logs زي:

```text
User Login
DNS Query
Network Connection
HTTP Request
Process Creation
```

دي بتقول:

> **Something happened.**

لكن Security Appliances زي:

* IDS
* IPS
* Firewalls
* EDR

ممكن تكون أصلًا عملت Detection وطلعت **Alert**.

يعني الـ Device نفسه شاف حاجة suspicious وقال:

> **"أنا شايف نشاط ممكن يكون malicious."**

فالـ Log اللي الجهاز بيبعته للـ SIEM مش مجرد Event عادي، ده **Alert Log**.

---

# المثال الأول — Snort IDS Alert

السلايد فيه:

```text
12/12-06:22:52.879193 [**]
[1:2014126:1] ET CURRENT_EVENTS DRIVEBY
Blackhole Likely Flash Exploit Request /field.swf
[Classification: A Network Trojan was Detected]
[Priority: 1] {TCP}

192.168.45.10:1046
    ->
78.46.173.138:80
```

ده Alert من:

**Snort IDS**

خلينا نفهمه.

---

## مين اتصل بمين؟

```text
192.168.45.10:1046
        ↓
78.46.173.138:80
```

يعني الجهاز الداخلي:

**192.168.45.10**

عمل اتصال بـ:

**78.46.173.138**

على Port:

**80**

يعني HTTP.

---

# لكن Snort شاف حاجة مش طبيعية

الـ Signature بيقول:

```text
Blackhole Likely Flash Exploit Request
```

يعني Snort شاف Network Traffic بيطابق Pattern مرتبط بـ:

**Blackhole Exploit Kit / Flash Exploit**

والـ Classification:

```text
A Network Trojan was Detected
```

والـ Priority:

```text
1
```

يعني الـ IDS مش بيقول:

> "كان فيه Network Connection."

هو بيقول:

> **"أنا اكتشفت Traffic يطابق Pattern لنشاط malicious/suspicious."**

وده فرق كبير جدًا.

---

# Event ولا Alert؟

لو كان عندنا Log بيقول:

```text
192.168.45.10 → 78.46.173.138:80
```

بس من غير أي Detection:

ده:

**Network Event**

لكن Snort عمل:

```text
Traffic
 ↓
Signature Match
 ↓
Potential Exploit
```

إذن:

# Alert

---

# هل معنى Alert إن الجهاز اتصاب 100%؟

**لا.**

ودي نقطة مهمة جدًا.

الـ Snort Alert بيقول إن:

> **Potentially infected**

يعني الجهاز **قد يكون اتصاب**.

لكن لسه محتاج **Triage / Investigation**.

ممكن يكون:

* True Positive
* False Positive
* Attempted Exploitation
* Successful Exploitation

فالـ Alert مش هو نفسه Incident.

---

# 2. المثال الثاني — Palo Alto Threat Log

السطر التاني جاي من:

**Palo Alto Firewall**

والـ Log بيقول إن:

```text
192.168.0.2
```

اتصل بـ:

```text
onlinebrandsecuritys.com
```

والـ URL مرتبط بـ:

```text
malware-sites
```

وكمان حصل:

```text
ws.zip
```

وهو ملف ZIP suspicious.

---

# إيه اللي حصل هنا؟

بشكل مبسط:

```text
192.168.0.2
      ↓
onlinebrandsecuritys.com
      ↓
Suspicious URL
      ↓
ws.zip
      ↓
Malware-related detection
```

فالـ Palo Alto مش مجرد بيسجل:

> "User visited a website."

هو بالفعل عمل Detection وقال:

> **"الـ URL ده معروف إنه malicious/suspicious."**

إذن الـ Log ده يمثل:

# Alert

---

# الفرق بين المثالين

### Snort

شاف:

```text
Network Traffic
      ↓
Matched Exploit Signature
      ↓
ALERT
```

### Palo Alto

شاف:

```text
URL Connection
      ↓
Known Malicious URL
      ↓
ALERT
```

الاتنين Security Appliances وعملوا Detection **قبل ما البيانات توصل للـ SIEM**.

---

# ودي أهم نقطة في السلايد

الكتاب بيقول:

> **Some logs represent alerts!**

يعني مش لازم الـ SIEM هو أول مكان يحصل فيه Detection.

ممكن الـ Detection يحصل **قبل الـ SIEM**.

مثلاً:

```text
Network Traffic
      ↓
       IDS
      ↓
Detection
      ↓
Alert Log
      ↓
SIEM
```

بدل:

```text
Network Traffic
      ↓
      SIEM
      ↓
Detection Rule
      ↓
Alert
```

الاتنين ممكن يحصلوا.

---

# قارنِي بين الـ Event والـ Alert Log

## Event Log

بيمثل:

> **Something happened.**

مثلاً:

```text
User logged in
```

الـ SIEM بعد كده ممكن يحلل الـ Event ويكتشف إنه suspicious.

---

## Alert Log

بيمثل:

> **A security tool already detected something suspicious.**

مثلاً:

```text
IDS:
Blackhole exploit detected
```

يعني الـ Security Tool سبق وعمل Detection.

---

# الصورة الكبيرة

عندنا نوعين من الـ Logs:

```text
                    LOGS
                     │
            ┌────────┴────────┐
            ↓                 ↓
      Event Logs         Alert Logs
            │                 │
            ↓                 ↓
   "Something happened"  "Something suspicious
                          was detected"
            │                 │
            └────────┬────────┘
                     ↓
                    SIEM
```

---

# 3. ليه لازم نفرق بينهم في الـ SIEM؟

لأن الكتاب بيقول:

> **These logs need to be handled differently in the SIEM than normal events.**

ليه؟

لأن الـ Event Log لسه محتاج Detection.

لكن الـ Alert Log:

**Security Tool already found something suspicious.**

يعني مستوى الـ Context مختلف.

مثلاً:

### Event

```text
User connected to IP 185.x.x.x
```

الـ SIEM محتاج يسأل:

> هل الـ IP ده malicious؟

---

### Alert

```text
IDS:
Connection matched known C2 signature
```

هنا عندك بالفعل:

> **Detection Result**

فمينفعش تعامل الاتنين بنفس الطريقة بالضرورة.

---

# طرق التعامل مع Alert Logs

مفيش Architecture واحدة لازم كل الـ SOCs تستخدمها. فيه أكتر من طريقة ممكنة حسب البيئة.

## Option 1 — Triage in IDS

ممكن يكون عندنا:

```text
IDS
 ↓
Analyst Triage
 ↓
Only Important Alerts
 ↓
SIEM
```

يعني الـ **SOC Analyst** يراجع الـ IDS Alerts الأول، وبعد كده الـ Alerts المهمة فقط هي اللي تدخل الـ SIEM.

### الميزة

* تقليل الـ **Noise** قبل ما البيانات تدخل الـ SIEM.
* تقليل حجم البيانات والـ Alerts اللي محتاجة معالجة.

### العيب

* ممكن نفقد **Context** مهم.
* مفيش **Centralization** كاملة لكل الـ Alerts.
* لو الـ Alerts المهمة ما وصلتش للـ SIEM، ممكن نخسر فرصة للـ Correlation مع مصادر أخرى.

---

## Option 2 — Send Everything to SIEM

ممكن ندخل كل الـ IDS Alerts إلى الـ SIEM:

```text
IDS
 ↓
All Alert Logs
 ↓
SIEM
 ↓
Centralized Triage
```

كده كل الـ Alerts بتروح لمكان مركزي، والـ SIEM يقدر يربطها مع:

* Endpoint Logs
* Network Logs
* Authentication Logs
* Cloud Logs

وده ممكن يدي الـ Analyst **Context أكبر** أثناء التحقيق.

مثلاً:

```text
IDS Alert
    +
Endpoint Log
    +
Authentication Log
    +
Network Log
    ↓
SIEM Correlation
    ↓
Better Context
```

---

## Option 3 — Send Important Alerts Directly to Ticketing / Incident Management

ممكن نحول الـ Alerts المهمة إلى **Alert Ticket**:

```text
Security Appliance
        ↓
Critical Alert
        ↓
Ticketing / Incident Management
```

وده ممكن يكون مناسب جدًا للـ **High / Critical Confidence Alerts**.

لكن لو عملنا ده لكل Alert:

```text
10,000 Alerts
      ↓
10,000 Tickets
```

ممكن نغرق الـ **Incident Management System** في Tickets، والـ SOC مش هيقدر يتعامل معاها بكفاءة.

---

# مفيش إجابة واحدة صح

وده بالضبط اللي الكتاب بيقوله:

> **There are multiple possible valid answers here.**

يعني مفيش Architecture واحدة لازم كل SOCs تستخدمها.

القرار يعتمد على:

* حجم البيئة
* كمية الـ Alerts
* جودة الـ Detection
* False Positive Rate
* قدرة الـ SOC Team
* SIEM Cost
* سرعة الـ Response المطلوبة
* أهمية الـ Alert

---

# مثال يوضح المشكلة

تخيلي IDS بيطلع:

```text
10,000 Alerts/day
```

ولو عملنا:

```text
ALL IDS ALERTS
      ↓
Ticketing System
```

هيبقى عندك:

```text
10,000 Tickets
```

والـ SOC مش هيقدر يتعامل معاهم.

لكن لو الـ IDS عنده:

```text
100 Critical Alerts
```

ممكن نعمل:

```text
Critical IDS Alert
        ↓
Incident Ticket
```

بينما الـ Medium/Low:

```text
IDS
 ↓
SIEM
 ↓
Correlation / Triage
```

وده مثال على **Tactical Design**.

---

# الربط بالسلايدات السابقة

إحنا عندنا دلوقتي نوعين من الـ Flow.

## Flow 1 — Normal Event

```text
Endpoint / Network
        ↓
       Event
        ↓
       Log
        ↓
       SIEM
        ↓
Parsing / Enrichment
        ↓
Analytics Rule
        ↓
     Interesting
        ↓
       ALERT
        ↓
      Triage
        ↓
     Incident
```

---

## Flow 2 — Security Tool Already Detected It

```text
Network Traffic
        ↓
       IDS
        ↓
   Detection Rule
        ↓
   Alert Generated
        ↓
     Alert Log
        ↓
       SIEM
        ↓
   Triage / Correlation
        ↓
     Incident?
```

ودي أهم إضافة في السلايد ده.

---

# الخلاصة

ثبتي الأربع أفكار دول:

### 1. الـ Log مجرد Representation

**Log** = السجل اللي بيمثل البيانات.

وممكن يمثل:

* Event
* Alert

---

### 2. مش كل Log = Event

ممكن Security Appliance يطلع **Alert Log**.

---

### 3. الـ Alert Log معناه إن Detection حصل بالفعل

مثلاً:

```text
IDS
 ↓
Signature Match
 ↓
Alert
```

فالـ SIEM يستقبل **Alert جاهز** بدل ما يبدأ من Event خام.

---

### 4. الـ SOC لازم يقرر هيتعامل مع الـ Alerts إزاي

ممكن:

```text
IDS → Analyst → SIEM
```

أو:

```text
IDS → SIEM → Analyst
```

أو:

```text
IDS → Critical Alert → Ticket
```

أو حتى تستخدم **أكتر من طريقة حسب الـ Severity / Confidence**.

وأهم Mental Model هنا:

> **Some logs describe things that happened (Events), while other logs describe detections made by security tools (Alerts). Both can go to the SIEM, but they shouldn't necessarily be treated the same way.**
