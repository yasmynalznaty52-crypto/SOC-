# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 33  - TheHive: Case Closure

عندنا الـ Case مشتغلة كده:

```text id="u8f3qm"
Alert
 ↓
Triage
 ↓
Accept
 ↓
Case
 ↓
Playbook
 ↓
Tasks
 ↓
Investigation
```

لما نخلص التحقيق، نوصل لـ:

**Case Closure**

---

# 1️⃣ إمتى نقدر نقفل الـ Case؟

الكتاب بيقول:

> once tasks are completed, the case can be classified and closed

يعني مجرد ما اخلص التاسكات المطلوبة بناء علي ال playbook

مثلاً عندنا Playbook فيه:

```text id="p4k7zs"
☑ Identify phishing email
☑ Identify victims
☑ Analyze attachment
☑ Check proxy logs
☑ Check endpoint
☑ Contain affected host
```

لو كل الـ Mandatory Tasks خلصت:

```text id="b5x2nc"
All required tasks ✅
        ↓
Classify Case
        ↓
Close Case
```

و كمان احيانا بيكون عندي optional tasks مش لازم التاسكات اللي من النوع ده اعملها كلها لو هي مش مناسبه للحالة

---

# 2️⃣ قبل ما نقفل، بنعمل Classification

دي نقطة مهمه و هي ان the hive او اي ims مش بيقفل ال case و خلاص زي كده مثلا:

```text id="d7m3qa"
Open Case → Do Work → Close
```

لا احنا المفروض قبل ما نقفلها نسال ايه حصل بالظبط؟

مثلا:

**true positive ولا false positive**

---

# 3️⃣ بنحدد Category

يعني ال incident ده نوعه ايه هل هو مثلا:

**phishing , malware**

و هكذا

---

# 4️⃣ بنكتب Closing Note

و دي بنكتب ملخص لل case و اللي عملناه فيها مثلاً:

```text id="x6v2kp"
A phishing email containing a malicious Word document
was delivered to 10 users.

The attachment contained an auto-running macro
that attempted to contact a malicious domain.

The affected users were identified and the malicious
email was removed.

No evidence of successful compromise was found.
```

و مش لازم اكتب معلومات كتير انا اهم حاجه اوضح:

**What happened?**

**What did we find?**

**What did we do?**

**What was the impact?**

---

# 5️⃣ إيه المعلومات اللي لازم تظهر في الـ Closing Note؟

الصفحه دي بتقول انهم 4 حاجات:

### 1-Delivery vector

و هي معناها المهاجم وصل للضحية بتاعتي ازاي؟

مثلاً:

**Phishing Email**

أو:

**Malicious Attachment**

### 2-detection method

و دي معناها احنا اكتشفنا ال incident ازاي؟

مثلاً:

**SIEM Alert**

أو:

**EDR Detection**

أو:

**User Report**

### 3-Impact

و دي حصل ايه بسبب ال attack

مثلاً:

**No compromise**

أو:

**3 users executed malware**

أو:

**1 host compromised**

### 4- Systems Affected

و دي معناها ايه اللي اتاثر مثلاً:

**10 Email Accounts**

**3 Windows Endpoints**

**1 Server**

---

# ⭐ مثال كامل

تخيلي Case:

**Phishing Wave**

التحقيق أثبت:

* 50 users استلموا الـ Email
* 5 فتحوا الـ Attachment
* جهازين شغلوا الـ Malware
* تم عزل الجهازين
* تم حذف الـ Email

ممكن Classification يكون:

```text id="n9c4wh"
Incident Type:
Phishing

Delivery Vector:
Malicious Attachment

Detection:
SIEM + User Report

Impact:
2 compromised endpoints

Affected Systems:
2 Windows endpoints

Classification:
True Positive
```

وبعدها:

**Case → CLOSED ✅**

---

# 🧠 طيب ايه اهمية كل ده؟

تخيل ان عندي اكتر من 10000 case علي مدار السنه لو كل case اتقفلت من غير ما اعملها كل ده انا حرفيا مستفدتش من كل ال cases دي

لكن لو كل Case اتصنفت:

```text id="r3x8mv"
Phishing → 2,000
Malware → 1,500
Credential Attack → 800
Scanning → 600
```

دلوقتي بدأ يظهر عندي **trend**

و كمان حاجه تاني و هي ان ال soc هيقدر يعمل **metric**

و ده مهم عشان اعرف كل ال atacks اللي حصلت و كمان نسبة مرات حدوثها مثلاً بعد سنة:

```text id="q7k2fd"
Phishing        40%
Malware         25%
Credential      15%
Scanning        10%
Other           10%
```

فنسأل:

**إيه أكتر Attack بيحصل عندنا؟**

الإجابة:

**Phishing**

---

# 💰 وهنا الإدارة تدخل

لو الـ SOC قدر يثبت بالأرقام:

> "40% من الـ Incidents عندنا ناتجة عن Phishing."

ممكن يقول للإدارة:

**محتاجين نستثمر في Email Security وAnti-Phishing Controls.**

يعني الـ Incident Data تساعد في:

**Justify Security Spending**

بمعنى:

نستخدم الأرقام عشان نثبت إننا محتاجين فلوس/أدوات/موارد لتحسين الدفاعات

---

# 🧠 و الاهم طبعا Feedback للـ Threat Intelligence

يعني المعلومات اللي طلعناها من ال cases ترجع تاني لفريق ال Threat intelligence

مثلاً اكتشفنا:

```text id="m5v9cz"
100 Phishing Incidents
        ↓
Common Domains
Common Hashes
Common IPs
Common Techniques
Common Malware
```

الـ Threat Intelligence Team يستفيد منها.

مثلاً:

```text id="w4n6ps"
Known malicious domain
        ↓
Add to Threat Intelligence
        ↓
Detection Rule
        ↓
Future Alert
```

يعني الـ SOC بيتعلم من الحوادث السابقة

---

# 🔄 دورة كاملة

وده أهم Concept في السلايد:

```text id="k8q3yb"
        INCIDENT
           ↓
      Investigation
           ↓
      Classification
           ↓
        Closure
           ↓
        Metrics
           ↓
      Find Trends
           ↓
Improve Defenses
           ↓
Threat Intelligence
           ↓
Better Detection
           ↓
Future Incidents
```

يعني **Case Closure** مش معناها "خلصنا منها وخلاص".

الـ Case المقفولة بتتحول إلى **Data مفيدة جدًا للمستقبل**

---

# ⭐ مثال بسيط جدًا

لو خلال 6 شهور عندك:

**100 Incidents**

ولقيتي:

```text id="v2m7xa"
60 Phishing
20 Malware
10 Credential Attacks
10 Other
```

هتعرفي إن:

**Phishing هو أكبر مصدر للمشاكل عندنا.**

بعد كده تسألي:

**ليه الـ Phishing بينجح؟**

تكتشفي إن معظم الـ Phishing بييجي بـ:

**Malicious Word Attachment**

فتبدأي تعملي:

* Email filtering أقوى
* Block certain attachment types
* User awareness training
* Detection rules
* Threat intel entries

وبعد 6 شهور:

**Phishing incidents ↓**

يبقى عندك دليل إن الـ Defense اتحسن

---

# 🎯 الخلاصة

**Case Closure = مش مجرد Close Button.**

قبل ما نقفل الـ Case:

```text id="s9h4kc"
1. Complete mandatory tasks
2. Classify the incident
3. True Positive / False Positive
4. Record relevant categories
5. Write closing summary
6. Record impact + detection + delivery + affected systems
7. Close the Case
```

وبعدها البيانات دي تستخدم في:

```text id="e6q1rz"
Closed Cases
      ↓
Metrics
      ↓
Trends
      ↓
Understand attacks
      ↓
Improve defenses
      ↓
Threat Intelligence feedback
```

---

# 🧠 وأهم جملة:

**كل Case مقفولة هي Data للمستقبل**
