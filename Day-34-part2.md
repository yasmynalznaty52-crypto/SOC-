# بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 34 - Part 2

## Intelligence Definition

الجزء ده بيشرح يعني إيه **Intelligence** أصلاً قبل ما نقول **Cyber Threat Intelligence (CTI)**.

الكتاب بيقول:

> "Taking in external information from a variety of sources and analyzing it against existing requirements in order to provide an assessment that will affect decision making."

الجملة كبيرة، لكن هنشرحها جزء جزء 👇

---

## 1️⃣ يعني إيه Intelligence؟

هو عبارة عن **معلومات خارجية أنا حللتها وقارنتها مع حاجة معينة أو احتياج معين عشان تساعدني على اتخاذ قرار**.

وده معناه إن مش أي معلومة وخلاص.

لا، بتكون معلومة:

**جمعتها → حللتها → قارنتها باحتياج معين → طلعت Assessment → خدت قرار بناءً عليها.**

---

## 2️⃣ Taking in External Information

يعني:

**بأخذ معلومات من مصادر خارجية.**

مثلاً:

```text
Threat Intelligence Feed
        ↓
   Malicious IP
        ↓
     185.x.x.x
```

دي معلومة جاية من **مصدر خارجي**.

لكن لسه **مش Intelligence كاملة**.

لأننا لسه ما حللناهاش، ولسه مش عارفين تأثيرها على بيئتنا.

---

## 3️⃣ From a Variety of Sources

ده معناه إني مش لازم أعتمد على مصدر واحد أجيب منه المعلومة.

لا، لازم أشوف أكتر من مصدر وأجمع معلومات مختلفة.

مثلاً في الـ Cyber ممكن أجمع:

```text
Threat Feed
     +
Security Research
     +
MISP
     +
Vendor Report
     +
Our SIEM Logs
     +
Incident History
```

كل ده بيديني معلومات مختلفة، وبعد كده أبدأ **أربط المعلومات ببعض** وأحللها.

---

## 4️⃣ Analyzing It

دي أهم حاجة تقريبًا.

وهنا بيقول إن مش مجرد إني جبت Data وقلت:

> أهو عندي معلومة.

لا، لازم **أحللها وأستفاد منها عن طريق إني أطلع منها معلومة جديدة ومفيدة**.

مثلاً عندي:

```text
IP = 185.10.20.30
```

Threat Feed بيقول:

```text
Malicious
```

لكن أنا أبدأ أحلل:

* مين استخدم الـ IP؟
* مرتبط بأي Malware؟
* بيستخدم كـ C2 ولا Hosting؟
* ظهر إمتى؟
* هل استهدف قطاع معين؟
* هل ظهر عندي في الـ Logs؟
* هل في أجهزة داخلية اتصلت بيه؟

هنا بدأت أحول:

```text
Data → Meaning
```

---

## 5️⃣ Against Existing Requirements

ده معناه إني مش بجمع حاجات كده وخلاص.

لا، أنا عندي **سؤال عايزله إجابة** أو **حاجة معينة محتاج أعرفها**.

### مثال بسيط جدًا من الكتاب:

### 🌦️ Weather Report

المعلومة:

```text
Temperature = 15°C
Rain = Expected
```

لو أنا بس قريتها، دي:

**Information**

لكن عندي Requirement:

> هل أنا محتاج أخد جاكت النهارده؟

أبدأ أحلل:

```text
Cold + Rain
      ↓
I need a coat
```

هنا المعلومة أثرت على القرار بتاعي، يبقى هي كده:

**Intelligence**

---

## 6️⃣ مثال الـ Traffic Report

السلايد بتقول:

> Traffic Report: How much time do I need to get to work?

خلينا نفكر فيها.

المعلومة:

```text
Traffic is heavy
```

دي كده:

**Information**

لكن أنا عندي Requirement:

> لازم أوصل الشغل الساعة 9:00.

أحلل:

```text
Normal travel time = 30 min
Traffic delay      = +30 min
Expected travel    = 60 min
```

فالنتيجة:

```text
لازم أتحرك الساعة 8:00 بدل 8:30.
```

دي بقى **Intelligence** لأن التحليل أدى إلى:

**Decision**

---

# 7️⃣ نطبق نفس الفكرة على Cybersecurity

ودي أهم حاجة بالنسبة لينا. 🔥

افترض إن عندي:

```text
IP: 185.10.20.30
```

لقيته في **Threat Intelligence Feed**.

الـ Feed بيقول:

```text
Known malicious IP
```

دي:

**Information**

لكن عندك Requirement:

> هل الـ IP ده يمثل Threat حقيقي لبيئتنا؟

أبدأ أحلل:

```text
185.10.20.30
       ↓
Known C2
       ↓
Associated with Malware X
       ↓
Seen recently
       ↓
Our host 10.10.10.25 connected to it
```

الـ **Assessment** هنا:

```text
There is a high likelihood that the internal host may be compromised.
```

والقرار:

```text
Isolate host
        +
Investigate endpoint
        +
Search for related IOCs
        +
Reset credentials if necessary
```

هنا بقى عندي:

**Intelligence**

---

# 8️⃣ الفرق بين Information و Intelligence

دي حاجة مهمة لازم نفهم الاختلاف.

### Information

هي معلومة عادية أو بيانات عادية عندي.

### Intelligence

هي عبارة عن معلومة أنا **حللتها** وحاولت أطلع منها معلومة مفيدة تساعدني فيما بعد إني **أقرر أو أخد قرار**.

مثلاً:

```text
IP = 1.2.3.4

      ↓ Analysis

Known C2 infrastructure
+
Associated with ransomware
+
Our host communicated with it

      ↓ Assessment

Possible compromise

      ↓ Decision

Isolate the host
```

إذن:

```text
Information
    ↓
Analysis
    ↓
Assessment
    ↓
Decision
```

---

# 9️⃣ أهم Formula في الصفحة

دي من أهم الـ Concepts في الـ **Threat Intelligence**:

```text
External Information
        ↓
     Analysis
        ↓
Compare with Requirements
        ↓
    Assessment
        ↓
Decision Making
```

وده بيوضح إن **Intelligence** مش مجرد Data.

لازم يكون عندنا:

**Information + Analysis + Requirement + Assessment → Decision**

---

# 🔟 طب إيه معنى Assessment؟

كلمة **Assessment** هنا مش معناها إني أعيد المعلومة زي ما هي.

مثلاً بدل ما أقول:

> "الـ IP ده malicious."

أقول:

> بناءً على المعلومات المتاحة، في احتمال كبير إن الجهاز الداخلي اتعرض لاختراق.

ده:

**Assessment**

يعني:

> **استنتاج مبني على تحليل الأدلة.**

بمعنى:

```text
Evidence
   ↓
Analysis
   ↓
Assessment
```

---

# 1️⃣1️⃣ وده يفسر ليه CTI مش مجرد IOC List

لأن السلايد اللي فات كنا بنقول:

> **NOT just a list of bad domains and IP addresses**

لأن:

```text
Bad IP List
```

لوحدها = **Information**

لكن:

```text
Bad IP
   +
Context
   +
Analysis
   +
Our Environment
   +
Assessment
   +
Recommended Action
```

=

**Intelligence**

وده فرق كبير جدًا.

---

# 1️⃣2️⃣ العلاقة بين Intelligence و Threat Intelligence

الكتاب حاطط:

```text
Intelligence
      ↓
Threat Intelligence
      ↓
Cyber Threat Intelligence
```

الفكرة إننا بنبدأ بالمفهوم العام:

### Intelligence

معلومات وتحليل يساعدنا على اتخاذ قرار.

⬇️

### Threat Intelligence

نطبق نفس المفهوم على **Threats**.

⬇️

### Cyber Threat Intelligence

نطبقها على **Cyber Threats**.

يعني:

```text
Intelligence
      ↓
Threats
      ↓
Cyber Threats
      ↓
Cyber Threat Intelligence
```

---

# 🔥 مثال أخير يثبت الموضوع

تخيل إني **SOC Analyst**.

وصلّي:

```text
Alert:
User connected to evil.com
```

## Step 1 — Information

أنا أعرف إن:

```text
Domain = evil.com
```

دي مجرد:

**Information**

---

## Step 2 — External Information

Threat Intelligence تقول:

```text
evil.com = malicious
```

لسه عندي Information.

---

## Step 3 — Analysis

أكتشف:

```text
Domain → Phishing
Domain → Credential Theft
Domain → Campaign X
```

وأقارنها بالبيئة بتاعتي:

```text
Our user visited it
        +
Submitted credentials
```

---

## Step 4 — Assessment

أستنتج:

```text
User credentials may have been compromised.
```

ده هو:

**Assessment**

---

## Step 5 — Decision

أقرر:

```text
Reset credentials
        +
Revoke sessions
        +
Investigate endpoint
        +
Hunt for other affected users
        +
Block domain
```

ده:

**Intelligence**

---

# 🧠 الخلاصة

**Intelligence is not simply information.**

It is:

> **Information collected from different sources, analyzed against a specific requirement, turned into an assessment, and used to support decision making.**

وأهم Flow:

```text
Information
     ↓
  Analysis
     ↓
Requirement
     ↓
 Assessment
     ↓
Decision
```

وفي الـ Cyber:

```text
Threat Data
     ↓
Analysis + Context
     ↓
CTI
     ↓
Assessment
     ↓
Defensive Decision
     ↓
Action
```

## ⭐ أهم Concept

```text
Data ≠ Intelligence
```

المعلومة لوحدها مش كفاية.

لازم:

```text
Data
 ↓
Analysis
 ↓
Context
 ↓
Requirement
 ↓
Assessment
 ↓
Decision
```

عشان نقدر نقول إن عندنا **Intelligence**.
