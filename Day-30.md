# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 30 - TheHive's Workflow

الفكرة كلها:

**SIEM يطلع Alert → TheHive يستقبله → Analyst يعمل Triage → لو حقيقي يتحول Case → Case ياخد Playbook/Tasks → نضيف IOCs → Cortex يحللها → Analyst يحقق → Case يتقفل.**

---

## 1️⃣ SIEM → Alert Queue

أول حاجة عندنا:

```text
SIEM
  ↓
Alert
  ↓
TheHive Alert Queue
```

الـ SIEM اكتشف حاجة مشبوهة وطلع Alert.

مثلاً:

```text
🚨 Suspicious PowerShell Activity
Host: WIN-01
User: Ahmed
```

الـ Alert يدخل Alert Queue في TheHive.

### Alert Queue يعني إيه؟

ببساطة:

قائمة الـ Alerts اللي مستنية الـ Analyst يعمل لها Triage.

---

## 2️⃣ Analyst يعمل Triage

الـ Analyst يشوف الـ Alert ويسأل:

**هل ده فعلًا Incident ولا False Positive؟**

عندنا احتمالين:

```text
                 Alert
                   ↓
                Triage
               ↙      ↘
       False Positive   Real Incident
            ↓                 ↓
         Reject              Accept
                              ↓
                             Case
```

### لو False Positive

مثلاً SIEM اعتبر Login مشبوه، لكن اتضح إنه Login طبيعي.

يبقى:

**Reject Alert**

ومش محتاجين نعمل Incident Case كامل.

---

## 3️⃣ لو Alert حقيقي → Case

لو الـ Analyst اقتنع إن الـ Alert يستحق Investigation:

```text
Accepted Alert
      ↓
     Case
```

الـ Case هو الملف اللي هنشتغل فيه على الـ Incident.

مثلاً:

```text
Case #123
Possible Malware Infection
```

---

## 4️⃣ Case Template → Playbook

هنا TheHive ممكن يستخدم:

**Case Template**

والـ Case Template = Playbook

مثلاً Case خاص بـ Malware:

```text
Malware Case Template
        ↓
     Tasks
```

الـ Template ممكن يكون مجهز مسبقًا بمجموعة Tasks.

---

## 5️⃣ Pre-set Tasks = Playbook Steps

مثلاً الـ Malware Playbook فيه:

```text
☐ Identify affected host
☐ Identify user
☐ Analyze process
☐ Check hash
☐ Search SIEM
☐ Contain host
```

كل واحدة من دول:

**Task**

والـ Tasks هي Playbook Steps.

يعني:

**Playbook = الخطة**

و

**Task = خطوة من الخطة**

---

## 6️⃣ Observables = IOCs

أثناء التحقيق، الـ Analyst ممكن يلاقي Indicators.

مثلاً:

* IP Address
* Domain
* URL
* Hash
* Username
* Hostname

TheHive بيسمي الحاجات دي:

**Observables**

والـ Observables ممكن تمثل IOCs مهمة في التحقيق.

مثلاً:

```text
Case
 │
 ├── Task: Analyze malware
 │
 ├── Observable: evil.com
 ├── Observable: 192.168.1.50
 └── Observable: ABC123... (Hash)
```

---

## 7️⃣ Cortex يحلل الـ Observables

وهنا الجزء المهم جدًا.

TheHive عنده Observable:

```text
evil.com
```

ممكن تقولي:

**عايزة أعرف معلومات أكتر عن الـ Domain ده.**

Cortex يدخل:

```text
TheHive
   ↓
Observable
   ↓
Cortex
   ↓
Analyzer
   ↓
Enrichment
```

الـ Analyzer ممكن يبحث عن معلومات إضافية عن الـ Observable.

مثلاً:

```text
evil.com
   ↓
Analyzer
   ↓
Known malicious?
YES

Threat reputation?
High

Related malware?
XYZ
```

فـ Cortex بيضيف:

**Context**

لـ Observable.

---

## 8️⃣ طيب إيه معنى Enrichment؟

دي كلمة مهمة جدًا.

**Enrichment = إضافة معلومات جديدة للبيانات الموجودة.**

عندك:

```text
IP = 10.10.10.10
```

دي معلومة بسيطة.

بعد Enrichment ممكن يبقى عندك:

```text
IP = 10.10.10.10

Reputation = Malicious
Country = X
Previous sightings = 15
Associated malware = XYZ
```

فـ Analyst بقى عنده Context أكبر يساعده ياخد قرار.

---

## 9️⃣ Responders — دي جديدة في السلايد

الـ Analyzer بيعمل:

**Analysis / Information gathering**

لكن الـ Responder بيعمل:

**Action**

يعني بدل ما يجيبلك معلومات، ممكن ينفذ Action تلقائي.

مثلاً:

```text
Malicious IP detected
        ↓
Responder
        ↓
Block IP
```

أو:

```text
Incident detected
      ↓
Responder
      ↓
Send Email
```

أو:

```text
Compromised Host
      ↓
Responder
      ↓
Start data collection
```

---

# 🧠 Analyzer vs Responder

دي مهمة جدًا:

|         | Analyzer          | Responder           |
| ------- | ----------------- | ------------------- |
| وظيفته  | يجمع/يحلل معلومات | ينفذ Action         |
| الهدف   | Enrichment        | Response/Automation |
| مثال    | فحص IP Reputation | Block IP            |
| مثال    | فحص Hash          | Send Email          |
| النتيجة | Context           | Action              |

احفظيها:

**Analyzer = Tell me more.**

**Responder = Do something.**

---

# 🔥 مثال كامل من البداية للنهاية

تخيلي SIEM اكتشف:

**User downloaded suspicious executable.**

### 1. SIEM

```text
SIEM
 ↓
Alert
```

### 2. TheHive

```text
Alert Queue
```

### 3. Triage

الـ Analyst يفحص الـ Alert.

يكتشف إن الموضوع حقيقي.

```text
Accept
 ↓
Case
```

### 4. Case Template

يختار:

**Malware Investigation**

### 5. Tasks

تظهر:

```text
☐ Identify Host
☐ Analyze Process
☐ Check Hash
☐ Search SIEM
☐ Contain Host
```

### 6. Observable

يطلع Hash:

```text
ABC123
```

يتضاف للـ Case:

```text
Observable = ABC123
```

### 7. Cortex

```text
ABC123
 ↓
Cortex
 ↓
Analyzer
```

والنتيجة:

```text
Malicious = YES
Malware = XYZ
```

ده **Enrichment**.

### 8. Response

لو محتاج Containment:

```text
Responder
 ↓
Isolate Host
```

### 9. Finish

الـ Analyst يكمل الـ Tasks ويسجل الـ Worklogs.

لما الـ Mandatory Tasks تخلص:

```text
Tasks Completed
      ↓
Case Closed
```

---

# ⭐ مهم الرسم ده

```text
                    SIEM
                      ↓
                  ALERT QUEUE
                      ↓
                    TRIAGE
                   ↙      ↘
             Reject        Accept
              ↓               ↓
         False Positive      CASE
                               ↓
                     CASE TEMPLATE
                       (PLAYBOOK)
                               ↓
                            TASKS
                               ↓
                     Analyst Investigation
                               ↓
                        OBSERVABLES
                      (IP / Hash / URL...)
                               ↓
                            CORTEX
                           ↙      ↘
                      Analyzer   Responder
                         ↓           ↓
                    Enrichment    Action
                    / Context    / Response
                         ↓           ↓
                         └─────┬─────┘
                               ↓
                         Investigation
                               ↓
                           Close Case
```

---

# 🎯 أهم 5 حاجات في السلايد

**Alert Queue** → الـ Alerts المستنية Triage.

**Case** → الـ Incident المقبول للتحقيق.

**Case Template** → الـ Playbook الجاهز.

**Task** → خطوة من الـ Playbook.

**Observable** → IOC زي IP/Hash/URL.

**Analyzer** → يحلل الـ Observable ويعمل Enrichment.

**Responder** → ينفذ Action تلقائي.

---

## وأهم فرق:

**Cortex مش بس بيبحث عن المعلومات؛ هو Automation Engine، والـ Analyzers للـ Enrichment والـ Responders لتنفيذ Actions.**
