<div align="center">

# بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيمِ

# Day 17

</div>

---

# Events, Alerts, Anomalies, and Incidents

في هذا الجزء هنتعرف على الفرق بين:

* **Events**
* **Alerts**
* **Incidents**
* **Event Collection**
* **Alert Collection**
* ودور الـ **SOC Analyst** في الـ **Triage**

---

# 1. Events

> **Event = Any observable occurrence in a system or network**

يعني الـ **Event** هو أي حاجة قابلة للملاحظة حصلت على الـ **System** أو الـ **Network**.

ودي أوسع وأعم فئة.

### أمثلة:

```text
User → Login → Success
```

ده **Event**.

```text
PowerShell.exe → Run
```

ده برضه **Event**.

الفكرة ببساطة إن حاجة حصلت ونقدر نلاحظها ونسجلها في الـ Logs.

---

# 2. Alert

> **Alert = An event of interest that may be unwanted or unauthorized**

هنا بنبدأ نعمل **Filtering** للـ Events.

عندي عدد ضخم جدًا من الـ Events، وبعضها ممكن يكون مشبوه أو يستحق الانتباه، وبالتالي الـ **Detection Tool** ممكن يعتبر Event معين **Alert**.

لكن مهم جدًا:

> **Alert ≠ Incident**

ومش كل Alert معناه إن فيه Attack حصل فعلًا.

الـ Alert ممكن يكون:

* **True Positive**
* **False Positive**

يعني وجود Alert معناه إن فيه حاجة تستحق التحقيق، لكن لسه مش متأكدين إنها فعلًا Attack.

---

# 3. Incident

> **Incident = A violation or imminent threat of violation of computer security policies, acceptable use policies, or standard security practices**

بمعنى أبسط:

الـ **Incident** بيكون لما نتأكد إن اللي حصل يمثل **انتهاك أو تهديد للـ Security**.

---

# العلاقة بين Event → Alert → Incident

تخيلي إن عندنا جهاز حصل عليه الآتي:

### 1. Event

```text
PowerShell.exe
      ↓
   Started
```

ده **Event**.

لكن مجرد إن PowerShell اشتغل **مش معناه إنه Attack**.

---

### 2. Alert

الـ **EDR** اكتشف إن PowerShell شغّل Command غريب أو اتصل بـ **Suspicious IP**.

```text
PowerShell
    ↓
Suspicious Command / IP
    ↓
   ALERT
```

هنا بقى عندنا **Alert**.

لكن لسه ما نقدرش نقول إن ده **Incident**.

---

### 3. Analyst Triage

هنا يبدأ دور الـ **SOC Analyst**.

الـ Analyst يبدأ يحقق ويسأل:

* مين المستخدم؟
* إيه الـ Process؟
* إيه الـ PowerShell Command؟
* اتصل بأنهي IP؟
* هل الـ IP Malicious؟
* هل فيه Persistence؟
* هل فيه أجهزة تانية اتأثرت؟

---

### 4. Confirmed Incident

لو التحقيق أثبت إن اللي حصل **Malware أو Attack أو Security Violation**:

```text
Event
   ↓
Detection / Analysis
   ↓
Alert
   ↓
Analyst Triage
   ↓
Confirmed Incident
```

وهنا يبدأ التعامل مع الـ Incident من خلال:

> **Incident Management System**

---

# لماذا نحتاج إلى Filtering؟

لأن الـ **Events** ممكن تكون بالملايين.

ومستحيل إن الـ SOC Analyst يراجع كل Event بنفسه.

لذلك بنحتاج:

```text
Security Tools
      ↓
   Detection
      ↓
    Alerts
      ↓
 SOC Analyst
      ↓
    Triage
      ↓
   Incident
```

---

# Alert ≠ Incident

مهم جدًا نفتكر:

```text
Something Happened
       ↓
     EVENT
       ↓
 Detection / Processing
       ↓
     ALERT
       ↓
 Confirmation
       ↓
   INCIDENT
```

فالـ Alert لسه محتاج **Investigation و Confirmation**.

---

# SIEM ودوره في الـ Events والـ Alerts

الـ **SIEM** غالبًا بيجمع الـ Events والـ Logs، وبيعمل عليها **Processing و Detection Rules**، والنتيجة ممكن تكون Alerts.

لكن الـ SIEM مش هو اللي بيقرر بالضرورة إن الحاجة دي **Incident**.

الصورة الأبسط:

```text
Logs / Events
      ↓
     SIEM
      ↓
Parsing
      ↓
Detection Rules
      ↓
   ALERT
      ↓
SOC Analyst
      ↓
   TRIAGE
      ↓
 INCIDENT
```

الـ Analyst هو اللي بيعمل **Triage والتحقيق** ويحدد إذا كان الموضوع فعلًا Incident أم لا.

> **Note:** Your security tools may not use the terminology in the same way.

يعني ما نفترضش إن كل الـ Tools بتستخدم نفس المعاني بالضبط لكلمات:

* Event
* Alert
* Incident

لذلك لما تستخدم أداة معينة، لازم تفهم هي بتستخدم المصطلحات دي إزاي.

---

# Event Collection

> **Most logs are records of event as transaction data**

أغلب الـ Logs اللي بنجمعها من البيئة بتكون عبارة عن **Records** بتسجل إن حاجة حصلت.

لكن تسجيل إن حاجة حصلت **مش معناه بالضرورة إنها Malicious**.

---

# 🧠 يعني إيه Event؟

إحنا قلنا:

> **Event = Any observable occurrence in a system or network**

يعني أي حاجة نقدر نلاحظها ونطلع عنها Log تعتبر Event.

مثلاً:

```text
User logged in
```

ده Event.

```text
User visited a website
```

ده Event.

```text
DNS query happened
```

ده Event.

```text
Network connection happened
```

ده Event.

---

# Windows Sysmon Network Connection

عندنا Log من **Windows Sysmon**:

```text
UtcTime: 2018-09-23 16:16:16.054
ProcessId: 8012
Image: C:\Users\user1\AppData\Local\slack\app
3.3.1\slack.exe

User: win10\user1
Protocol: tcp

SourceIp: 10.150.159.161
SourcePort: 60201

DestinationIp: 52.85.81.133
DestinationPort: 443
DestinationPortName: https
```

الـ Log ده بيقول لنا إن حصل **Network Connection**.

خلينا نفكّه:

### وقت الحدث

```text
UtcTime: 2018-09-23 16:16:16.054
```

يعني الاتصال حصل في الوقت ده.

### الـ Process

```text
ProcessId: 8012
```

ده الـ **Process ID** الخاص بالبرنامج اللي عمل الاتصال.

### البرنامج

```text
Image:
C:\Users\user1\AppData\Local\slack\app
3.3.1\slack.exe
```

البرنامج اللي عمل الـ Connection هو:

**slack.exe**

### المستخدم

```text
User: win10\user1
```

الاتصال حصل من خلال User اسمه:

**user1**

### الـ Protocol

```text
Protocol: tcp
```

الاتصال استخدم:

**TCP**

### Source

```text
SourceIp: 10.150.159.161
SourcePort: 60201
```

يعني الجهاز الداخلي:

```text
10.150.159.161:60201
```

هو اللي بدأ الاتصال.

### Destination

```text
DestinationIp: 52.85.81.133
DestinationPort: 443
DestinationPortName: https
```

الجهاز اتصل بـ:

```text
52.85.81.133:443
```

باستخدام **HTTPS**.

---

# هل ده Attack؟

**مش بالضرورة.**

وده جوهر الفكرة.

الـ Log بيقول:

> Slack.exe عمل HTTPS connection إلى 52.85.81.133.

هل Slack المفروض يتصل بالإنترنت؟

**آه، طبيعي جدًا.**

إذن حاليًا:

```text
Network Connection
       ↓
      EVENT
```

وليس:

```text
Network Connection
       ↓
    INCIDENT
```

ولا حتى بالضرورة:

```text
Network Connection
       ↓
     ALERT
```

هو مجرد **Event**.

---

# Squid Proxy

السلايد فيه:

```text
1335543155 315 127.0.0.1 TCP_MISS/301 -1
GET http://www.imdb.com/title/tt0056869
```

ده Log من **Squid Proxy**.

بيوضح إن فيه User/Client عمل:

```text
GET Request
     ↓
imdb.com/title/tt0056869
```

يعني حد زار URL معين.

هل زيارة IMDb تعتبر Attack؟

غالبًا:

**لا.**

إذن:

```text
Website Visit
      ↓
     EVENT
```

الـ Proxy سجل إن حاجة حصلت، وخلاص.

---

# Apache Web Server

عندنا:

```text
117.201.11.139
-- [02/Jan/2017:02:35:54 -0800]
"GET / HTTP/1.1"
200 34374
```

ده **Apache Access Log**.

يعني الـ IP:

```text
117.201.11.139
```

عمل HTTP GET Request للـ Web Server.

والـ Server رد:

```text
200
```

يعني الـ Request نجح.

مرة تانية:

> حصل Request.

ده **Event**.

مش معناها تلقائيًا إنه Attack.

---

# BIND DNS

عندنا:

```text
Feb 27 15:12:28
srv named[8978]:
client 1.1.1.2#38595:
query: allegro.pl IN A +E
```

ده Log من **BIND DNS Server**.

اللي حصل:

```text
Client
  ↓
DNS Query
  ↓
allegro.pl
```

يعني جهاز عمل DNS Query عشان يعرف الـ IP الخاص بالـ Domain.

مرة أخرى:

**Event.**

---

# Linux Authentication

السطر:

```text
Sep 23 08:54:56 ubuntu CRON[16355]:
pam_unix(cron:session):
session opened for user root by
(uid=0)
```

ده بيسجل إن:

```text
Session
   ↓
opened
   ↓
user root
```

وده **Observable Occurrence** حصل على النظام.

إذن:

**Event.**

لكن هل User root عمل حاجة Malicious؟

الـ Log ده لوحده **مش بيقولنا كده**.

---

# ما المشترك بين كل الأمثلة؟

السلايد جاب Logs من مصادر مختلفة:

```text
Squid Proxy
Apache
BIND DNS
Linux Authentication
Windows Sysmon
```

لكن كلهم في النهاية بيسجلوا:

> **Someone/something did something.**

يعني:

```text
User → Login

User → Website

Client → DNS Query

Server → HTTP Request

Process → Network Connection

Cron → Session
```

كل دي **Events**.

---

# متى يصبح الـ Event Interesting؟

الـ Event في حد ذاته ممكن يكون طبيعي جدًا.

لكن ممكن يبقى Interesting لما نبدأ نعمل عليه **Processing و Analysis** ونربطه بأحداث أخرى.

مثلاً:

```text
03:00 AM
    ↓
Login
    ↓
Unusual Country
    ↓
New Device
    ↓
Multiple Failed Logins
    ↓
Successful Login
    ↓
Admin Privileges Used
```

كل Event لوحده ممكن ما يكونش كافي.

لكن لما نجمع الأحداث ونربطها ببعض، الصورة ممكن تبقى Suspicious.

وهنا بيظهر دور الـ **SIEM**.

---

# ماذا يفعل الـ SIEM؟

الـ SIEM ممكن يساعدنا في:

### 1. Parse Events

يعني يسحب الـ Logs ويفهمها ويقسمها إلى **Fields**.

### 2. Apply Threat Intelligence

يقدر يستخدم معلومات من الـ **Threat Intelligence** للمساعدة في تحديد النشاط المشبوه.

### 3. Correlate with Other Logs

ودي من أهم الحاجات.

Event واحد ممكن ما يبانش خطير، لكن لما نربطه بأحداث تانية، القيمة بتبان.

### 4. Match Against Known Malicious Indicators

الـ SIEM ممكن يقارن الـ Events بقوائم فيها:

* Malicious IPs
* Malicious Domains
* Indicators of Compromise (IOCs)

---

# متى يتحول الـ Event إلى Alert؟

لما الـ SIEM يعمل للـ Event:

* Parsing
* Threat Intelligence Matching
* Correlation
* Detection Rules

ويكتشف إن فيه حاجة **Suspicious**، ممكن يعمل:

```text
EVENT
  ↓
Analysis / Processing
  ↓
Suspicious Information
  ↓
ALERT
```

وبعد الـ Alert، لو التحقيق أثبت وجود **Compromise**:

```text
ALERT
  ↓
Investigation / Triage
  ↓
Confirmed Compromise
  ↓
INCIDENT
```

---

<div align="center">

## End of Part 1

</div>
