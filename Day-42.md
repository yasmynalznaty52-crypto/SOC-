بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 42 — Threat Intelligence Platform Products

## Threat Intelligence Platform (TIP) vs Threat Intelligence Vendor / Provider

---

# 1️⃣ Threat Intelligence Platform Products

عندي نوعين أساسيين:

## 1. Self-Hosted / Free

ده أقدر أستضيفه عندي وأستخدمه زي مثلًا:

* MISP
* OpenCTI

## 2. Commercial

دي منتجات تجارية أنا بشتريها من شركات مختلفة زي مثلًا:

* Palo Alto XSOAR TIM
* CrowdStrike Falcon X
* LogRhythm TLM
* ThreatConnect
* Recorded Future
* IBM X-Force Exchange
* Anomali ThreatStream

مش مهم أعرف أسامي كل دول.

---

# 1️⃣ MISP

**MISP = Malware Information Sharing Platform**

وده Open Source وممكن يتعمله **Self-Hosting**.

يعني مثلًا:

```text
Your Organization
      │
      ↓
    MISP
      │
 ┌────┼────┐
 ↓    ↓    ↓
IPs  Hashes Domains
```

تقدري تخزني فيه:

* IPs
* Domains
* URLs
* Hashes
* Threat Information
* Context
* Relationships

---

# 2️⃣ OpenCTI

ده برضو **Self-Hosted / Open Source**.

فكرته حلوة وكويسة، زي إنه مثلًا بيعمل:

**Relationship + Threat Intelligence**

يعني مش بس:

```text
IP → Bad
```

لكن ممكن أشوف العلاقات:

```text
Threat Actor
     ↓
Campaign
     ↓
Malware
     ↓
Infrastructure
     ↓
IP / Domain
     ↓
TTP
```

وده بيساعدني أشوف الـ **Threat Landscape** كـ Relationships.

---

# طيب إيه هو الـ Commercial TIPs؟

دي زي ما قولنا إنها عبارة عن منتجات بتعملها الشركات، وغالبًا بتكون جزء من **Ecosystem** أكبر.

الكتاب بيديني أمثلة زي:

```text
Palo Alto XSOAR TIM
CrowdStrike Falcon X
ThreatConnect
Anomali ThreatStream
...
```

والاختيار بيعتمد طبعًا على حاجات كتير منها:

* الـ Depth of Analysis اللي محتاجاه
* حجم الـ Threat Intelligence
* الـ Integrations الموجودة
* الـ Security Tools اللي عندك
* الـ Workflow بتاع الـ SOC
* هل محتاجة Sharing؟
* هل محتاجة Custom Fields / Relationships؟
* حجم الـ Indicators

يعني مفيش:

> "أفضل TIP في العالم"

بشكل مطلق.

---

# ⚠️ أهم حاجة في الصفحة

أهم حاجة في الصفحة دي آخد بالي منها هي:

> **A threat intelligence platform does not produce intelligence for you.**

دي اتكلمنا عنها قبل كده، وبنأكد عليها تاني.

يعني لو عندي:

```text
MISP
```

مش معنى إني عملت MISP إني فجأة بقي عندي **Threat Intelligence جاهزة**.

MISP ممكن يساعدني في:

```text
Store
Query
Correlate
Share
Integrate
```

لكن الـ **Intelligence نفسها** لازم تكون:

* إنتِ عملتيها.
* أو حصلتي عليها من مصدر خارجي.
* أو اتعملت بواسطة Threat Intelligence Team / Vendor.

---

# Threat Intelligence Platform vs Threat Intelligence Vendor

وهنا بقى الفرق المهم جدًا.

الكتاب بيفرق بين:

**Threat Intelligence Platform**

و

**Threat Intelligence Vendor**

---

## 🟦 TIP

مثال:

```text
MISP
```

دوره:

```text
Your Threat Intelligence
        ↓
      MISP
        ↓
Store / Query / Correlate / Share
```

يعني هو منصة لإدارة الـ Intelligence.

---

## 🟩 Threat Intelligence Vendor

شركة عندها **Threat Intelligence Analysts** بيعملوا Analysis ويطلعوا Reports.

مثلًا بشكل عام:

```text
Threat Intelligence Vendor
        ↓
Researchers / Analysts
        ↓
Collect + Analyze
        ↓
Threat Reports / Intelligence
```

أنا لما أشتري / أستهلك الـ Intelligence دي، ممكن بعد كده أدخلها في TIP عندي:

```text
Threat Intelligence Vendor
          ↓
      Intelligence
          ↓
         TIP
          ↓
     Your SOC
```

---

# مثال يثبت الفرق

تخيلي إن عندي:

```text
MISP
```

ولقيت فيه:

```text
IP: 1.2.3.4
```

MISP مش هيقولي تلقائيًا:

> "الـ IP ده جزء من Campaign X التابعة لـ Threat Actor Y، والهدف هو قطاع Z."

إلا لو المعلومة دي موجودة أصلًا أو تم إدخالها / تحليلها من مصدر آخر.

لكن لو عندي **Threat Intelligence Vendor**، ممكن ألاقي Report فيه:

```text
Threat Actor: X
Campaign: Y
Malware: Z

Infrastructure:
1.2.3.4
evil[.]com

TTPs:
T1566
T1059
T1071
```

دي **Intelligence produced by analysts**.

بعد كده أقدر أدخل المعلومات دي إلى الـ TIP عندي.

---

# الـ Flow المهم جدًا

```text
External Threat Intelligence
        │
        │
        ↓
┌────────────────────┐
│ Threat Intelligence │
│ Vendor / Researchers│
└────────────────────┘
        │
        ↓
   Intelligence
        │
        ↓
       TIP
        │
 ┌──────┼──────┐
 ↓      ↓      ↓
SIEM   SOAR    IMS
        │
        ↓
   SOC Analyst
```

وفي نفس الوقت ممكن الـ Analyst عندي يكتشف حاجة جديدة:

```text
Incident Investigation
        ↓
New IOC / Analysis
        ↓
TIP
        ↓
Share with others
```

يعني الـ TIP ممكن يحتوي على Intelligence:

```text
جايالي من بره + أنا أنتجتها داخليًا
```

---

# MISP لا ينتج Threat Intelligence بنفسه

**"MISP is a Threat Intelligence Platform"**

فهم غلط:

> "يبقى MISP هو اللي هيعمل Threat Intelligence."

❌ لأ.

الأصح:

> **MISP enables you to manage, store, query, correlate, and share Threat Intelligence.**

لكن الـ **Analysis and Intelligence Production** لسه محتاجة:

* Analysts
* Threat Intelligence Team
* External Intelligence Providers

---

# 🔗 اربطيها بكل اللي خدناه

من أول صفحات الـ CTI:

```text
Raw Data
   ↓
Analysis
   ↓
Context
   ↓
Assessment
   ↓
Threat Intelligence
```

مين ممكن يعمل الـ Analysis؟

```text
┌────────────────────────────┐
│ Internal CTI Team          │
│ SOC / Security Analysts    │
│ External Intelligence      │
│ Researchers / Vendors      │
└────────────────────────────┘
              ↓
        Threat Intelligence
              ↓
             TIP
              ↓
       Store / Query / Share
              ↓
             SOC
```

---

# 🧠 إيه اللي يتفهم من الصفحة؟

## Examples of TIPs

اللي محتاجاه بشكل أساسي:

* **MISP و OpenCTI** → Open Source / Self-Hosted examples.
* الـ Commercial examples مش محتاجة أحفظ كل اسم إلا لو الكورس طلب مني.

والأهم:

### TIP

> Stores and queries threat information/intelligence.

### Threat Intelligence Vendor

> Produces/provides intelligence through analysts and reports.

---

# 🎯 الخلاصة

لو سألت:

### هل MISP بيعمل Threat Intelligence؟

الإجابة:

> **لا، مش بالمعنى المقصود هنا.**

هو بيساعدك:

```text
تخزني
تبحثي
تربطي
تتبادلي
وتستخدمي
```

الـ **Threat Intelligence**.

أما الـ Intelligence نفسها ممكن تكون:

```text
Created by your team
        +
Obtained from external sources/vendors
        ↓
       TIP
```

وده أهم **Distinction** في الصفحة كلها:

```text
TIP = Platform for managing intelligence

Threat Intelligence Vendor = Source / Provider of intelligence
```
