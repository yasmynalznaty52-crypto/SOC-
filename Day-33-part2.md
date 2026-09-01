# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 33 - Part 2 - Incident Management Systems Summary

الـ IMS هو المكان اللي الـ SOC بيستخدمه عشان:

يستقبل الـ Alerts → يحولها لـ Cases → ينظم التحقيق → يسجل اللي حصل → يقفل الـ Case → يطلع Metrics.

ومن أمثلته TheHive.

---

# 1️⃣ الـ IMS من أهم أدوات الـ SOC

السلايد بتقول:

> Your IMS is one of the most important pieces of software!

ليه؟

لأن الـ Analyst هيستخدمه طول الوقت.

مش أداة بتفتحيها مرة في الشهر.

الـ Analyst ممكن يقضي معظم شغله في:

```text
Alert
 ↓
Case
 ↓
Tasks
 ↓
Investigation
 ↓
Notes
 ↓
Classification
 ↓
Closure
```

فلو الـ IMS سيئ أو معقد، هتتعبي جدًا في الشغل اليومي.

---

# 2️⃣ Test the Interface

دي نصيحة SANS قوية جدًا:

> Test the interface, or you will be miserable! 😂

يعني قبل ما الشركة تختار IMS:

❌ متقولش:

"ده مشهور يبقى أكيد كويس."

❌ أو:

"ده غالي يبقى أحسن."

لا.

لازم الـ Analysts يجربوه فعليًا.

لأن ممكن تكتشفي إن:

* محتاج Clicks كتير
* البحث سيئ
* إضافة Notes صعبة
* Assignment معقد
* Workflow مش مناسب
* مفيش Integrations كويسة

والـ Analyst هيستخدم الأداة كل يوم.

---

# 3️⃣ Cases should be created from validated alerts

دي مرتبطة بالـ Triage اللي أخدناه.

مش كل Event:

```text
Event → Case ❌
```

ومش كل Alert:

```text
Alert → Case ❌
```

الأصح:

```text
Event
 ↓
Detection
 ↓
Alert
 ↓
Triage / Validation
 ↓
Is it legitimate?
 ↓
Yes / Suspicious
 ↓
Case
```

يعني الـ Case المفروض تتعمل من Alert تم التحقق منه أو قبوله للتحقيق، مش أي Alert عشوائي.

مثلاً:

```text
SIEM Alert
"Suspicious PowerShell"

        ↓

Analyst Triage

        ↓

Looks malicious

        ↓

Create Case
```

لكن لو:

```text
Alert
 ↓
False Positive
 ↓
Reject
```

مش محتاج Case كاملة.

---

# 4️⃣ Context from alert should be parsed into fields

دي مهمة جدًا.

لما الـ Alert يدخل الـ IMS، المعلومات الموجودة فيه المفروض تنتقل تلقائيًا للـ Case.

مثلاً الـ Alert فيه:

```text
Source IP: 10.10.10.50
Destination IP: 8.8.8.8
User: Ahmed
Hostname: PC-01
Hash: ABC123
URL: evil.com
```

بدل ما الـ Analyst يقعد يعمل:

**Copy → Paste → Copy → Paste 😭**

الـ IMS المفروض يستقبل البيانات في Fields منظمة:

```text
Case
├── Source IP
├── Destination IP
├── User
├── Hostname
├── Hash
└── URL
```

وده اسمه:

**Parsing**

يعني تحويل البيانات الخام إلى Fields مفهومة وقابلة للاستخدام.

---

# 5️⃣ Playbooks guide you through tasks

الـ Playbook هو:

مجموعة خطوات محددة للتحقيق في نوع معين من الـ Incident.

مثلاً:

**Phishing Playbook**

```text
1. Analyze Email
2. Identify Recipients
3. Analyze Attachment
4. Check Proxy Logs
5. Check Endpoint
6. Contain if needed
```

فالـ Analyst مش لازم كل مرة يفكر:

"أعمل إيه دلوقتي؟"

الـ Playbook بيقوده.

---

# 6️⃣ Tasks are assigned based on pre-made playbooks

الـ Playbook بيتحول إلى Tasks.

مثلاً:

```text
Phishing Playbook
       ↓
Tasks
       ↓
┌─────────────────────┐
│ Analyze Email       │
│ Analyze Attachment  │
│ Check Proxy         │
│ Check Endpoint      │
└─────────────────────┘
```

وفي TheHive ممكن:

```text
Task 1 → Analyst 1
Task 2 → Analyst 1
Task 3 → Analyst 2
Task 4 → Analyst 2
```

فده يرجعنا لموضوع **Task Assignment** اللي شرحناه.

---

# 7️⃣ Observables entered as discovered

أثناء التحقيق هتكتشفي حاجات مهمة:

**IP**

**Domain**

**URL**

**Hash**

**Email**

**Username**

**Hostname**

دي بنسميها:

**Observables**

فتضيفيها للـ Case.

مثلاً:

```text
Case
 ↓
Observables
 ├── 192.168.1.50
 ├── evil.com
 └── SHA256...
```

والأفضل إن الـ Observables تتضاف automatically لو الـ Tools تقدر تعمل ده.

مثلاً:

```text
SIEM
 ↓
Alert
 ↓
IMS
 ↓
Observable automatically extracted
```

بدل ما الـ Analyst يدخل كل حاجة يدويًا.

---

# 8️⃣ Close with categorizations for metrics

لما نخلص التحقيق:

```text
Tasks Completed
       ↓
Classification
       ↓
Close Case
```

مثلاً:

```text
Incident Type: Phishing
Delivery Vector: Attachment
Impact: 2 compromised hosts
Detection: SIEM
Result: True Positive
```

ليه بنعمل Classification؟

مش عشان نملأ بيانات وخلاص.

لكن عشان نطلع **Metrics**.

---

# 9️⃣ Use metrics for improvement

دي أهم نقطة في السلايد كلها تقريبًا.

بعد ما نقفل آلاف الـ Cases، نقدر نحلل البيانات.

مثلاً:

```text
1000 Incidents
      ↓
400 Phishing
250 Malware
150 Credential Attacks
100 Scanning
100 Other
```

نكتشف:

**Phishing هو أكبر مشكلة.**

فنبدأ نحسن دفاعات الـ Email.

---

# 🔄 الصورة الكبيرة كلها

لو جمعنا كل اللي درسناه:

```text
             EVENTS
                ↓
          Security Tools
                ↓
             ALERTS
                ↓
         SIEM / Triage
                ↓
      Validate / Investigate
                ↓
       ┌────────────────┐
       │   IMS / Case   │
       └────────────────┘
                ↓
           Playbook
                ↓
             Tasks
          ↙          ↘
   Analyst 1       Analyst 2
          ↘          ↙
           Investigation
                ↓
          Observables
                ↓
       Enrichment / Context
                ↓
       Complete Tasks
                ↓
         Classification
                ↓
          Close Case
                ↓
             Metrics
                ↓
       Improve SOC / Defense
                ↓
        Better Detection
```

---

# 🧠 ملخص

| المفهوم        | وظيفته                            |
| -------------- | --------------------------------- |
| Alert          | تنبيه بوجود نشاط يستحق النظر      |
| Triage         | نتحقق هل الـ Alert يستحق التحقيق  |
| IMS            | المكان اللي ندير فيه الـ Incident |
| Case           | الحادثة اللي بنحقق فيها           |
| Playbook       | خطة التحقيق                       |
| Task           | خطوة من خطوات الـ Playbook        |
| Observable     | معلومة ظهرت أثناء التحقيق         |
| IOC            | Observable نعتبره مؤشر اختراق     |
| Worklog        | ملاحظات Analyst أثناء تنفيذ Task  |
| Classification | وصف وتصنيف الـ Incident           |
| Closure        | إغلاق الـ Case بعد إتمام المطلوب  |
| Metrics        | أرقام نستفيد منها لتحسين الـ SOC  |

---

# 🎯 الـ Workflow

```text
Validated Alert
      ↓
     Case
      ↓
   Playbook
      ↓
    Tasks
      ↓
Observables + Investigation
      ↓
Classification
      ↓
Closure → Metrics → Improvement
```

والفكرة الأساسية جدًا:

**الـ IMS مش مجرد مكان بنقفل فيه Tickets؛ هو النظام اللي بينظم رحلة الـ Incident كاملة، وفي النهاية البيانات اللي بنجمعها من الـ Cases المقفولة بتساعد الـ SOC يعرف هو شغال كويس فين، وإيه اللي محتاج يتحسن**
