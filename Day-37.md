# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 37 — Cyber Threat Intelligence Definition

## 1️⃣ أول تعريف: Threat Intelligence

الكتاب بيقول:

> Threat intelligence is the analysis of adversaries – their capabilities, motivations, and goals

يعني هو عبارة عن تحليل لل attacker نفسه
عنده ايه ؟ عايز ايه ؟ هدفه ايه ؟

مثلًا عندي Threat Actor اسمه X.

أنا أدرس:

```text
Threat Actor X
    │
    ├── Capabilities
    │     └── Malware / Tools / Skills
    │
    ├── Motivations
    │     └── Money / Espionage / Revenge
    │
    └── Goals
          └── Steal credentials / Encrypt files
```

فأنا مش بس بقول:

> "X is malicious."

أنا بحاول أفهم الـ adversary.

---

## 2️⃣ طيب إيه اللي يخليها Cyber Threat Intelligence؟

هنا الجزء المهم جدًا:

> CTI is the analysis of how adversaries use the cyber domain to accomplish their goals.

وده معناه إن أنا مش مهتمة بس بالمهاجم، أنا مهتمة كمان إنه **إزاي هيستخدم الـ cyber domain عشان يوصل للهدف بتاعه**.

يعني أدرس:

* Malware
* Phishing
* Exploitation
* Credential Theft
* C2
* Persistence
* Lateral Movement
* TTPs

مثال:

الـ Threat Actor هدفه:

> Steal credentials

أحلل إزاي بيعمل ده cyber-wise:

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
      ↓
Exfiltration
```

ده Cyber Threat Intelligence.

---

## 3️⃣ أهم حاجة نركز فيها هي كلمة Analysis

الكتاب بيقول:

> Human analysis required

ودي مهمة جدًا.

يعني الـ CTI مش مجرد إن tool تقولك:

```text
IP = malicious
```

وخلاص.

لا، الـ human analyst لازم يفهم:

* Who?
* What?
* Why?
* How?
* Targeting whom?
* Using what TTPs?
* Is it relevant to us?
* What should we do?

وده يرجعنا لكلامنا:

```text
Information
    ↓
Investigation
    ↓
Enrichment
    ↓
Analysis
    ↓
Context
    ↓
Intelligence
```

---

## 4️⃣ Identify TTPs and Goals

الصفحة دي بتقول إن من أهداف CTI:

> Identify TTPs and goals of threat actor

### TTPs

يعني:

> Tactics, Techniques, and Procedures

بمعنى المهاجم ده بيعمل ايه وبيعمله ازاي؟

مثلاً:

**Tactic:**

> Credential Access

**Technique:**

> OS Credential Dumping

**Procedure:**

> Using a specific tool/command to dump credentials

وفي نفس الوقت أعرف:

**Goal إيه؟**

مثلاً:

> Goal → Steal credentials

فأنا بربط:

```text
Threat Actor
     ↓
Goal
     ↓
TTPs
     ↓
How they operate
```

---

## 5️⃣ "Output drives decision making"

ودي أهم جملة في الصفحة دي بالنسبة للـ SOC:

> Output drives decision making

يعني في النهاية أنا مش بعمل CTI عشان أعرف معلومات وخلاص.

لا، أنا عايز بناءً عليه أقرر أنا هعمل إيه.

مثلاً التحليل يقول:

> Threat Actor X is targeting organizations in our sector using phishing → PowerShell → C2.

إذن أقدر أقرر:

```text
Decision
   ↓
Create detection for PowerShell behavior
   ↓
Hunt for related IOCs
   ↓
Block malicious infrastructure
   ↓
Increase monitoring
   ↓
Check vulnerable systems
```

فـ CTI لازم يكون **actionable**.

---

## 6️⃣ وده يرجعنا لسؤال مهم

"المعلومة اللي بعمل عليها investigation و enrichment و analysis وبعدها يبقى عندي context، الناتج ده Intelligence صح؟"

أيوه.

والصفحه دي بتضيف:

لو الـ information والتحليل متعلقين بـ adversaries والـ cyber attacks:

```text
Information
     ↓
Investigation + Enrichment + Analysis
     ↓
Context + Assessment
     ↓
Cyber Threat Intelligence
     ↓
Decision
```

---

## 7️⃣ مثال SOC كامل

خلينا ناخد مثال قريب من اللي بنعمله في لابات THM.

عندي:

```text
IP: 45.x.x.x
```

و Threat Feed بتقول إنه مرتبط بـ malware.

دي معلومة أولية.

أبدأ أعمل investigation.

### Enrichment

أكتشف:

```text
Associated Malware → Malware X
Threat Actor → Actor Y
Known Purpose → C2
```

### Correlation

بعدين أروح للـ SIEM:

```text
Internal Host
      ↓
45.x.x.x
```

وأكتشف إن جهاز داخلي اتصل بالـ IP.

### Analysis

أربط الأحداث:

```text
Phishing
   ↓
Malware execution
   ↓
C2 connection
   ↓
Credential activity
```

وأوصل لـ assessment:

> "This activity is consistent with a potential compromise by Threat Actor Y."

هنا بقى عندي **CTI مفيدة**.

وبعدها:

```text
CTI
 ↓
Decision
 ↓
Investigate host
 ↓
Isolate if needed
 ↓
Hunt for same TTPs
 ↓
Block infrastructure
```

---

## طب إيه علاقة ده بالـ Threat Definition اللي خدناه؟

سبق وقلنا:

```text
Threat =
Intent + Capability + Opportunity
```

دلوقتي CTI بتساعدني أفهم الـ adversary:

```text
Intent
  ↓
Why are they attacking?

Capability
  ↓
What can they use?

TTPs
  ↓
How do they operate?

Goals
  ↓
What are they trying to achieve?

Opportunity
  ↓
Can they exploit something in my environment?
```

فأنا في النهاية أقدر أحدد:

> هل الـ adversary ده Threat بالنسبة لمنظمتي؟

---

## 9️⃣ والـ 3 مستويات بقت واضحة

```text
┌────────────────────────────┐
│       Intelligence         │
│ Analyzed information       │
│ used for decisions         │
└──────────────┬─────────────┘
               ↓
┌────────────────────────────┐
│     Threat Intelligence    │
│ Analysis of adversaries    │
│ capabilities/goals/etc.    │
└──────────────┬─────────────┘
               ↓
┌────────────────────────────┐
│ Cyber Threat Intelligence  │
│ How adversaries use cyber  │
│ to accomplish their goals  │
└────────────────────────────┘
```

---

# أهم حاجة نفهمها من الصفحة

CTI مش IOC feed.

يعني:

```text
IOC
↓
Piece of information
```

لكن:

```text
IOC
+ Threat Actor
+ Motivation
+ Goals
+ TTPs
+ Context
+ Analysis
+ Relevance to our environment
        ↓
       CTI
        ↓
     Decision
```

وده سبب إن السلايد قالت:

> Human analysis required

لأن الـ tool ممكن تجمعلك البيانات، لكن الـ analyst هو اللي يحطها في context ويفسرها ويطلع assessment مفيد للقرار.

---

# أهم حاجه هي الجملة دي

> Cyber Threat Intelligence is the analysis of how adversaries use the cyber domain to accomplish their goals.

وافهمها كده:

> أنا بدرس الـ attacker: هو مين، عايز إيه، عنده إيه، وبيستخدم إيه وإزاي في الـ cyber domain عشان يوصل لهدفه، وبطلع من التحليل ده information/assessment يساعدني آخد defensive decision.
