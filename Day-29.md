# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 29 - Tips for Successful Incident Categorization

## Tips for Successful Incident Categorization

احنا مش بنصنف ال incident عشان بس نملا بيانات احنا بنجمعها عشان نعرف نجاوب علي اسئلة تساعدنا نحسن من جودة ال security operation
و اول حاجه هنبدأ بيها هي:

### 1- Begin with the end in mind

و دي معناها اني ابدا بالنتيجه اللي انا عايزة اوصلها بعدين احدد الداتا اللي انا محتاجاها و اجمعها

مش كده:

```text
عندي Data كتير
      ↓
هطلع منها Metrics وخلاص
```

لكن:

```text
What do I want to know?
          ↓
What metric answers it?
          ↓
What data do I need?
          ↓
What threshold matters?
          ↓
What action will I take?
```

دلوقتي انا لازم اسال:

**What question do we want to answer?**

يعني ال SOC عاوز يعرف ايه مثلا:

**هل في Attack Method معين بينجح كتير؟**

إذن محتاجين Metric مناسب.

أو:

**هل الـ SOC عنده Alerts أكتر من قدرته؟**

يبقى محتاجين نقيس الـ Workload.

أو:

**هل الـ Phishing بيزيد؟**

يبقى نتابع Phishing Attempts.

أو:

**هل الـ SOC سريع في الاستجابة؟**

يبقى نقيس Dwell Time / Response Times.

---

### نيجي دلوقتي للسؤال التاني و هو:

## Which numbers will we need?

هو باختصار متوسط عدد ال tickets الموجودة في ال queue او ال **Average Queue Length**

طيب إيه **Average Queue Length**؟

يعني بدل ما أبص على الـ Queue في لحظة واحدة، أشوف متوسط عدد الـ Tickets اللي كانت مستنية خلال فترة معينة.

طب ليه الـ SOC يهتم بالرقم ده؟

علشان يعرف:

* هل الـ Analysts قادرين يلحقوا الـ Alerts ولا لأ؟

لو الطبيعي عندك:

```text
Average Queue = 10–20
```

وفجأة بقى:

```text
Average Queue = 80
```

🚨 هنا غالبًا الفريق **Overloaded**.

ممكن يكون السبب:

* Alerts زادت جدًا.
* فيه Rule بتطلع False Positives كتير.
* عدد الـ Analysts قليل.
* فيه Incident كبير واخد وقت الفريق.

---

## رقم تلاته: What is the threshold for action?

و دي معناها مش كل رقم اشوفه بيبقي محتاج action، بل بالعكس انا لازم احدد امتي الرقم يبقي كبير او صغير بشكل غير طبيعي لدرجة يستدعي تدخل؟

مثلاً:

### Average Queue Length

```text
0–20    → Normal
21–40   → Watch
41+     → Action Required
```

لو وصل:

```text
45 tickets
```

يبقى فيه **Threshold** اتكسر.

فتبدأي تسألي:

**ليه الـ Queue كبيرة؟**

ممكن:

* Alerts زادت.
* Rule فيها مشكلة.
* عدد الـ Analysts قليل.
* Incident كبير شاغل الفريق.

---

## رابع حاجه هي What actions will you take?

و دي نقطة مهمه طبعا و الكتاب بيقول:

> do not report numbers because you can

يعني باختصار متقعدش تلم في metric لمجرد انك قادر تجمعها لازم يكون في غرض ورا ال metric دي.

مثلاً:

```text
Metric:
Average Queue Length

Threshold:
> 40

Action:
Investigate workload
Tune noisy rules
Reallocate analysts
```

كده الـ Metric بقى **Actionable**.

---

# 🔥 مثال 1: Which attack methods are working?

السؤال:

**إيه طرق الهجوم اللي بتنجح عندنا؟**

مش بس نسجل:

```text
Phishing = 500 attempts
```

لكن نهتم بالـ:

### Successful Delivery Vectors

يعني:

**أي Attack Vector نجح فعلًا في الوصول أو التأثير؟**

مثلاً:

```text
Phishing → 100 attempts → 10 successful
Web Exploit → 50 attempts → 20 successful
USB → 30 attempts → 1 successful
```

ده بيديك معلومة مهمة جدًا:

**الـ Web Exploit عنده Success Rate أعلى في البيئة دي.**

فممكن تحتاجي تحسني دفاعات الـ Web.

---

# 🔥 مثال 2: Are we overloaded?

السؤال:

**هل فريق الـ SOC عليه ضغط زيادة؟**

نقيس مثلاً:

**Average Queue Length**

عدد الـ Cases الموجودة في الـ Queue.

أو:

**Ticket Workload**

حجم الـ Tickets اللي بيتعامل معاها الفريق.

مثلاً:

```text
Incoming Alerts ↑
        +
Queue Length ↑
        +
Analyst Workload ↑
        ↓
SOC Overloaded
```

وده ممكن يخلي الإدارة تحتاج:

* Analysts إضافيين.
* Automation.
* Rule Tuning.
* Better Prioritization.

---

# 🔥 مثال 3: Track Phishing Attempts

السؤال:

**هل محاولات الـ Phishing بتزيد؟**

السلايد بتقول نتابع:

* Reported Emails
* Blocked Emails
* Phishing Incidents

مثلاً:

```text
Reported Emails
      ↓
Blocked Emails
      ↓
Actual Phishing Incidents
```

ممكن تكتشفي:

```text
August → 100
September → 150
October → 300
```

يبقى فيه Trend واضح:

**Phishing activity increasing.**

لكن خلي بالك: زيادة الـ Reports مش بالضرورة معناها زيادة الهجمات فقط؛ ممكن تعكس أيضًا تحسن وعي الموظفين والإبلاغ.

---

# 🔥 مثال 4: Dwell Time

السؤال:

**قد إيه المهاجم بيقعد في البيئة قبل ما نكتشف/نحتوي النشاط؟**

هنا نتابع أوقات مثل:

### Time to Acknowledge

من لحظة Alert لحد ما Analyst يبدأ يتعامل معاه.

### Time to Contain

من لحظة اكتشاف المشكلة لحد ما يتم Containment.

مثلاً:

```text
Alert
 ↓ 5 min
Acknowledged
 ↓ 20 min
Contained
```

يبقى عندك:

```text
Time to Acknowledge = 5 min
Time to Contain = 20 min
```

لو متوسط الـ Time to Contain بدأ يزيد:

**محتاجين نعرف ليه.**

---

# 🔥 مثال 5: Is the Security Team doing a good job?

السؤال هنا مش:

**"هل الـ Analysts شاطرين؟"**

بمعنى شخصي.

لكن:

**هل أداء الـ Security Team فعّال؟**

ممكن نتابع:

### Critical Incident Count

عدد الـ Critical Incidents.

و:

### Impact

حجم تأثيرهم.

مثلاً:

```text
Quarter 1:
Critical Incidents = 20
High Impact = 15

Quarter 2:
Critical Incidents = 10
High Impact = 4
```

ده ممكن يشير إلى تحسن.

لكن برضه مش لوحده دليل قاطع؛ لازم نحط الأرقام في سياقها.

---

# 🧠 أهم فكرة في الجزء ده

## Know what normal is

يعني لازم اسأل نفسي:

**Do I know what normal is?**

عشان لما تيجي حالة مثلا ازاي هقول انها غير طبيعية و انا معرفش ال **Normal Baseline**.

مثلاً:

عادةً عندك:

```text
20–30 Alerts/day
```

وفجأة:

```text
500 Alerts/day
```

هنا فيه **Anomaly** واضحة.

لكن لو أصلًا الطبيعي عندك:

```text
400–600 Alerts/day
```

فالـ 500 مش حاجة غريبة.

---

# 🧠 اربطي الأربع أسئلة ببعض

كل Metric تسألي عليه:

### 1. Why?

ليه بجمع الرقم ده؟

### 2. What?

إيه السؤال اللي الرقم هيجاوب عليه؟

### 3. Threshold?

إمتى الرقم يستدعي Action؟

### 4. Action?

هعمل إيه لما الـ Threshold يتكسر؟

مثلاً:

```text
Question:
Are we overloaded?

        ↓

Metric:
Average Queue Length

        ↓

Normal:
< 30

        ↓

Threshold:
> 50

        ↓

Action:
Investigate workload
+
Tune noisy alerts
+
Consider analyst allocation
```

---

# 🔄 وده بيربط كل اللي خدناه لحد الآن

أنتِ من أول الجزء ده بتبني صورة كاملة:

```text
EVENT
  ↓
ALERT
  ↓
TRIAGE
  ↓
CASE / INCIDENT
  ↓
CATEGORIZATION
  ↓
INVESTIGATION
  ↓
CLOSED CASE
  ↓
METRICS
  ↓
TRENDS
  ↓
IMPROVE SOC
```

يعني الـ Closed Cases مش مجرد تاريخ قديم.

هي Data نقدر نتعلم منها.

---

# ⭐ افهم السلايد دي كده

**Start with the question, not the metric.**

يعني:

**Question → Metric → Threshold → Action**

والأمثلة الأربعة المهمة:

| السؤال                            | الـ Metric                            |
| --------------------------------- | ------------------------------------- |
| Which attacks are working?        | Successful delivery vectors           |
| Are we overloaded?                | Average queue length / workload       |
| Are phishing attempts increasing? | Reported + blocked emails + incidents |
| How fast do we respond?           | Time to acknowledge / contain         |
| Are we effective?                 | Critical incident count + impact      |

---

# 🎯 الخلاصة

**Metric من غير Action = غالبًا مجرد رقم.**

لكن:

**Useful Metric = رقم له سؤال + Baseline + Threshold + Action.**

وده بالضبط اللي SANS عايزك تفهميه من السلايد.
