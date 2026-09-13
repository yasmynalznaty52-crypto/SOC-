# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 39 — Threat Intelligence Platforms and You

الفكرة الأساسية إنه عندي في CTI عندي طرفين:

**Producers** = دول اللي بيعملوا الـ Intelligence

**Consumers** = دول اللي بيستخدموا الـ Intelligence

وفي أغلب الـ SOCs بكون أنا كـ **SOC Analyst** عبارة عن **Consumer** للـ Threat Intelligence.

---

## 1️⃣ Threat Intelligence Producers & Consumers

🔹 **Producer:**

هو الـ **Threat Intelligence Producer**، وهو الشخص أو الـ team اللي بيجمع الـ data ويعمل عليها analysis.

يعني مثلًا **Threat Intelligence Team** تلاقي:

```text
IP: 185.x.x.x
Domain: evil-domain.com
Hash: abc123...
```

دي في البداية مجرد **Threat Data / Observables**.

الفريق يبدأ يحلل:

* الـ IP ده تابع لمين؟
* ظهر فين؟
* مرتبط بأنهي malware؟
* بيستخدم كـ C2؟
* مرتبط بأنهي Threat Actor؟
* بيستهدف مين؟
* إيه الـ TTPs المستخدمة؟
* First Seen / Last Seen؟
* هل هو relevant للـ organization؟

وفي النهاية يطلع **Intelligence مفيدة**.

---

## 2️⃣ مين هو الـ Threat Intelligence Group؟

الـ SEC450 بيقول:

> Many SOCs contain a threat intelligence group

يعني بعض الـ **SOCs الكبيرة** بيكون فيها **Threat Intelligence Team / Group** مخصص.

مثلًا:

```text
SOC
│
├── SOC Analysts
│      └── Alert Triage / Investigation
│
├── Threat Intelligence Team
│      └── Produces CTI
│
└── Incident Response
       └── Handles incidents
```

الـ Threat Intelligence team ممكن يكون مسؤول عن:

* جمع threat data
* تحليل Threat Actors
* تحليل campaigns
* تحليل malware
* تحليل TTPs
* Enrichment
* إنتاج Intelligence
* مشاركة الـ Intelligence مع الـ SOC

---

## 3️⃣ طب أنا كـ SOC Analyst بعمل إيه؟

الجزء ده مهم طبعًا لأنه بيقول إن أنا كـ **SOC Analyst** أعتبر **Consumer**.

يعني مش مطلوب مني كل مرة أبدأ من الصفر وأعمل Intelligence كاملة.

بدل كده، عندي Alert:

```text
SIEM
 ↓
Suspicious connection
 ↓
Source IP: 185.x.x.x
```

فسأل:

**هل الـ IP ده معروف malicious؟**

هنا هستخدم **Threat Intelligence**.

مثلًا:

```text
IP → Threat Intelligence Platform
             ↓
       Known C2 infrastructure
       Associated malware: X
       First seen: June 2026
       Confidence: High
```

المعلومة دي تساعدني في التحقيق بعدين.

---

# 4️⃣ إيه الشغل اليومي اللي بيحتاج Threat Intelligence؟

الكتاب ذكر 3 أمثلة مهمة جدًا:

### 🔹 Validating Alerts

يعني عندي Alert وعايزة أعرف ده إيه بالظبط:

**False Positive ولا True Positive؟**

مثال:

```text
Alert:
Internal host → 185.x.x.x
```

هبحث عن الـ IP في **Threat Intelligence**.

لو:

```text
185.x.x.x
Known C2
Associated with malware X
```

ده يرفع الـ **confidence** إن الـ alert suspicious.

لكن مهم:

```text
Known malicious IOC ≠ automatically confirmed incident
```

لسه محتاجة **Context وتحقيق**.

---

### 🔹 Looking for Threats

يعني بدل ما أستنى الـ SIEM يطلع Alert، ممكن أعمل **Threat Hunting**.

مثلًا عندي Domain معروف مرتبط بـ malware:

```text
evil-domain.com
```

هروح أدور في الـ logs:

```text
Has any internal host contacted evil-domain.com?
```

فهلاقي:

```text
PC-102 → evil-domain.com
```

وهنا هبدأ أعمل **investigation**.

---

### 🔹 Investigating Incidents

لو عندي Incident بالفعل، **Threat Intelligence** تساعدني أفهم:

```text
Who?
What?
How?
Why?
```

مثلًا:

```text
Phishing Email
      ↓
Malicious Attachment
      ↓
PowerShell
      ↓
Credential Dumping
      ↓
C2
```

Threat Intelligence ممكن تساعدني أربط الـ activity دي بـ:

* Malware
* Threat Actor
* Campaign
* TTPs
* Infrastructure
* Other IOCs

وبالتالي أوسع نطاق التحقيق.

---

# 5️⃣ طيب إيه هو Threat Intelligence Platform (TIP)؟

الـ **TIP = Threat Intelligence Platform**

نقدر نعتبره:

**Knowledgebase + Automation layer للـ Threat Intelligence**

يعني مكان بخزن/أدير فيه:

```text
Threat Data
+
Threat Information
+
Threat Intelligence
+
Context
+
Relationships
```

مثال مبسط:

```text
IOC: evil.com
       │
       ├── Malware: Trojan.X
       ├── Campaign: Campaign-A
       ├── Threat Actor: Group-X
       ├── TTP: T1566
       ├── First Seen
       └── Description / Context
```

وده قريب جدًا من اللي كنا بنتكلم عنه في الصفحة اللي فاتت:

```text
IOC = Observable + Context
```

الـ TIP المفروض مايبقاش مجرد:

```text
evil.com
1.2.3.4
abc123hash
```

وخلاص.

لا، المفروض يحافظ على **السياق والعلاقات بينهم**.

---

# 6️⃣ الـ TIP بيعمل Automation إزاي؟

الكتاب بيقول:

> Automates exchange and querying of data from other security tools

يعني الـ TIP ممكن يتكامل مع أدوات تانية.

مثلًا:

```text
SIEM
  ↕
TIP
  ↕
EDR
  ↕
Firewall
  ↕
IDS
```

مثال عملي:

الـ SIEM شاف:

```text
Connection → 1.2.3.4
```

ممكن يعمل Query للـ TIP:

```text
Is 1.2.3.4 malicious?
```

والـ TIP يرجع:

```text
Malicious
Confidence: High
Type: C2
Associated Malware: X
```

فأنا كـ Analyst مش مضطرة كل مرة أدور يدويًا في كل مصدر.

---

# 7️⃣ أهم جملة في الصفحة

> Threat Intelligence Platforms do NOT produce intelligence for you!

دي مهمة جدًا.

يعني:

```text
TIP ≠ Intelligence Analyst
```

الـ TIP ممكن:

* يجمع Data
* يخزن Data
* يربط Data
* يعمل Enrichment
* يعمل Queries
* يعمل Automation
* يتكامل مع Security Tools

لكن مش هو اللي بيفكر مكان الـ Analyst.

مثال:

الـ TIP يقول:

```text
IP: 1.2.3.4
Malicious: YES
```

لكن أنا اللي لازم أسأل:

* هل الـ IP ده مرتبط بالـ alert اللي عندي؟
* هل الـ connection ده فعلًا malicious؟
* هل الجهاز اتعرض لـ compromise؟
* إيه الـ malware المستخدم؟
* إيه الـ attack technique؟
* إيه الـ impact؟
* أعمل containment ولا لأ؟

دي **Human Analysis + Decision Making**.

---

# 🔗 ربط الصفحة بالصفحة اللي فاتت

إحنا كنا بنقول:

## Bad CTI

```text
1.2.3.4
Known malicious
```

مفيش Context.

## Good CTI

```text
1.2.3.4
   ↓
C2 Server
   ↓
Malware X
   ↓
Campaign Y
   ↓
Threat Actor Z
   ↓
TTP: T1071.001
   ↓
Targeted organizations
   ↓
First/Last Seen
   ↓
Confidence
```

الـ TIP يساعدني أحفظ وأربط النوع ده من المعلومات وأجيبه بسرعة.

لكن الـ **Analyst** هو اللي يحلل ويطلع **assessment** وقرار.

---

# 🎯 الصورة الكاملة

المهم أفهم الـ **workflow** ده لأنه بيربط كذا صفحة ببعض:

```text
Threat Data
    ↓
Threat Information
    ↓
Threat Intelligence Team
    ↓
Analysis + Context + Assessment
    ↓
Cyber Threat Intelligence
    ↓
Threat Intelligence Platform
    ↓
SOC Analyst consumes it
    ↓
Alert Validation / Hunting / Investigation
    ↓
Decision
    ↓
Action
```

## مثال SOC حقيقي

```text
SIEM Alert
   ↓
Internal PC contacted 1.2.3.4
   ↓
SOC Analyst queries TIP
   ↓
TIP says:
C2 infrastructure
Associated with Malware X
High confidence
   ↓
Analyst investigates endpoint
   ↓
Finds PowerShell execution
   ↓
Finds persistence
   ↓
Confirms compromise
   ↓
Contain host
```

هنا الـ **TIP ساعد الـ Analyst**، لكنه ماخدش القرار مكانه.

---

# ⭐ الخلاصة

أهم 5 حاجات من الصفحة:

* **Producer** → بينتج Threat Intelligence.

* **Consumer** → بيستخدم Threat Intelligence، وده غالبًا دور الـ **SOC Analyst**.

* **SOC Analyst** يستخدم CTI في:

  * Alert Validation
  * Threat Hunting
  * Incident Investigation

* **TIP = Knowledgebase + Integration + Automation** للـ Threat Data / Information / Intelligence.

* **TIP لا ينتج Intelligence بدل الـ Analyst**؛ الـ Human Analysis والـ Decision Making لسه أساسيين.

### وأهم distinction:

```text
TIP
↓
يساعدني أجمع وأدير وأسترجع الـ Threat Intelligence

لكن

Analyst
↓
يفهم الـ Context
↓
يعمل Assessment
↓
ياخد Decision
```
