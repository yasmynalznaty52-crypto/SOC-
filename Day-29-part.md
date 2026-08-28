# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 29 Part2 - TheHive — Incident Management System

## TheHive — Incident Management System

the hive it is an open-source incident management system و الكتاب بيستخدمه كاداة للشرح العملي

و هو المكان اللي ال soc analyst بيستلم فيه ال cases و يحقق فيها و يسجل اللي عمله و يربطه بال IOCs و في النهاية يقفل ال case

---

## 1- Incident are organized by case

هنا بيقول ان ال the hive بيحط ال incident في case و دي اللي بيكون فيها كل المعلومات المتعلقه بال incident

مثلاً جالك Alert:

```text
🚨 Suspicious PowerShell Activity
Host: PC-01
User: Ahmed
```

ممكن يتحول إلى:

```text
Case #123
Suspicious PowerShell Activity
```

و بيكون جواها كل التفاصيل الخاصه بالتحقيق

---

## 2- Case Template = Playbook

هنا بيقول ان ال case template هو ال playbook الخاص ب the hive

مثلاً عندك:

```text
Malware Case Template

ممكن يحتوي:

Case Template
      ↓
Tasks
├── Identify Host
├── Identify User
├── Analyze Process
├── Check Hash
├── Search SIEM
└── Containment
```

و ده بدل ما ال analyst يبدأ من الصفر الplay book بيديله الخطوات اللي مطلوبة

---

## 3- Tasks = Playbook Steps

هنا الكتاب بيقول ان كل case انا بلاقيها بتكون فيها خطوات للتحقيق

مثلاً:

```text
Case: Malware Infection

Tasks:
☐ Identify affected host
☐ Check EDR
☐ Analyze hash
☐ Search SIEM
☐ Contain host
```

و كل خطوة هنا تمثل task

**task = actions that analyst needs to complete**

---

## 4- Worklog = Notes

هنا بيقول دلوقتي ال analyst عمل تاسك مثلا check hash و طلع ان ال hash ده malicious و بقي محتاج انه يسجل هو عمل ايه و طلع ايه هنا يجي دور ال worklog و هو عبارة عن notes المرتبطه بال task نفسها

مثلاً:

```text
Task:
Check Hash

Worklog:
Hash was checked against threat intelligence.
It was identified as malicious.
```

و ده مهم عشان يبقي عندنا evidence of what analyst did

---

## 5- Observables = IOCs

و ده من اهم مصلحات the hive و هو عبار عن piece of data or indicator المتعلقه بال incident زي مثلا:

* ip address
* domain name
* hash
* url
* email address
* filename

مثلاً Case فيه:

```text
Malicious Domain:
evil-example.com

IP:
185.x.x.x

Hash:
abc123...
```

الحاجات دي تتحط كـ:

**Observables**

و الحاجات دي سميناها كده لانها عبارة عن الحاجات ال observed اثناء التحقيق بتاعي

مثلاً:

> "الـ Email كان فيه URL معين."

فالـ URL ده Observable.

---

## 6- Observables can be enriched

و ده معناه انو عندي Observable، وعايز أعرف عنه معلومات إضافية.

مثلاً عندي:

```text
Observable:
192.168.x.x
```

ممكن أسأل Threat Intelligence:

**هل الـ IP ده معروف إنه Malicious؟**

أو عندي:

```text
Hash:
ABC123
```

أسأل:

**هل الـ Hash ده مرتبط بـ Malware؟**

---

## 7- Cortex + Analyzer

هنا النقطه دي معناها ان ال the hive ممكن يتكامل مع the cortex و ده بيوفرله analyzer و ده عبارة عن اداة بتاخد ال observable و تعمل عليه enrichment / analysis

مثلاً:

```text
Observable
    ↓
Cortex
    ↓
Analyzer
    ↓
Additional Information
```

مثال:

```text
Hash
 ↓
Analyzer
 ↓
Threat Intelligence Lookup
 ↓
Malicious = True
```

فبدل Analyst ما يعمل كل البحث يدويًا، الأدوات ممكن تساعده.

---

# خلينا نجمع كل حاجة في سيناريو واحد

تخيلي وصل Alert:

**EDR detected suspicious executable**

## Step 1 — Alert

```text
EDR
 ↓
Alert
```

## Step 2 — Case

TheHive يعمل:

```text
Case #500
Suspicious Executable
```

## Step 3 — Case Template

الـ Case يستخدم Malware Template:

```text
Malware Investigation
```

## Step 4 — Tasks

TheHive يجهز:

```text
☐ Identify Host
☐ Identify User
☐ Analyze Process
☐ Check Hash
☐ Search SIEM
☐ Containment
```

## Step 5 — Analyst

الـ Analyst يبدأ ينفذ الـ Tasks.

مثلاً:

```text
Check Hash
```

## Step 6 — Worklog

يسجل:

```text
Hash checked against TI.
Hash identified as malicious.
```

## Step 7 — Observable

الـ Hash يتحفظ في الـ Case كـ:

```text
Observable
```

## Step 8 — Enrichment

TheHive يرسل الـ Observable إلى Cortex:

```text
Hash
 ↓
Cortex
 ↓
Analyzer
 ↓
Threat Intelligence Result
```

ويطلع:

```text
Malware Family: XYZ
Known Malicious: YES
```

## Step 9 — Investigation

الـ Analyst يستخدم المعلومات دي عشان يقرر:

**هل الجهاز Compromised فعلًا؟**

ولو نعم:

**نعمل Containment / Incident Response.**

## Step 10 — Close

بعد ما كل الـ Mandatory Tasks تخلص:

```text
Tasks Completed
      ↓
Case Closed
```

---

# 🧠 افهم TheHive بالشكل ده

```text
                 THEHIVE
                    │
                  CASE
                    │
            Case Template
               (Playbook)
                    │
                  TASKS
            ┌───────┼───────┐
            ↓       ↓       ↓
          Task    Task     Task
            │
         Worklog
          (Notes)

Case
 │
 └── Observables
       │
       ↓
     Cortex
       │
       ↓
    Analyzers
       │
       ↓
   Enrichment
```

---

# ⭐ أهم المصطلحات في السلايد

| TheHive       | معناها                                  |
| ------------- | --------------------------------------- |
| Case          | الـ Incident/Ticket اللي بنحقق فيه      |
| Case Template | Playbook جاهز                           |
| Task          | خطوة من خطوات الـ Playbook              |
| Worklog       | Notes عن الشغل اللي اتعمل في الـ Task   |
| Observable    | IOC / Indicator مرتبط بالـ Case         |
| Cortex        | محرك بيساعد في Automation & Enrichment  |
| Analyzer      | أداة بتحلل الـ Observable وتجيب Context |

---

# 🎯 وأهم Workflow

```text
Alert
  ↓
Case
  ↓
Case Template
  ↓
Tasks
  ↓
Worklogs
  ↓
Observables
  ↓
Enrichment
  ↓
Investigation
  ↓
Close Case
```
