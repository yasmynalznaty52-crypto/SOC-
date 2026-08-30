# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 31 - Part 2 - TheHive: Example Case Template

تخيل معايا ان عندنا incident و نوعه **Phishing wave-attachmens**

يعني حصل عليا حملة phishing و الاميلات دي كمان فيها malicious attachment زي كده مثلا:

```text
Multiple employees
        ↓
Receive phishing emails
        ↓
Malicious attachment
        ↓
Potential compromise
```

---

# 1️⃣ Case Template

لما يحصل عندي Case جديدة من النوع ده مش بنبدا من الصفر لان عندي template متخصص لننوع ده اسمه **phishing wave-attachment attack**

و ده معمول مسبقا وظيفته هي انه لما يحصل عندي incident من النوع ده:

اقول ايه الحاجات اللي مفروض احقق فيها؟

و ايه ال Responce action اللي انا محتاج اعمله في الحاله دي؟

---

# 2️⃣ Template بيعمل إيه؟

و ظيفته هنا انه بيقسم ال cases ل tasks جاهزة مثلاً ممكن تلاقي:

```text
Phishing Wave – attachments

Tasks:
☐ Identify malicious attachment
☐ Identify affected users
☐ Check email logs
☐ Check for execution
☐ Search endpoints
☐ Check proxy logs
☐ Contain affected hosts
```

إذن:

**Case Template → Pre-populated Tasks**

وده بالضبط معنى:

> "This list of tasks was prepopulated by the case template."

---

# 3️⃣ ليه الـ Tasks دي موجودة؟

مبدئيا التاسكات دب مش معمولة بشكل عشوائي بالعكس دي كلها مبنية علي **investigative questions** يعني أسئلة انا لازم اجاوب عليها زي مثلا:

* مين استلم الـ Email؟
* هل فتح الـ Attachment؟
* هل الـ Attachment اتنفذ؟
* هل حصل Malware Infection؟

وكمان:

### Response Actions

يعني:

**لو اتأكدنا إن فيه Compromise، نعمل إيه؟**

مثلاً:

**نعمل Containment للجهاز**

---

# 4️⃣ Task Groups

هنا دي نقطة مهمه و بيقول انه ال tasks اللي عندي دي متقسمه ل task groups و ال groups دي مرتبطة بمراحل من ال **Cyber Kill Chain**

مثلاً:

```text
Delivery
Exploit
Install
...
```

فبدل ما يبقى عندك 20 Task مرميين جنب بعض، بيتنظموا حسب المرحلة اللي بيغطوها.

مثلاً:

```text
DELIVERY
├── Identify phishing email
├── Identify recipients
└── Analyze attachment

EXPLOIT
├── Check if attachment was opened
└── Check exploitation activity

INSTALL
├── Check for malware installation
└── Check endpoint activity
```

طيب ليه **Cyber Kill Chain** هنا؟

لأننا بنحاول نفهم:

**المهاجم وصل لفين في الـ Attack؟**

مثلاً لو لقينا:

```text
Delivery ✅
Exploit ❌
Install ❌
```

ده معناه:

الـ Phishing Email وصل للضحية، لكن مفيش دليل إن الـ Attack كمل للمرحلة التالية.

لكن لو:

```text
Delivery ✅
Exploit ✅
Install ✅
```

فالموضوع أخطر

---

# 5️⃣ كل Task لها Analyst

و ده طبعا مرتبط بالجزء اللي فات بتاع **Case VS Task management**

في TheHive ممكن تلاقي:

```text
Task 1 → Analyst 1
Task 2 → Analyst 1
Task 3 → Analyst 2
Task 4 → Analyst 2
```

يعني مش لازم نفس الشخص يعمل كل حاجة.

مثلاً:

```text
Delivery
├── Analyze Email       → Analyst 1
├── Identify Recipients → Analyst 1

Exploit
├── Check Execution     → Analyst 2

Install
├── Endpoint Analysis   → Analyst 2
```

---

# 6️⃣ Analyst يضغط Start

لما الـ Task تتعين لـ Analyst معين، يقدر يبدأ الشغل عليها.

مثلاً:

```text
Task:
Analyze malicious attachment

Assigned to:
Analyst 1

        ↓

      START
```

لما يدوس Start، يبدأ فعليًا تنفيذ الـ Task.

وبعدها ممكن يسجل في الـ Worklog:

```text
Attachment analyzed.

File hash:
ABC123...

File identified as malicious
```

---

# 🔥 خلينا نعمل سيناريو كامل

وصلت 50 رسالة Phishing للموظفين.

وفيها ملف:

```text
invoice.pdf.exe
```

الـ SOC عمل Case:

**Phishing Wave – attachments**

واستخدم الـ Case Template.

TheHive تلقائيًا حط Tasks:

```text
DELIVERY
├── Identify recipients
├── Analyze phishing email
└── Analyze attachment

EXPLOIT
├── Check who opened attachment
└── Search suspicious execution

INSTALL
├── Check for malware installation
└── Identify compromised hosts
```

### Analyst 1

يشتغل على:

```text
Identify recipients
Analyze email
Analyze attachment
```

ويكتشف:

**20 employees received it.**

### Analyst 2

يشتغل على:

```text
Check suspicious execution
Identify compromised hosts
```

ويكتشف:

**3 machines executed the malicious file.**

### Analyst 1 يشوف النتيجة

يقدر يفتح الـ Case ويشوف الـ Worklogs الخاصة بـ Analyst 2.

وبالتالي الاتنين شغالين على نفس الـ Case في نفس الوقت

---

# ⭐ معنى الجملة المهمة في السلايد

> "The case template was designed to reflect common investigative questions as well as response actions"

يعني الـ Template مش مجرد قائمة Tasks.

هو معمول بناءً على:

**What do we need to know?**

و

**What do we need to do?**

---

# 🧠 فهم الجزء ده كالتالي

```text
Case Template
      ↓
   Playbook
      ↓
 Task Groups
      ↓
    Tasks
      ↓
Assign Analysts
      ↓
   Start Task
      ↓
   Worklog
      ↓
Complete Task
```

والـ Task Groups ممكن تكون مرتبطة بـ:

```text
Cyber Kill Chain
     ↓
Delivery
Exploit
Install
...
```

---

# 🎯 الخلاصة

السلايد بتقول إنك لما تعملي Case جديد في TheHive باستخدام Template جاهز، TheHive مش بيسيب الـ Analyst يبدأ من الصفر.

الـ Template بيعمل:

**Case → Tasks جاهزة → Task Groups → Assignment → Investigation**

وكل Task ممكن تتعين لـ Analyst مختلف.

وده يخلي الـ Investigation:

**Standardized + Organized + Collaborative**

يعني كل Analyst يعرف هو مطلوب منه يعمل إيه بالضبط، والـ SOC يضمن إن الخطوات المهمة مش هتتنسى.
