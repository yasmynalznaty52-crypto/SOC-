بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 43 — Threat Intel Feeds (Part 2)

## How to Measure Feed Effectiveness?

دلوقتي هنكمل جزء إزاي نعرف نقيس **How the Feed Is Effective**.

### 1️⃣ Relevance

**Perhaps one of the most important!**

طب ليه؟

لأن ممكن Feed يكون:

* Accurate جدًا
* Fast جدًا
* مليان Indicators

لكن مش Relevant للبيئة بتاعتي.

مثال:

```text
Feed:
100,000 indicators
```

لكن معظمهم خاصين بـ:

```text
Gaming industry
```

وأنا بشتغل في:

```text
Healthcare
```

فالقيمة العملية ممكن تكون محدودة.

لذلك:

> Relevance to your industry and environment is critical.

### 2️⃣ Fields / Contents

لازم أسأل:

**الـ Feed ده بيقدم إيه؟**

مثلاً:

```text
Feed A:
IPs only

Feed B:
IPs + Domains + URLs

Feed C:
IPs + Domains + Malware + TTPs + Context
```

وده مهم جدًا عشان الـ Analyst تعرف تستخدمه بسرعة.

لو عندي Incident متعلق بـ Malware، وFeed فيه IPs فقط، ممكن مايدينيش كل الـ Context اللي محتاجاه.

### 3️⃣ Speed

**How much time is there between discovery and availability?**

يعني:

```text
Threat discovered
       ↓
Research
       ↓
Feed updated
       ↓
Your TIP
       ↓
Your SIEM/IDS
```

كل مرحلة فيها Delay.

وأنا محتاجة أعرف:

**الـ Feed Latency قد إيه؟**

### 4️⃣ Accuracy vs Completeness

مش بس هسأل:

"هل الـ Feed Accurate؟"

لكن:

**إيه الـ Definition بتاعهم للـ Accurate؟ وإيه اللي بيدخلوه وإيه اللي بيستبعدوه؟**

لأن Feed شديد الدقة لكنه يستبعد Threats غير مؤكدة ممكن يؤدي إلى:

**Missed Detections / False Negatives.**

---

# نروح بقى لـ ISACs و ISAOs

الكتاب في الآخر بيقول:

> Join ISACs and ISAOs!

ودي نقطة مهمة.

## يعني إيه ISAC؟

**ISAC = Information Sharing and Analysis Center**

وهو عبارة عن مركز لمشاركة وتحليل Cyber Threat Intel جوه قطاع معين.

يعني بدل كل شركة في قطاع معين تواجه Threats لوحدها:

```text
Company A ─┐
Company B ─┤
Company C ─┼──→ ISAC
Company D ─┤
Company E ─┘
```

المجموعة تشارك Threat Information المناسبة للقطاع.

## طيب وإيه ISAO؟

**ISAO = Information Sharing and Analysis Organization**

الفكرة قريبة، لكن الـ Scope مش لازم يكون قطاع صناعي محدد بنفس طريقة الـ ISAC.

الهدف العام:

**Information Sharing + Analysis + Collaboration**

## ليه الكتاب بيقول Join Them؟

لأنها ممكن تكون مصدر **High-value, industry-relevant information**.

يعني بدل ما أجيب Feed عام:

```text
Generic Threat Feed
```

ممكن أخد Intelligence مرتبطة مباشرة بالقطاع اللي شغالة فيه.

وده يرجعنا لأهم كلمة:

**Relevance**

---

# الـ ISACs المذكورة في السلايد

خلينا نفهم كل واحدة بدل حفظ أسماء وخلاص:

### 🏥 Health ISAC (H-ISAC)

خاص بقطاع:

**Healthcare**

يعني Threats المتعلقة بالمستشفيات، Healthcare Organizations، Medical Infrastructure... إلخ.

### 🏛️ Multi-State ISAC (MS-ISAC)

يركز على:

**State, Local, Tribal, and Territorial Governments**

والـ Cybersecurity Information المتعلقة بالجهات الحكومية المحلية / الإقليمية.

### 🗳️ EI-ISAC

**Elections Infrastructure Information Sharing and Analysis Center**

متخصص في:

**Election Infrastructure**

### 💧 Water ISAC (W-ISAC)

قطاع:

**Water / Wastewater**

### 💰 FS-ISAC

**Financial Services ISAC**

قطاع:

**Financial Services**

زي المؤسسات والخدمات المالية.

### ✈️ Aviation ISAC (A-ISAC)

قطاع:

**Aviation**

### 💻 IT-ISAC

قطاع:

**Information Technology**

### 🎓 REN-ISAC

**Research and Education Networking ISAC**

خاص بقطاع:

**Research + Education**

زي المؤسسات الأكاديمية والبحثية والشبكات التابعة لها.

### 🛍️ Retail and Hospitality ISAC

قطاع:

**Retail + Hospitality**

### 🚢 MTS-ISAC

**Maritime Transportation System ISAC**

قطاع:

**Maritime Transportation**

### 🔥 DNG-ISAC

**Downstream Natural Gas ISAC**

قطاع:

**Downstream Natural Gas**

### 🛢️ ONG-ISAC

**Oil and Natural Gas ISAC**

قطاع:

**Oil + Natural Gas**

### 🚀 S-ISAC

**Space Information Sharing and Analysis Center**

قطاع:

**Space**

---

# طيب ليه الـ ISAC مهم في الـ Threat Feed؟

ممكن الـ ISAC نفسه يوفر أو يسهّل الوصول إلى معلومات زي:

```text
Threat Actor
      ↓
Targeting your industry
      ↓
Observed TTPs
      ↓
Malware
      ↓
Infrastructure
      ↓
IOCs
```

وده بالنسبة للـ SOC Analyst Valuable جدًا، لأني مش باخد:

> "Random malicious IP from the internet"

لكن ممكن أخد:

> Threat Information مرتبطة بالـ Industry اللي أنا بحميها.

---

# 🔗 ربط الصفحة كلها ببعض

دلوقتي الـ SOC عنده:

```text
              External Sources
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
   Threat Feeds              ISAC/ISAO
        │                       │
        └───────────┬───────────┘
                    ↓
                   TIP
                    ↓
          ┌─────────┼─────────┐
          ↓         ↓         ↓
         SIEM      SOAR      IMS
          │         │         │
          └─────────┼─────────┘
                    ↓
               SOC Analyst
                    ↓
             Investigation
                    ↓
             New Intelligence
                    ↓
                   TIP
                    ↓
                Sharing
```

وده يوضح ليه الـ TIP مش مجرد Database.

هو حلقة وصل بين **Threat Intelligence Sources** والـ **Security Operations**.

---

# أهم جزء: إزاي أختار Feed؟

لو جالي Feed جديد، ماقولش:

"عنده مليون IOC → يبقى ممتاز."

أعمل Evaluation بالأسئلة دي:

### 1. Relevance

هل المعلومات دي مرتبطة بالـ Industry والـ Environment بتاعي؟

### 2. Fields / Contents

بيقدم إيه؟

* IPs?
* Domains?
* URLs?
* Hashes?
* Malware?
* TTPs?
* Threat Actors?
* Context?

### 3. Speed

قد إيه بيأخذ من وقت اكتشاف الـ Threat لحد ما المعلومة توصل للـ Feed؟

### 4. Accuracy

كام Indicator فعليًا صحيح / مفيد؟

### 5. Completeness

هل بيحاول يكون شامل ولا بيحط بس الـ Confirmed Indicators؟

### 6. Integration

هل أقدر أوصله بالـ TIP / SIEM / SOAR / Tools بتاعتي؟

### 7. Philosophy

الـ Provider Conservative ولا Inclusive في إضافة Indicators؟

---

# 🧠 ودي أهم صورة ذهنية للصفحة

ما نفكرش:

```text
Threat Feed = List of Bad IPs
```

فكر:

```text
Threat Feed
     ↓
Threat Data + Context
     ↓
Evaluate:
 ├── Relevant?
 ├── Accurate?
 ├── Complete?
 ├── Fast?
 ├── What contents?
 └── Integrates?
     ↓
    TIP
     ↓
SOC Detection / Hunting / Investigation
```

---

# 🎯 الخلاصة اللي المفروض نخرج بيها

**Threat Feed الجيد مش اللي عنده أكبر عدد من الـ IOCs.**

الـ Feed بيتقيّم بناءً على:

> **Relevance + Contents + Speed + Accuracy + Completeness + Integration**

ومهم جدًا فهم الـ **Accuracy vs Completeness Trade-off**:

* **Accuracy عالية** → Indicators مؤكدة أكثر، لكن ممكن تفوّت Threats غير مؤكدة → **False Negatives محتملة**.
* **Completeness أعلى** → Coverage أوسع، لكن ممكن تدخل Indicators مش Malicious فعلًا → **False Positives محتملة**.

وأخيرًا:

> **ISACs/ISAOs** مصدر مهم للحصول على Threat Intelligence مرتبطة بالـ Industry، وSEC450 يعتبر الانضمام إليها خطوة مفيدة للحصول على معلومات ذات قيمة وRelevance أعلى.

### ولو عايزين نربط كل Chapter لحد هنا في جملة واحدة:

**Threat Data → Threat Feed / External Sources → TIP → Enrichment/Correlation → SIEM/SOAR/IMS → SOC Analyst → Investigation & Decision → New Intelligence → Sharing.**
