# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 41 — TIP Workflow — Part 2

## أولًا: نبص على الـ Workflow

الصفحة عندي:

```text
SIEM
   │
   ↓
Incident Management System
   │
   ↓
Threat Intelligence Platform
   ↑
   │
External Sources

TIP
 │
 ├── Detailed Analysis
 ├── SOAR
 │      ↓
 │   Automated Indicator
 │   Lookup / Submission
 │
 └── Analyst Reports
```

الفكرة الأساسية:

الـ TIP موجود في النص وبيتبادل **Indicators + Threat Information** مع باقي الـ Security Tools، مش شغال لوحده.

---

# 1️⃣ SIEM → TIP

خلينا ناخد Incident حقيقي.

الـ SIEM شاف:

```text
WIN-PC01
      ↓
Connected to
      ↓
156.96.46.116
```

الـ SIEM عنده Alert.

الـ Analyst عايزة تعرف:

**الـ IP ده معروف malicious ولا لأ؟**

هنا يحصل:

```text
SIEM
 ↓
156.96.46.116
 ↓
TIP Lookup
```

والـ TIP ممكن يرجع:

```text
IP: 156[.]96[.]46[.]116
Type: C2
Associated Malware: X
Confidence: High
Context: TA Infrastructure
```

وده يساعد الـ Analyst في الـ Investigation.

---

# 2️⃣ Incident Management System → TIP

زي ما إحنا عارفين أكيد إن الـ IMS مهمته هي تنظيم الـ Incident.

يعني بدل ما تكون القضية مجرد Alert:

```text
Alert
```

تبقى:

```text
Incident
├── Host
├── User
├── Timeline
├── Evidence
├── IOCs
├── Investigation
└── Actions
```

خلال الـ Investigation ممكن تكتشفي IOC جديد:

```text
evil[.]com
```

فتبعتيه للـ TIP:

```text
IMS
 ↓
evil[.]com
 ↓
TIP
```

بحيث يتخزن مع الـ Context المناسب.

---

# 3️⃣ External Sources → TIP

دي طبعًا خطوة مهمة، وهي إن مش لازم أعتمد بس على المعلومات الداخلية اللي أنا لقيتها.

ممكن أخد Threat Intel من مصدر خارجي.

مثلًا لو لقيت Hash للـ File ممكن أبعتُه على **VirusTotal** وهلاقي معلومات تانية وتفاصيل.

مثلًا:

```text
External Threat Feed
        ↓
      TIP
        ↓
     SOC
```

الـ External Source ممكن يكون:

* Vendor
* Industry Group
* Threat Intelligence Provider
* Sharing Community

وتكون بتوفر:

* Malicious IPs
* Malicious Domains
* Hashes
* URLs
* Threat Actor Infrastructure
* Campaign Information

## طيب نيجي لسؤال مهم: ليه الـ External Source أصلًا مهم؟

تخيل إن شركة تانية اكتشفت:

```text
1.2.3.4
```

وطلع **C2 Infrastructure** جديد.

أنا لسه مشفتوش عندي.

لو الـ Threat Intelligence اتشارك:

```text
Organization A
      ↓
Discovers malicious IP
      ↓
Threat Sharing
      ↓
TIP
      ↓
Organization B
```

أنا ممكن أعرف عنه قبل ما يحصل عندي Incident مشابه.

وده معنى كلام الكتاب:

> "sharing is caring"

المقصود إن مشاركة Threat Intelligence تزيد فرص اكتشاف التهديدات.

---

# 4️⃣ Detailed Analysis → TIP

ممكن يكون عندي Analyst أو Threat Intelligence team عمل **Detailed Analysis** لـ Malware أو Attack.

مثلًا اكتشفوا:

```text
Malware X
│
├── SHA256: abc123
├── C2: evil[.]com
├── IP: 1.2.3.4
├── Persistence: Scheduled Task
└── TTP: T1053.005
```

المعلومات دي تتخزن في الـ TIP.

فبعد كده أي Analyst يلاقي:

```text
evil[.]com
```

يقدر يعمل Lookup ويلاقي الـ Context الكامل.

---

# 5️⃣ SOAR ↔ TIP

ودي من أهم العلاقات.

**SOAR = Security Orchestration, Automation and Response**

الـ SOAR يقدر يعمل:

### Automated Indicator Lookup

مثلًا:

```text
SIEM Alert
    ↓
SOAR
    ↓
Extract IP
    ↓
Query TIP
    ↓
Is it malicious?
```

بدل ما الـ Analyst تعمل Lookup يدوي.

### Automated Indicator Submission

العكس كمان.

لو الـ SOAR استخرج Indicator جديد من Incident:

```text
New IOC discovered
       ↓
SOAR
       ↓
Submit IOC
       ↓
TIP
```

فبالتالي الـ TIP يتحدث تلقائيًا.

---

# 🔄 الصورة الكاملة للـ Automation

تخيل السيناريو ده:

```text
             External Sources
                    ↓
                    TIP
                 ↙  ↓  ↘
              SIEM  SOAR  IMS
                ↓    ↓     ↓
             Alert  Auto   Incident
                ↓   Lookup    ↓
              Analyst ← Investigation
                ↓
          Detailed Analysis
                ↓
             New IOCs
                ↓
               TIP
```

ده تقريبًا الـ **SOC Ecosystem** اللي المفروض نشوفه.

---

# 6️⃣ Analyst Reports → TIP

دي كمان مهمة.

الـ Analyst ممكن تعمل Investigation وتطلع Report.

مثلًا:

```text
Incident Report
────────────────────
Malicious IP:
156[.]96[.]46[.]116

Malware:
Malware X

C2:
evil[.]com

TTP:
T1071.001

Observed:
2026-09-20
```

المعلومات المهمة من الـ Report ممكن تدخل الـ TIP.

يعني:

```text
Analyst Report
      ↓
Threat Information
      ↓
TIP
```

وبالتالي الـ Knowledge بتاعة الـ Organization بتتراكم مع الوقت.

---

# ⭐ أهم حاجة: الـ TIP مش نقطة نهاية

ماتتخيلش:

```text
TIP
 ↓
Search
```

وخلاص.

الـ TIP هو **Hub** في النص:

```text
                 External Sources
                       ↓
SIEM ───────────────→ TIP ←──────────── SOAR
                       ↑
                       │
                      IMS
                       ↑
                Analyst Reports
                       ↑
                Detailed Analysis
```

والـ TIP:

* يستقبل Indicators
* يخزن Context
* يستقبل External Intelligence
* يسمح بالـ Lookup
* يشارك المعلومات
* يتكامل مع SIEM/SOAR/IMS
* يساعد الـ Analyst في Investigation

---

# 🧩 أهم جملة في كلام الكتاب

الكتاب بيقول:

> most of the input and output from the system are indicators and threat information

يعني لو بصينا للـ TIP كـ System:

## Inputs:

```text
Indicators
Threat Information
External Feeds
Analyst Findings
Security Tool Data
```

## Processing:

```text
Storage
Enrichment
Correlation
Analysis
Lookup
```

## Outputs:

```text
Threat Information
Context
Indicators
Intelligence
```

وبعدين الـ Security Tools والـ Analysts يستخدموها.

---

# 🎯 ليه كل ما عندك Sources أكتر يكون أفضل؟

الكتاب بيقول:

> the more sources you have of malicious indicators and threat information ... the more likely you are to catch attackers

الفكرة إن كل Source ممكن يشوف جزء مختلف من الـ **Threat Landscape**.

مثلًا:

```text
Source A → Malicious IPs
Source B → Malware Hashes
Source C → Threat Actors
Source D → Phishing Domains
Source E → Industry-specific threats
```

الـ TIP يجمعهم في مكان واحد.

لكن فيه نقطة مهمة جدًا من الكتاب:

> Ideally tailored for your industry and environment

يعني مش أي Threat Feed وخلاص.

الأفضل إن الـ Intelligence تكون **Relevant** لبيئتك وصناعتك.

مثلًا لو عندك **Healthcare Organization**، Threat Intelligence مرتبطة بالـ Healthcare Threats ممكن تكون أكثر Relevance من Feed عام مليان Indicators مش مرتبطة ببيئتك.

---

# 🧠 اربطي كل صفحات الـ TIP ببعض

إحنا بدأنا بـ:

## صفحة 1:

**What is TIP?**

```text
Knowledgebase + Integration + Automation
```

## صفحة 2:

**Features**

```text
Store + Lookup + Context + Correlation + Sharing
```

## صفحة 3:

**Requirements**

```text
What do I actually need to store and how much?
```

## الصفحة دي:

**How does the TIP interact with the entire SOC?**

يعني:

```text
                    External Sources
                          ↓
                          ↓
SIEM ───────────────→  TIP  ←──────────── SOAR
 │                     │ ↑                  │
 │                     │ │                  │
 ↓                     ↓ │                  ↓
Alerts             IMS / Analysis      Automation
 │                     │
 └────────→ Analyst ←──┘
              │
              ↓
        Reports / Findings
              │
              ↓
             TIP
```

---

# 📝 إيه اللي يتفهم كويس؟

الـ **TIP Workflow** كده:

> **TIP acts as a central hub for threat information, receiving indicators from security tools and external sources, storing and correlating them, and making them available through lookups, APIs, automation, and sharing.**

وبالعربي:

الـ TIP هو **Hub في الـ SOC** بيستقبل Threat Information من الـ SIEM والـ IMS والـ External Sources والـ Analysts، يخزنها ويربطها ببعض، وبعد كده يتيحها للـ SIEM/SOAR/Analysts عن طريق **Lookup وAPI وAutomation**.

---

# ⭐ وأهم 4 حاجات في السلايد

```text
Input
  ↓
Store / Correlate
  ↓
Lookup / Automation
  ↓
Decision
```

يعني في الآخر الهدف مش إننا نجمع IOCs كتير؛ الهدف إن الـ **Threat Intelligence** توصل للـ Analyst في الوقت والمكان اللي تساعدها فيه على الـ **Detection وInvestigation واتخاذ القرار**.
