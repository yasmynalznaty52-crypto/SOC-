# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 20 - Alert Log Flow Options

## Alert Log Flow Options Illustrated

أول سؤال هنا هو:

> **الـ Alerts بتتولد فين؟**

عندنا مكانين أساسيين ممكن الـ Alerts تتولد فيهم:

1. **Point Security Products**
2. **SIEM**

---

# 1. Point Security Products

زي:

* `IDS`
* `IPS`
* `EDR`
* `Firewall`
* `Antivirus`
* `WAF`

والـ Analyst ممكن يدخل مثلاً على الـ **EDR** ويعمل **Triage**.

ودي نقطة مهمة جدًا:

> **الـ SIEM مش هو المكان الوحيد اللي ممكن يحصل فيه Triage.**

---

# 2. SIEM

الـ SIEM هو مكان بتتحط فيه الـ Logs، وممكن كمان يعمل:

* `Analytics`
* `Correlation`
* `Detection`
* `Alert Generation`

مثلاً عندي:

```text
Windows Endpoint
      ↓
    Events
      ↓
     SIEM
      ↓
 SIEM Rules
      ↓
    Alerts
```

وده اسمه:

> **SIEM-generated Alert**

لكن لو حصل إن الـ **EDR** أطلق Alert، والـ **IDS** أطلق Alert، والـ **Firewall** أطلق Alert، فهنا بنبدأ نسأل:

> إزاي الـ Alerts دي هتتجمع؟ وفين الـ Analyst هيعمل Triage؟

---

# Option 1 - Separate Security Product Consoles

كل Tool أو Security Product عنده **Alert Console** خاص بيه.

مثلاً الـ Analyst في الـ Morning Shift يعمل:

```text
Check EDR
    ↓
Check IDS
    ↓
Check Firewall
    ↓
Check Email Security
    ↓
Check SIEM
```

في البداية الـ Analyst بيشوف الـ Alerts الصادرة من كل مصدر.

مثلاً شاف Alert من الـ **EDR** ويدخل يلاقي:

```text
Process Tree
Command Line
Parent Process
User
Host
Time
Network Activity
File Hash
```

فيبقى عندي **Context** كويس جدًا.

لكن المشكلة هنا إن الـ Analyst لو عنده Alerts جاية من أكتر من Tool، ممكن يضطر يتنقل بين أكتر من Console:

```text
EDR Alert
    ↓
EDR Console

IDS Alert
    ↓
IDS Console

SIEM Alert
    ↓
SIEM Console
```

وممكن نفس الـ Attack تظهر في أكتر من مكان.

مثلاً نفس الـ Attack ممكن تعمل:

```text
EDR Alert
+
IDS Alert
+
Firewall Alert
+
SIEM Alert
```

فـ الـ Analyst ممكن يضطر يجمع الصورة بنفسه من مصادر مختلفة.

---

# Option 2 - Everything in SIEM

وده من أشهر التصاميم.

كل الـ Security Tools تبعت الـ Alerts بتاعتها للـ SIEM:

```text
EDR ───────┐
IDS ───────┤
Firewall ──┤
Email ─────┤
Windows ───┤
Linux ─────┤
            ↓
           SIEM
            ↓
       Alert Queue
            ↓
         Analyst
```

يعني الـ Analyst ممكن يفتح الـ SIEM ويشوف:

```text
All Alerts
```

مثلاً:

```text
#1 Critical - Malware
#2 High     - Brute Force
#3 High     - C2 Communication
#4 Medium   - Suspicious PowerShell
```

وهنا عندي:

> **Centralized Alert Queue**

يعني الـ Analyst يقدر يفتح الـ SIEM ويشوف كل الـ Alerts في مكان واحد.

وده بيسهل عملية:

* `Triage`
* `Prioritization`
* `Correlation`

لأن كل الـ Alerts موجودة في مكان مركزي.

---

# Logging the Alert into SIEM ≠ Analyst Must Triage in SIEM

دي نقطة مهمة جدًا.

الكتاب بيقول إن الـ Security Products المفروض تسجل الـ Alerts بتاعتها في الـ SIEM، لكن:

> **Logging the alert into SIEM does not mean the analyst must triage in SIEM.**

يعني ممكن:

```text
EDR
 ↓
Alert
 ↓
SIEM
```

الـ SIEM يسجل الـ Alert.

لكن الـ Analyst يفضل يعالج الـ Alert من الـ **EDR نفسه**.

يعني:

> **مكان تخزين الـ Alert مش بالضرورة يكون مكان الـ Triage.**

ودي نقطة مهمة جدًا في تصميم الـ SOC.

---

# Option 3 - Everything in Another Tool

ممكن كمان الـ Alerts تروح لـ **Tool** تانية تكون هي المكان المركزي للتعامل معاها.

من الأمثلة:

* `SOAR`
* `Incident Management Platform`

---

# SOAR

**Security Orchestration, Automation and Response - SOAR**

ممكن الـ SOAR يكون المكان المركزي اللي الـ Analyst بيتعامل منه مع:

* `Alerts`
* `Incidents`
* `Enrichment`
* `Automation`
* `Response Actions`

مثلاً:

```text
EDR ───────┐
IDS ───────┤
SIEM ──────┤
Firewall ──┤
Email ─────┘
      ↓
     SOAR
      ↓
Central Alert Queue
      ↓
   Analyst
```

---

# الفرق بين SIEM و SOAR

## SIEM

الـ SIEM بشكل أساسي بيعمل:

```text
Collect
   ↓
Store
   ↓
Correlate
   ↓
Analyze
   ↓
Detect
   ↓
Alert
```

يعني الـ SIEM بيركز على **جمع وتحليل البيانات واكتشاف النشاط المشبوه وإنتاج الـ Alerts**.

---

## SOAR

الـ SOAR بيركز أكتر على:

```text
Alert
   ↓
Enrichment
   ↓
Automation
   ↓
Investigation Actions
   ↓
Response
```

مثلاً عندي Alert:

```text
User downloaded malicious file
```

الـ SOAR ممكن يعمل تلقائيًا:

```text
Get File Hash
      ↓
Check Threat Intelligence
      ↓
Get User Information
      ↓
Get Endpoint Information
      ↓
Check Reputation
      ↓
Create Incident
      ↓
Notify Analyst
```

وفي بعض البيئات ممكن ينفذ **Response** كمان، حسب الـ **Playbook** والصلاحيات.

---

# السؤال الحقيقي في تصميم Alert Flow

السؤال اللي الكتاب عايزنا نفكر فيه هو:

> **Where do you triage alerts?**

مش:

> **Where are alerts generated?**

ولا:

> **Where are alerts stored?**

لكن:

> **Where does the SOC Analyst actually investigate and triage them?**

ودي من أهم الأفكار في الجزء ده.

---

# مثال واقعي مهم جدًا

خلينا نقول إن عندك Attack:

```text
Attacker
   ↓
Phishing Email
   ↓
User opens attachment
   ↓
PowerShell executes
   ↓
Malware connects to C2
```

ممكن يحصل الآتي:

## Email Security

يطلع:

```text
Malicious Attachment
```

## EDR

يطلع:

```text
Suspicious PowerShell
```

## Network IDS

يطلع:

```text
Possible C2 Traffic
```

## SIEM

يجمع:

```text
Email Event
+
EDR Event
+
Network Event
```

ويعمل Correlation:

```text
User received malicious email
+
Executed PowerShell
+
Connected to suspicious IP
```

فيولد:

```text
Possible Phishing-Based Compromise
```

دلوقتي عندك **4 Alerts مرتبطة بنفس الـ Incident**.

---

# لو بتشتغل بطريقة غير مركزية

```text
Analyst
   ↓
Email Console
   ↓
EDR Console
   ↓
IDS Console
   ↓
SIEM
```

الـ Analyst ممكن يضطر يتنقل بين أكتر من مكان علشان يبني الصورة الكاملة.

---

# لو عندك Centralized Triage

```text
Email ──┐
EDR ────┤
IDS ────┤
SIEM ───┘
    ↓
Central Queue
    ↓
Analyst
```

يبقى الـ Analyst شايف الصورة الأكبر في مكان واحد.

---

# أهم Concept في الجزء ده

الجزء ده **مش بيقول إن فيه اختيار واحد صح دائمًا**.

هو بيقول إنك لازم تصمم الـ **Alert Flow** حسب طريقة الـ **SOC Analysts** في التعامل مع الـ Alerts.

لازم تسأل:

### 1. Where are alerts generated?

مثلاً:

```text
EDR
IDS
SIEM
Firewall
```

### 2. Where are alerts stored?

مثلاً:

```text
SIEM
Database
Security Platform
```

### 3. Where are alerts triaged?

مثلاً:

```text
EDR
SIEM
SOAR
Incident Management Platform
```

هل هنعمل **Centralization** والـ Alerts هتروح Queue واحدة؟

ولا:

```text
EDR Queue
IDS Queue
Firewall Queue
```

وكل واحدة يتم التعامل معاها بشكل منفصل؟

وده مرتبط طبعًا بالـ **Successful Triage** اللي شرحناه.

الـ Slide الحالية بتشرح **الـ Infrastructure اللي الـ Alerts بتتحرك من خلالها قبل وأثناء الـ Triage**.

---

# الصورة الكبيرة

```text
              EVENTS
                 ↓
       Security Monitoring
                 ↓
        ┌────────┴────────┐
        ↓                 ↓
  Point Product          SIEM
  generates alert   generates alert
        │                 │
        └────────┬────────┘
                 ↓
        Alert Collection
                 ↓
          Triage Queue
                 ↓
        Prioritize Alerts
                 ↓
            Investigate
                 ↓
              Respond
```

---

# الخلاصة

Alerts can be generated by individual security products such as IDS/EDR, or by the SIEM through analytic rules.

The SOC must decide where analysts will triage these alerts:

```text
Separate Product Consoles
        OR
Centralized SIEM
        OR
Downstream Platform
such as SOAR / Incident Management
```

والأهم:

> **مكان تسجيل الـ Alert مش لازم يكون نفس مكان الـ Triage.**

يعني:

```text
Alert Generated
      ↓
Alert Stored
      ↓
Alert Triaged
```

التلاتة ممكن يحصلوا في نفس الـ Platform، وممكن يحصلوا في Platforms مختلفة.

ودي من أهم النقاط في الـ **Alert Flow Design**.

