# بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيمِ

# Day 17 — Part 2

---

# How Much Should I Collect?

السؤال هنا:

> هل كل ما أجمع Logs أكثر، الـ Detection هيتحسن أكثر؟

الإجابة:

**مش بالضرورة.**

ودي من الأفكار المهمة في الجزء ده.

المطلوب مش إننا نجمع كل حاجة ممكنة، لكن نجمع الأشياء اللي تعتبر:

> **Security-Relevant**

يعني:

```text
More Data
   ≠
Better Detection
```

---

# Collecting Lots of Events: Is It Great for Detection?

لما أجمع كل الـ Logs، منطقي جدًا أفكر:

> "لما يحصل Attack أكيد هلاقي Evidence."

والفكرة دي جزء منها صح.

وجود Data أكثر ممكن يساعدنا في:

* Detection
* Investigation

لكن المشكلة إن الكمية الكبيرة جدًا من البيانات ممكن تعمل مشاكل أكبر.

والكتاب بيسأل:

> **Collecting lots of events is great for detection...or is it?**

يعني هل فعلًا جمع كمية ضخمة من الـ Events دايمًا شيء جيد؟

الإجابة: **لا.**

---

# 1. More Volume = More Cost

> **In most SIEMs, more volume = more cost**

الموضوع أكبر بكثير لأن بعض الـ SIEMs بتتسعر بناءً على كمية البيانات اللي بتدخلها أو بيتم الاحتفاظ بها.

فكل ما زادت كمية البيانات:

```text
More Data Volume
      ↓
   More Cost
```

---

# 2. Searching More Data Takes Longer

لو عندي Data كبيرة ومعظمها ملهاش علاقة بالـ Investigation، عملية البحث ممكن تبقى:

* أبطأ
* أكثر استهلاكًا للموارد

وده مهم جدًا للـ SOC لأن وقت الـ Incident بنكون عايزين البحث يكون سريع.

```text
More Data
    ↓
More Data to Search
    ↓
Slower Searches
```

---

# 3. Signal vs Noise

دي من أهم النقاط في الجزء ده.

الكتاب بيستخدم تشبيه:

> **Finding the needle in the haystack**

يعني إيجاد إبرة وسط كومة قش.

### Signal

**Signal** = المعلومة المهمة اللي تشير لحاجة **Suspicious أو Security-Relevant**.

### Noise

**Noise** = كمية البيانات الموجودة لكن مش مفيدة للتحليل الأمني.

فلو عندي كمية ضخمة جدًا من الـ Noise، الوصول للـ Signal بيبقى أصعب.

```text
More Noise
    ↓
Harder to Find Signal
    ↓
Harder / Slower Detection
```

---

# هل معنى كده إني أحذف الـ Logs؟

**مش لازم.**

والكتاب مش بيقول:

> "اجمع Logs قليلة."

الفكرة هي:

> اجمع الـ Logs اللي ليها علاقة بالمعلومات الأمنية المهمة.

والسؤال اللي لازم أسأله عن أي Log:

> **هل الـ Log ده ممكن يساعدني في Detection و Investigation؟**

لو الإجابة:

**نعم**

يبقى يستحق إني أجمعه.

ولو ملوش قيمة أمنية واضحة، ممكن أقلل منه أو مبعتوش للـ SIEM.

---

# What Should I Collect?

المعيار الأساسي:

> **Anything that helps you detect a security-related issue**

مثلاً:

### Authentication Logs

ممكن تساعد في اكتشاف:

* Brute Force
* Account Compromise
* Privilege Abuse

### Process Creation

ممكن تساعد في اكتشاف:

* Malware
* Suspicious Execution

### Network Connection Logs

ممكن تساعد في اكتشاف:

* Malicious IP
* Suspicious Network Activity

الفكرة مش إن كل Log لازم يكون Malicious.

الفكرة إن الـ Log يكون عنده **Security Value**.

---

# Most Teams Have Both Problems

الكتاب بيقول حاجة مهمة:

> **Most teams both collect too much that they need and don't collect enough of what they do need.**

يعني المشكلة مش مشكلة كمية البيانات فقط.

المشكلة الحقيقية:

> **هل البيانات اللي عندي هي البيانات الصح؟**

ممكن يكون عندي:

```text
Huge Amount of Logs
        ↓
     لكن
        ↓
Missing Important Evidence
```

وفي نفس الوقت ممكن يكون عندي Logs كتير جدًا ملهاش قيمة.

إذن:

```text
Too Much Unnecessary Data
        +
Too Little Important Data
        ↓
Bad Visibility
```

---

# Logging Strategy بتتغير مع الوقت

الكتاب بيقول:

> **This is an ever-moving target.**

يعني الـ **Security Logging** مش حاجة تعملها مرة وخلاص.

لازم الـ Logging Strategy تتطور باستمرار.

ليه؟

---

## Attacks بتتغير

الـ Attackers بيستخدموا Techniques جديدة.

```text
New Attacks
    ↓
New Techniques
    ↓
New Evidence
```

---

## Logging Capabilities بتتغير

الـ Tools والـ Operating Systems والـ Cloud Services بتضيف Logs جديدة.

يعني الـ Visibility اللي كانت متاحة عندي قبل كده ممكن تتغير مع الوقت.

---

## Detection Requirements بتتغير

الـ SOC ممكن يكتشف إن Log معين بقى مهم جدًا بسبب **Attack Scenario جديد**.

فلازم باستمرار نسأل:

> **هل الـ Logs اللي بجمعها حاليًا مازالت كافية؟**

---

# Threat Intelligence

وهنا بيظهر دور **Threat Intelligence**.

تحديد الـ Logs اللي نحتاجها يتطلب معرفة:

1. **How logging works**
2. **What logs are available**
3. **What attacks we might encounter**
4. **What evidence those attacks produce**

والنقطة الرابعة مرتبطة جدًا بالـ **Threat Intelligence**.

مثلاً لو Threat Intelligence قالت:

> Attack معين بيستخدم PowerShell لتنفيذ Payload.

يبقى نسأل:

> هل عندي Logs تقدر توريني PowerShell Execution؟

لو لأ:

```text
Attack Technique
      ↓
Expected Evidence
      ↓
No Required Logs
      ↓
Visibility Gap
```

عندي هنا:

> **Visibility Gap**

---

# العلاقة بين Attack و Evidence

دي نقطة مهمة جدًا في الـ **Blue Team**.

الـ Attack بيترك وراءه:

> **Artifacts / Evidence**

مثلاً:

```text
Attack
  ↓
Creates Process
  ↓
Network Connection
  ↓
File Creation
  ↓
Authentication Activity
```

إذن لازم تكون عندك Logs قادرة على تسجيل الحاجات دي.

وعشان كده العلاقة المهمة هي:

```text
Threat Intelligence
        ↓
Attack Techniques
        ↓
Expected Evidence
        ↓
Required Logs
```

---

# مثال كامل

تخيلي عندك Threat Intelligence عن Attack بيعمل:

```text
Initial Access
      ↓
PowerShell Execution
      ↓
C2 Communication
      ↓
Credential Theft
```

نبدأ نفكر في الـ Logs المطلوبة لكل مرحلة.

---

## Initial Access

ممكن أحتاج:

```text
Authentication Logs
VPN Logs
Firewall Logs
```

---

## PowerShell

أحتاج:

```text
Process Creation
PowerShell Logs
```

---

## C2

أحتاج:

```text
DNS Logs
Network Connection Logs
Proxy Logs
```

---

## Credential Theft

ممكن أحتاج:

```text
Authentication Events
Endpoint Security Logs
```

كده أنا مش بجمع الـ Logs عشوائيًا.

أنا بجمعها لأن:

> **عندي Use Case أمني واضح.**

---

# ماذا أفعل لو عندي Log مش مفيد؟

الكتاب بيقول:

> **If you can show that a subset of them are providing no value, don't be shy cutting them out!**

يعني لو أثبتنا إن نوع معين من الـ Events:

* ملوش قيمة في الـ Detection.
* ملوش قيمة في الـ Investigation.
* بيستهلك حجم كبير.
* بيعمل Noise.

ممكن نقلل منه أو نستبعده من الـ SIEM.

لكن ده لازم يكون:

> **قرار مبني على تحليل**

مش مجرد:

> "الـ Logs كتير، نلغيهم."

---

# Don't Blindly Collect Everything

في بداية الـ SOC ممكن التفكير يكون:

> "خليني أجمع كل حاجة عشان أبقى Safe."

لكن مع الوقت هتكتشفي إن:

```text
Everything
    ≠
Useful
```

والـ SOC الناضج بيبني:

> **Tactical Collection Strategy**

يعني:

> أجمع البيانات اللي عندها قيمة أمنية حقيقية.

---

# ربط الجزء ده بالجزء السابق

إحنا كنا قلنا:

```text
EVENT
  ↓
SIEM
  ↓
Processing
  ↓
ALERT
  ↓
TRIAGE
  ↓
INCIDENT
```

دلوقتي لازم نقف قبل ما نحط الـ Events في الـ SIEM ونسأل:

> **هل أنا أصلًا محتاج أجمع الـ Event ده؟**

فتبقى الصورة:

```text
              Security Environment
                       ↓
                 Events Generated
                       ↓
             ┌────────────────────┐
             │ Security-Relevant? │
             └─────────┬──────────┘
                       ↓
                      YES
                       ↓
                 Collect Logs
                       ↓
                     SIEM
                       ↓
               Search / Correlation
                       ↓
                   Detection
                       ↓
                    ALERT
                       ↓
                    Triage
                       ↓
                   INCIDENT
```

---

# 🎯 الخلاصة

احفظي الفكرة دي:

> **The goal is not to collect everything. The goal is to collect what helps us detect and investigate security issues.**

يعني:

### ❌ مش:

```text
More Logs = Better Security
```

### ✅ لكن:

```text
More Relevant Logs = Better Visibility
```

---

# أهم 3 مشاكل من جمع كل حاجة

```text
More Volume
     ↓
 More Cost
```

```text
More Data
     ↓
Slower Searches
```

```text
More Noise
     ↓
Harder Detection
```

---

# وفي المقابل: جمع Logs أقل من اللازم

لو قللنا الـ Logs زيادة عن اللزوم:

```text
Too Little Data
      ↓
Missing Evidence
      ↓
Can't Detect / Investigate
```

فإحنا بندور على **التوازن**:

> **Collect enough security-relevant data to detect and investigate attacks, without drowning the SIEM in unnecessary noise.**

وده سبب إن الـ **Logging Strategy** تعتبر عملية مستمرة، وبتتطور مع:

```text
Threat Landscape
       +
Detection Needs
       +
Available Logging Capabilities
```

---

# Final Concept

الصورة الكاملة:

```text
                SECURITY ENVIRONMENT
                        ↓
                  EVENTS GENERATED
                        ↓
              Security-Relevant?
                    ↙       ↘
                  NO         YES
                  ↓           ↓
               Noise     Collect Logs
                              ↓
                             SIEM
                              ↓
                     Processing / Search
                              ↓
                         Correlation
                              ↓
                         Detection
                              ↓
                           ALERT
                              ↓
                           TRIAGE
                              ↓
                    Confirmed Incident
```

> **Collect the right data, not just more data.**

<div align="center">

## End of Day 17

</div>
