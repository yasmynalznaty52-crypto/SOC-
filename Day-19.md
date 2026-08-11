# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Alert Triage

دي الخطوة اللي بعد الـ Alert Collection مباشرة.

مرحلة الـ **Triage** هي المرحلة اللي بنبدأ فيها نحدد:

> أي Alert محتاج اهتمام الأول؟ وهل هو فعلاً يستحق الـ Investigation؟

---

# 1. Generated Alerts Go to a Triage Interface

الكتاب بيقول:

> `Generated alerts go to one (or multiple) interfaces for triage`

يعني بعد ما الـ Alert يتولد لازم يروح لمكان الـ Analyst يقدر يشوفه ويتعامل معاه، زي:

* `SIEM Console`
* `Security Monitoring Platform`
* `SOC Dashboard`
* `Security Onion Console`
* `Ticketing System`

المسار:

```text
IPs → Alerts → SIEM → Triage Queue → SOC Analyst
```

الـ Analyst مش مفروض يفضل يدور يدويًا وسط كل الـ Logs علشان يسرع من الوصول، وعشان كده واحد من الـ Interfaces بيعرض له الـ Alerts المهمة.

---

# 2. What is a Triage Queue?

لو أنا عندي عدد كبير من الـ Alerts في اليوم، والـ Alerts دي بيتعامل معاها مجموعة من الـ Analysts، فمحتاجين **Queue** تسهل عملية التعامل معاها.

الـ Analyst بيقدر يشوف منها:

* الـ Alerts الموجودة.
* إيه الـ Alert الأهم.
* مصدر الـ Alert.
* الـ Alert حصل كام مرة.
* الـ Severity.
* المعلومات المرتبطة بالـ Alert.

وبالتالي الـ Queue بتساعد الـ Analyst يعرف يبدأ بإيه.

---

# 3. إيه المعلومات اللي بنعرضها في الـ Triage Queue؟

الكتاب بيقول:

> `A list of all recently fired alerts`

يعني الـ Triage Queue بتعرض قائمة بكل الـ Alerts اللي تم إطلاقها مؤخرًا.

لكن مش مجرد أسماء، هي بتعرض معلومات تساعد الـ Analyst ياخد قرار.

الكتاب بيقول:

> `How many times each alert fired`

يعني عدد المرات اللي الـ Alert اتكرر فيها.

وده مهم جدًا لأن الـ Frequency جزء مهم من الـ Context.

مثلاً لو Alert حصل آلاف المرات، ممكن يكون السبب:

* `Misconfiguration`
* `Detection Rule` واسعة جدًا
* `Compromised System`
* `Automated Scanning`
* `False Positive`

---

# 4. Source of the Alert

الـ Queue ممكن توضح الـ Alert جاي منين.

وده مهم لأن الـ Analyst محتاج يعرف مين اللي اكتشف المشكلة.

مثلاً:

```text
EDR
Firewall
IDS
IPS
Authentication System
Cloud Security Tool
```

فمصدر الـ Alert جزء مهم من الـ Context.

---

# 5. Assessed Severity

كل Alert كمان بيكون ليه Severity.

زي مثلاً:

```text
Low
Medium
High
Critical
```

وطبعًا:

> **الأعلى Severity مش بالضرورة معناه إن الـ Alert ده Incident.**

الـ Severity بتساعد في **Prioritization**، لكنها مش العامل الوحيد في تحديد الأولوية.

---

# Keys to Triage Success

الكتاب بيقول:

> **Keys to triage success: Prioritization, Context, and Speed**

يعني نجاح الـ Alert Triage بيعتمد على 3 حاجات أساسية:

1. **Prioritization**
2. **Context**
3. **Speed**

ودي لازم تكون واضحة جدًا.

---

## 1. Prioritization

يعني:

> أبدأ بأنهي Alert؟

ممكن يكون عدد الـ Alerts كبير ومختلف في الأهمية داخل الـ Triage Queue، فلازم نتأكد إن الـ Analyst بيعرف:

> `What should I work on first?`

---

## 2. Context

دي من أهم الحاجات في الـ SOC.

الـ Analyst مثلاً ممكن يشوف:

```text
Suspicious Connection
```

لكن محتاج Context علشان يقدر يحكم على الـ Alert.

مثلاً:

```text
Source IP
Destination IP
Username
Hostname
Process
Timestamp
```

لأن الـ Alert من غير Context بيكون صعب جدًا تقييمه.

---

## 3. Speed

السرعة مهمة لأن الـ Attacks ممكن تكون شغالة بالفعل في الوقت اللي حصل فيه الـ Alert أو في الوقت اللي الـ Analyst شاف فيه الـ Alert.

لكن السرعة مش معناها إننا نرمي أي Alert على الـ Analyst بدون معلومات.

المطلوب هو:

> **Fast and informed triage.**

يعني سرعة مع وجود Context كافي لاتخاذ قرار صحيح.

---

# Single Queue vs Multiple Queues

الكتاب بيقول:

> `Some SOC choose to centralize all alerts into a single queue, others will decide to have multiple queues that must be worked independently`

فيه طريقتين أساسيتين:

## 1. Single Queue

كل الـ Alerts تدخل في Queue واحدة، وكل حاجة تكون في مكان واحد، والـ Analyst عنده **Single View** للـ Alerts.

```text
All Alerts
    ↓
Single Queue
    ↓
SOC Analysts
```

---

## 2. Multiple Queues

بنقسم الـ Alerts على أكتر من Queue حسب:

* الـ Severity
* الـ Team
* الـ Technology
* نوع الـ Security Tool
* المسؤولية

مثلاً:

```text
Network Alerts
      ↓
Network Security Team
```

```text
Endpoint Alerts
      ↓
Endpoint Security Team
```

```text
Cloud Alerts
      ↓
Cloud Security Team
```

---

# ليه نستخدم Multiple Queues؟

لو المؤسسة كبيرة، ممكن يكون عندها تخصصات مختلفة.

مثلاً:

```text
Network Security Team
```

مسؤولة عن Network Alerts.

و:

```text
Endpoint Security Team
```

مسؤولة عن EDR Alerts.

و:

```text
Cloud Security Team
```

مسؤولة عن Cloud Alerts.

فمش شرط كل الـ Alerts تروح لنفس المكان.

---

# Single Queue مش معناها إن Analyst واحد يعالج كل حاجة

دي نقطة مهمة.

ممكن يكون عندك:

```text
ONE CENTRAL QUEUE
        ↓
Multiple Analysts
```

يعني الـ Queue واحدة، لكن الـ Analysts كتير.

---

# مثال كامل

عندك SOC يستقبل:

```text
10:01 → EDR Alert
10:02 → Firewall Alert
10:03 → IDS Alert
10:04 → Cloud Alert
10:05 → Authentication Alert
```

كلهم يدخلوا:

```text
Triage Queue
```

والـ Queue ترتبهم مثلًا:

```text
1. Critical Malware Detection
2. High C2 Communication
3. High Account Compromise
4. Medium Suspicious Login
5. Low Policy Violation
```

الـ Analyst يبدأ:

```text
#1 Critical
```

وبعدين:

```text
#2 High
```

وهكذا.

وده هو معنى:

> **Prioritization**

---

# اربطي السلايد ده بالـ Alert Collection

السلايد اللي فات كان:

```text
Security Tool
     ↓
Alert Log
     ↓
SIEM
```

دلوقتي:

```text
Security Tool
     ↓
Alert
     ↓
SIEM / Security Platform
     ↓
Triage Queue
     ↓
SOC Analyst
```

فالـ **Triage Queue** هي المرحلة اللي بتوصل بين:

**Automated Detection**

و

**Human Investigation**

---

# الفرق بين Detection و Triage

مهم جدًا متخلطيش بينهم.

## Detection

الـ Tool أو الـ SIEM يقول:

> **"في حاجة suspicious."**

وينتج:

**Alert**

```text
Detection
   ↓
"Something looks suspicious"
```

---

## Triage

الـ Analyst يقول:

> **"خليني أفهم الـ Alert ده وأحدد أهميته وأقرر هل محتاج Investigation أعمق."**

يعني:

```text
Triage
   ↓
"How important is this, and what should I do next?"
```

---

# الخلاصة

السلايد ده عايزك تفهمي إن الـ Alerts بعد ما تتولد **لازم يكون لها مكان واضح للـ Triage**.

والـ Triage الجيد يعتمد على 3 حاجات:

```text
Prioritization
     +
Context
     +
Speed
```

### Prioritization

نعرف **إيه اللي نشتغل عليه الأول**.

### Context

نعرف **إيه اللي حصل وحواليه معلومات إيه**.

### Speed

نتعامل مع الـ Alert **في الوقت المناسب** قبل ما الـ Attacker يوسع نشاطه.

والـ SOC ممكن يستخدم:

```text
Single Queue
```

أو:

```text
Multiple Queues
```

حسب تصميم المؤسسة وطريقة توزيع المسؤوليات.

وأهم Flow لحد هنا:

```text
EVENT
  ↓
LOG
  ↓
SIEM / SECURITY TOOL
  ↓
DETECTION
  ↓
ALERT
  ↓
TRIAGE QUEUE
  ↓
PRIORITIZATION + CONTEXT + SPEED
  ↓
SOC ANALYST
  ↓
INVESTIGATION
  ↓
INCIDENT MANAGEMENT
```

ده كده بيكمّل الصورة اللي بنبنيها من أول **Event Collection** لحد **SOC Triage**.

---

# Successful Triage

الـ Flow الأساسي:

```text
Alerts from all sources
        ↓
Triage Queue
        ↓
Investigation
```

## 1. Input: Alerts from all sources

الـ Alerts بتيجي بسبب الـ Detection Systems، واللي ممكن تيجي من مصادر مختلفة.

مثلاً:

```text
IDS
IPS
EDR
Firewall
SIEM
Authentication Systems
Cloud Security Tools
```

---

## 2. Output: Ranked Alerts

الـ Output أو المطلوب من الـ Triage هو:

> **Ranked Alerts**

يعني الـ Alerts بتكون مترتبة حسب الأولوية.

والهدف إن الـ Analyst يعرف يقرر أنهي Alert يبدأ بيه.

---

# Ranked Alerts

يعني الـ Alerts بتكون متترتبة حسب الأولوية.

والهدف إن الـ Analyst يعرف يقرر أنهي Alert يبدأ بيه.

### هل الـ Highest Severity دايمًا هو الأول؟

الإجابة:

**لا.**

لأن الـ Triage مش مجرد Severity فقط، لكن الـ Analyst لازم يبص على الـ Context كامل.

ممكن Alert يكون مكتوب عليه:

```text
High
```

و Alert تاني:

```text
Medium
```

لكن الـ Medium يكون أخطر في الظروف الحالية.

وده لأن الأولوية بتعتمد على حاجات زي:

* مدى تقدم الـ Attack.
* أهمية الـ System.
* أهمية الـ User.
* مستوى الـ Privilege.
* نوع الـ Attack.
* الـ Target.
* هل النشاط غريب أو غير معتاد؟
* هل الـ Attack يبدو Targeted؟

---

# 3. How Far Has the Attack Progressed?

دي نقطة مهمة، وهي إن الـ Analyst بيسأل:

> الـ Attacker وصل لفين؟

### Scenario 1

```text
Initial Access Attempt
        ↓
Block
```

مثلاً:

حاول يدخل لكنه اتمنع.

---

### Scenario 2

```text
Successful Initial Access
        ↓
Execution
        ↓
Credential Access
        ↓
Lateral Movement
```

هنا الـ Attack متقدم جدًا وغالبًا له أولوية أعلى.

---

# 4. Criticality of the System

هنا الـ Analyst لازم يفهم ويسأل:

> الجهاز اللي اتهجم مهم أقد إيه؟

لأن الأجهزة بتختلف في الأهمية.

مثلاً:

```text
Normal Laptop
      ≠
Domain Controller
```

فـ Alert على جهاز عادي ممكن يكون أقل أولوية من Alert على **Domain Controller**.

---

# 5. Privilege of the Account

مين الـ User اللي ممكن يكون Compromised؟

مثلاً:

```text
Normal User
    ≠
Administrator
    ≠
Domain Administrator
```

فده ممكن يكون ليه Priority عالية جدًا.

لأن لو الحساب اتخترق، الـ Attacker ممكن يمتلك صلاحيات كبيرة جدًا.

---

# 6. Priority Assets, Accounts, or Data

يعني لازم نعرف إيه أهم حاجة في الـ Environment.

لو الـ Alert متعلق بواحد من التلاتة دول:

```text
Priority Assets
Priority Accounts
Priority Data
```

فغالبًا هيكون ليه Priority أعلى.

---

# 7. Unique or Targeted Attacks

الكتاب بيقول:

> `Whether it appears to be a unique or targeted attack or generic/common activity`

يعني مثلاً لو Alert اتكرر 10,000 مرة ومعروف إنه False Positive، ممكن ما نبصش عليه زي حاجة اشتبهنا إنها أول مرة تحصل، وفي مكان مش معتاد، أو نشاط مبتكر ومحدد لهدف معين.

فده ممكن يكون **Targeted Attack** ويحتاج Priority أعلى.

---

# 8. Management of Queue Size

الـ Analyst ممكن يكون عنده مثلاً:

```text
100 Alerts
```

وبعدين:

```text
500 Alerts
```

ومش قادر يخلص الـ Alerts بالسرعة المطلوبة.

فده خطر لأنه ممكن يكون فيه Alert مهمة مدفونة وسط كمية ضخمة من الـ Alerts.

زي ما الكتاب بيقول، الـ Triage الناجح له هدفين:

1. **Easy identification of the most important alerts**
2. **Management of queue size**

---

# إزاي الـ Analyst يعرف الأولوية؟

هنا بقى بنحتاج **Knowledge**.

الكتاب بيقول إن الـ Effective Analysts بيستخدموا معرفتهم بـ:

# Attack Progression

يعرف الـ Attack عادةً بيتطور إزاي.

مثلاً:

```text
Initial Access
      ↓
Execution
      ↓
Persistence
      ↓
Privilege Escalation
      ↓
Credential Access
      ↓
Lateral Movement
      ↓
Collection
      ↓
Exfiltration
```

لو شفتي Alert يشير إن الـ Attacker وصل لمرحلة متقدمة، ده ممكن يرفع الـ Priority.

---

# Attacker Maneuvering

الـ Analyst لازم يكون فاهم:

> **لو Attacker دخل البيئة، غالبًا هيحاول يعمل إيه بعد كده؟**

مثلاً:

```text
Compromised Workstation
       ↓
Credential Theft
       ↓
Find Admin Account
       ↓
Lateral Movement
       ↓
Domain Controller
```

فلو عندك Alert يدل على:

```text
Credential Theft
```

ممكن يكون مهم جدًا لأنك عارفة إن الخطوة اللي بعدها ممكن تكون **Lateral Movement**.

---

# TTPs

الـ Analyst كمان يعتمد على معرفته بـ:

> **Tactics, Techniques, and Procedures — TTPs**

يعني طرق وأساليب الـ Attacker.

مثلاً لو شفتي:

```text
PowerShell
+
Encoded Command
+
Suspicious Network Connection
```

المحلل المتمرس هيعرف إن الـ Combination ده ممكن يكون مرتبط بـ Attack Technique معينة.

فالموضوع مش مجرد قراءة:

> "PowerShell was executed."

لكن:

> **إيه الـ Context؟ وإيه الـ TTP اللي ممكن يكون مستخدم؟**

---

# مثال كامل على Successful Triage

تخيلي عندك 3 Alerts:

## Alert #1

```text
Low Severity
User visited blocked website
Normal Employee Laptop
```

---

## Alert #2

```text
High Severity
Suspicious PowerShell
Administrator Account
Production Server
```

---

## Alert #3

```text
Medium Severity
Failed Login
Normal User
```

لو بصينا على الـ Severity فقط:

```text
#2 → High
#3 → Medium
#1 → Low
```

واضح.

لكن السبب الحقيقي إن **#2 لازم تكون الأولى** أقوى من مجرد كلمة High:

```text
Administrator Account
        +
Production Server
        +
Suspicious PowerShell
        ↓
Potentially High Impact
```

فهي مرتبطة بـ:

* Privileged Account
* Critical Asset
* Suspicious Execution

وده يديها Priority عالية جدًا.

---

# مثال أكثر تعقيدًا

دلوقتي عندنا:

## Alert A

```text
Critical
Malware Detected
Employee Laptop
```

## Alert B

```text
Medium
Suspicious Login
Domain Administrator
Domain Controller
```

لو مشينا بالـ Severity فقط:

```text
Critical → Alert A
Medium → Alert B
```

لكن الـ Analyst لازم يفكر.

Alert B ممكن يكون أخطر لأن:

```text
Domain Admin
     ↓
Domain Controller
     ↓
Potential Privileged Compromise
```

إذن ممكن:

```text
Priority #1 → Alert B
Priority #2 → Alert A
```

وده بالضبط معنى:

> **Triage is not just sorting by severity.**

---

# بعد ما نحدد Priority #1؟

السلايد بيقول:

> **Once alerts are prioritized, the top item is chosen for investigation and validation in the next stage.**

يعني بعد ما رتبنا الـ Alerts:

```text
Priority #1
Priority #2
Priority #3
```

نأخذ:

# Priority #1

ونبدأ عليه:

**Investigation + Validation**

يعني نتحقق:

* هل الـ Alert حقيقي؟
* هل فيه Malicious Activity فعلًا؟
* إيه اللي حصل؟
* إيه الـ Scope؟
* وإيه الـ Impact؟

---

# اربطي السلايد ده باللي قبله

السلايد السابق:

```text
Alerts
  ↓
Triage Queue
  ↓
Prioritization
```

السلايد الحالي بيشرح **إزاي ننجح في الـ Prioritization**.

فتبقى الصورة:

```text
                ALERTS
                  ↓
          TRIAGE QUEUE(S)
                  ↓
        ┌─────────────────┐
        │   PRIORITIZE    │
        │                 │
        │ Attack Progress │
        │ Asset Criticality│
        │ Account Privilege│
        │ Data Sensitivity │
        │ Targeted Attack  │
        │ TTPs             │
        └────────┬────────┘
                 ↓
          RANKED ALERTS
                 ↓
          PRIORITY #1
                 ↓
       INVESTIGATION & VALIDATION
```

---

# أهم حاجة تحفظيها

**Successful Triage = مش إنك تحلي كل الـ Alerts.**

لكن إنك:

> **تحددي بسرعة وبشكل صحيح أي Alert يمثل أكبر خطر في الوقت الحالي، وتبدأي التحقيق فيه أولًا.**

والـ Priority بيتأثر بـ:

```text
Attack Progress
+
Asset Criticality
+
Account Privilege
+
Data Importance
+
Targeted/Unique Activity
+
Attacker TTPs
```

والـ Goal النهائي:

```text
Alerts
  ↓
Rank
  ↓
Most Important Alert
  ↓
Investigate
```

يعني من الآخر:

> **Detection tells you "something may be wrong."**
>
> **Triage tells you "what should I care about first?"**

ودي نقطة أساسية جدًا في شغل الـ SOC Analyst.
