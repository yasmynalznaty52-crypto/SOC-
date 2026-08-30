# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 31 - Case Assignment vs Task Assignment

في بعض ال incident management systems لما ال analyst ياخد case لازم ياخد كل الtasks اللي تخص ال case دي

لكن the hive مرن فممكن ال analyst ياخد ال case و الtasks تتوزع علي اكثر من analyst

---

## 1️⃣ Case Assignment

يعني:

```text id="bq1v4a"
Case #100
   ↓
Analyst 1
```

الـ Case كلها مسؤولة من Analyst 1.

مثلاً:

```text id="qv7n2k"
Case: Malware Investigation
Assigned to: Analyst 1
```

---

## 2️⃣ Task Assignment

ده بقي عنده ميزة قوية ان شكل ال case من جوه بيكون كده:

```text id="j4w9rc"
Case
 │
 ├── Task 1
 ├── Task 2
 ├── Task 3
 ├── Task 4
 ├── Task 5
 └── Task 6
```

كمان ممكن اوزعهم بالشكل ده:

```text id="0d5xkz"
Task 1 → Analyst 1
Task 2 → Analyst 1
Task 3 → Analyst 1
Task 4 → Analyst 1
Task 5 → Analyst 2
Task 6 → Analyst 2
```

و ده معناه اكتر من شخص علي نفس ال case في نفس الوقت

و ده مفيد لان لو مثلا عندي case صعبه زي مثلا malware investigation و بالشكل ده:

```text id="l7k3ps"
Task 1 → Identify Host
Task 2 → Check SIEM
Task 3 → Analyze Hash
Task 4 → Analyze Malware
Task 5 → Memory Analysis
Task 6 → Containment
```

ممكن لو عندي analyst جدد ميعرفش يعمل كل حاجه ممكن يعمل حاجات زي كده مثلا:

```text id="lq4f1d"
Identify Host
Check SIEM
Analyze Hash
```

لكن يجي عند تاسك معينه زي Memory Analysis و يلاقي نفسه مش فاهمه فبدل ما ال case كلها تتعطل و توقف بسببه يعمل:

```text id="d7q0vy"
Task: Memory Analysis
          ↓
     Senior Analyst
```

والـ Senior يكملها

### Analyst 1 + Analyst 2

مثلاً:

**Analyst 1 — Junior/New Analyst**

ياخد الـ Case:

```text id="4gq6jv"
Case: Malware
```

ويبدأ:

```text id="9r1b5e"
Task 1 ✅
Task 2 ✅
Task 3 ✅
Task 4 ❓
```

Task 4 صعبة.

**Analyst 2 — Senior**

ياخد Task 4 فقط:

```text id="4n8y9m"
Task 4
Memory Analysis
↓
Senior Analyst
↓
Completed
```

وبعدين يكتب في الـ Worklog إيه اللي عمله

---

## 3️⃣ Analyst 1 يقرأ الـ Worklog

دي نقطه حلو اوي في the hive و هي ان الجينيور Analyst1 ممكن يقرا ال worklog بتاعت السينيور Analyst2 اللي حل فيها التاسك زي مثلا الـ Senior كتب:

**Worklog:**

```text id="m7k2zq"
Memory dump was analyzed.
Suspicious process was identified.
The process was associated with the malicious hash
```

و كده الجينيور اتعلم من ال work log ده و المرة الجايه ممكن هو اللي ينفذ التاسك دي

و ده بيعمل **Learing over time**

الكتاب بيقول:

**Learns task over time**

يعني الجنيور مع الوقت بيتطور و يكسب خبرة كمان

في البداية:

```text id="s9g6hz"
Junior
 ↓
Easy Tasks
```

بعد فترة:

```text id="1c6w8v"
Junior
 ↓
Easy + Medium Tasks
```

وبعد وقت:

```text id="f3a2pl"
Experienced Analyst
 ↓
Complex Tasks
```

ف the hive مش بس بيساعد اني اوزع التاسكات علي ال analysts و ال SOC team لا هو كمان بيساعد في تطور مهارات الجينيور مع الوقت

---

## 4️⃣ Better load balancing

و ده معناه توزيع الشغل علي التيم يعني بدل ما يكون عندي analyst واخد تاسكات كتير زي مثلا 10 تاسكات و analyst تاني فاضي اوزعها عليهم هما الاتنين و كده هخلص الشغل اسرع

---

## 5️⃣ Shift Changeover

دي كمان نقطة مهمة جدًا في الـ SOC.

افترضي إن:

```text id="y2lq8a"
Analyst 1
Shift: 8 AM → 4 PM
```

بدأ Case ولسه مخلصتش.

يجي:

```text id="x9n3ku"
Analyst 2
Shift: 4 PM → 12 AM
```

يقدر يفتح الـ Case ويشوف:

* الـ Tasks اللي خلصت
* الـ Tasks اللي لسه
* الـ Worklogs
* الـ Observables
* إيه اللي عمله Analyst 1

فـ Shift Handover يبقى أسهل

---

# ⭐ يعني إيه Tierless SOC؟

دي نقطة مهمة في كلام السلايد.

في SOC تقليدي ممكن يكون:

```text id="9nq3u7"
Tier 1
  ↓
Tier 2
  ↓
Tier 3
```

لكن Tierless SOC بيحاول يكون أكثر مرونة.

مش لازم الـ Case كلها تنتقل من:

**Tier 1 → Tier 2**

ممكن:

```text id="8y5v2k"
Case
 │
 ├── Easy Task → Analyst 1
 ├── Easy Task → Analyst 1
 ├── Advanced Task → Analyst 2
 └── Advanced Task → Analyst 2
```

يعني كل Analyst يساهم بالجزء اللي عنده خبرة فيه

---

# أهم فكرة في السلايد

تخيل Case = مشروع كبير.

والـ Tasks = أجزاء المشروع.

بدل ما اقول:

**"ياسمين خدي المشروع كله."**

اقدر اقول:

```text id="r3v8nd"
Case
│
├── Task A → Analyst 1
├── Task B → Analyst 1
├── Task C → Analyst 2
├── Task D → Analyst 3
└── Task E → Analyst 1
```

وكلهم شغالين على نفس الـ Case

---

# افهمها كده

### Case Assignment

مين مسؤول عن الـ Case؟

### Task Assignment

مين هيعمل الجزء ده من الـ Case؟

والميزة في TheHive:

**Case واحدة ممكن يشتغل عليها أكثر من Analyst عن طريق توزيع الـ Tasks.**

---

# 🎯 Workflow كامل

```text id="w4t1qk"
Alert
 ↓
Case
 ↓
Case Template / Playbook
 ↓
Tasks
 ↓
┌─────────────────────────┐
│                         │
↓                         ↓
Analyst 1              Analyst 2
Easy Tasks             Complex Tasks
│                         │
↓                         ↓
Worklogs               Worklogs
│                         │
└───────────┬─────────────┘
            ↓
      Case Investigation
            ↓
        Case Closed
```

---

# 🎯 الخلاصة

TheHive بيديني **Granular Assignment**؛ يعني مش لازم اسلم الـ Case كلها لشخص واحد.

اقدر اقسمها **Task-by-Task**، وده يحسن:

* التعاون
* توزيع الحمل
* التعلم
* تسليم الشيفتات
