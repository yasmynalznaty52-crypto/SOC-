# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 20 - Part 2: Alert Log Flow Options

**السؤال الأساسي بعد ما الـ Alerts تتولد:**

> **هنعمل لها Triage فين؟**

وعندنا اختيارين رئيسيين:

* **Option 1 ⇒ Point Product**
* **Option 2 ⇒ Master Queue**

**Option 1 ⇒ Point Product**

كل Alert بتعمل Triage داخل الـ Point Product اللي ولده.

**Option 2 ⇒ Master Queue**

كل الـ Alerts تتجمع في Queue واحدة غالبًا داخل الـ SIEM أو Tool مركزية أخرى.

---

# Option 1] Point Product

تعمل Triage داخل الـ Point Product.

## عرض الدرس

يعني كل Security Tool مسؤولة عن الـ Alerts بتاعتها.

مثلاً:

```text
EDR
 ↓
EDR Alerts
 ↓
EDR Console
 ↓
Analyst
```

والـ IDS:

```text
IDS
 ↓
IDS Alerts
 ↓
IDS Console
 ↓
Analyst
```

والـ Email Security:

```text
Email Security
 ↓
Email Alerts
 ↓
Email Console
 ↓
Analyst
```

فممكن الـ Analyst يكون عنده:

```text
EDR Queue
IDS Queue
Firewall Queue
Email Queue
SIEM Queue
```

---

# طيب ليه نختار Option 1؟

هنا الكتاب قال:

> **"Security tools may provide better interface for assessing their type of alerts"**

يعني كل Security Tool بتكون متخصصة في نوع معين من الـ Data، وبالتالي الـ Vendor بيعمل لها Interface مناسبة لتحليل النوع ده من الـ Alerts.

---

# مثال مهم: PCAP Tool

افترضي عندك Network Security Tool بتتعامل مع:

**PCAP = Packet Capture**

الأداة ممكن تكتشف:

```text
Suspicious Network Traffic
```

لو دخلتي على الـ Tool نفسها، ممكن تلاقي:

```text
Packet #124
Source IP
Destination IP
Protocol
Port
Payload
TCP Flags
Packet Contents
```

وممكن تعملي:

```text
Follow TCP Stream
Extract Data
Inspect Packets
```

وده Interface متخصص جدًا في تحليل الـ Network Traffic.

لكن لو نفس الـ Alert راح للـ SIEM، فالـ SIEM غالبًا مش هيقدر يديكي نفس مستوى الـ Packet Analysis.

---

# مثال تاني: EDR

لو عندك Alert من الـ EDR:

```text
Suspicious PowerShell Execution
```

الـ EDR ممكن يعرض لك:

```text
Process Tree

winword.exe
     ↓
powershell.exe
     ↓
cmd.exe
     ↓
malware.exe
```

وممكن يديك:

* Command Line
* Parent Process
* Child Process
* File Hash
* User
* Host
* Process Timeline
* Network Connections

وده Interface معمول تحديدًا لتحليل Endpoint Activity.

فالـ EDR هنا أفضل مكان لفهم تفاصيل الـ Endpoint Alert.

بيعمل Interface كويسة لتحليل الـ Alert الخاصة بالأداة:

**Deep / Specialized Analysis**

---

# الميزة في Option 1

كل أداة عندها الـ Context الخاص بيها وواجهة متخصصة في نوع الـ Data.

| Alert               | أفضل Tool للتفاصيل |
| ------------------- | ------------------ |
| Network Traffic     | IDS / PCAP Tool    |
| Endpoint Process    | EDR                |
| Email               | Email Security     |
| Web Attack          | WAF                |
| Firewall Connection | Firewall           |

---

# لكن المشكلة هنا هي

الكتاب بيقول:

> **"You will have multiple alert queues to keep on top of"**

يعني عندك أكتر من Alert Queue لازم الـ Analyst يتابعهم.

مثلاً:

```text
             Analyst
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
      EDR      IDS     Firewall
       ↓        ↓        ↓
     Queue    Queue    Queue
```

وفوق دول:

```text
Email Queue
SIEM Queue
Cloud Queue
```

ودي مشكلة في الـ Triage.

لأن الهدف الأساسي من الـ Triage إني أعرف:

> **إيه أهم Alert أتعامل معاه الأول؟**

وكمان الـ Analyst لازم يبص على كذا Queue ويفاضل بينهم على مستوى الـ SOC كله.

يعني المشكلة مش إن الـ Point Product وحشة، بالعكس، هي ممتازة في الـ **Deep Analysis**، لكن المشكلة في إن عندي:

**Multiple Queues**

---

# Option 2] Master Queue

كل الـ Alerts تتجمع في مكان واحد:

**Single Queue**

غالبًا داخل الـ SIEM.

## المميزات

وأهم ميزة هنا هي:

**SIEM Context**

وهي إن الـ SIEM عنده Data من مصادر كتير، فممكن ياخد Alert من Point Product ويضيف له معلومات من مصادر أخرى.

خلينا ناخد مثال.

الـ IDS قال:

```text
Possible C2 Communication
```

لو دخلتي على الـ IDS فقط، ممكن تعرفي:

```text
Source IP: 10.10.10.20
Destination IP: 185.x.x.x
Port: 443
```

لكن الـ SIEM ممكن يقولك:

```text
IDS:
Possible C2 Communication

+

EDR:
powershell.exe running

+

Windows:
User logged in recently

+

DNS:
Host resolved suspicious-domain.com

+

Threat Intel:
Destination IP = Malicious
```

الـ SIEM جمع كل الـ Information دي.

---

# النتيجة؟

بدل Alert بسيط:

```text
Possible C2 Communication
```

بقى عندك صورة أقوى:

```text
Possible C2 Communication

Host: PC-023
User: Alice
Process: powershell.exe
Destination: Malicious IP
DNS Query: suspicious-domain.com
Threat Intel: Malicious
```

وده اسمه:

**Enrichment**

ومعناه:

> إضافة معلومات للـ Alert عشان أقدر أفهمه بشكل أفضل.

---

# Fidelity

وده يودينا لمفهوم مهم وهو:

**Fidelity**

يعني ببساطة:

> **قد إيه الـ Alert عنده Evidence / Context يخليك تثق إنه فعلًا يستحق Investigation؟**

والـ Fidelity عامل مهم في اختيار الـ Master Queue.

لأن الـ SIEM مش بس بيعمل جمع لكل الـ Alerts في مكان واحد، هو كمان ممكن يعمل:

**Correlation + Enrichment**

يعني يربط الأحداث المختلفة ببعض ويضيف Context للـ Alert.

---

# طيب هل Option 2 مثالي؟

لا.

الكتاب بيقول إن عنده **Small Downside** وهي:

> **"Lack of a custom interface"**

يعني الـ SIEM مش متخصص في كل نوع من الـ Alerts.

---

# مثال: EDR Alert داخل SIEM

عندك EDR Alert:

```text
Suspicious PowerShell
```

في الـ EDR ممكن تشوفي:

```text
Process Tree
Timeline
File
Hash
Command Line
Network
User
```

لأن الـ EDR معمول عشان تشوفي الـ Endpoint بالتفصيل.

لكن في الـ SIEM ممكن تشوفي:

```text
Alert:
Suspicious PowerShell

Host:
PC-123

User:
Bob

Command:
powershell.exe ...
```

لكن مش بنفس الـ Richness بتاع الـ EDR.

---

# الحل: SIEM + Point Product

الكتاب بيقترح حل كويس جدًا:

مش لازم أختار بين الـ SIEM والـ EDR.

ممكن أعمل:

```text
SIEM
 ↓
Master Queue
 ↓
Analyst
 ↓
┌──────────────────────────┐
│                          │
↓                          ↓
Investigate in SIEM     Need Deep Analysis
                            ↓
                       Point Product
```

يعني الـ SIEM هو المكان الأساسي للـ Triage.

لكن لو محتاج تفاصيل أكتر، أعمل:

**Pivot to the Point Product**

---

# مثال عملي

الـ SIEM عنده Alert:

```text
Suspicious PowerShell Execution
```

الـ Analyst يبدأ في الـ SIEM:

```text
Who?
What?
When?
Where?
Why?
```

ويشوف:

```text
User: Ahmed
Host: LAPTOP-22
Parent Process: WINWORD.EXE
Command: powershell -enc ...
Destination: 185.x.x.x
```

هنا يقول:

> **محتاج أشوف الـ Process Tree بالتفصيل.**

فيضغط:

```text
[Open in EDR]
```

فينقله مباشرة إلى الـ EDR Alert.

وده اللي الـ SANS يقصده بـ:

> **"Linking directly to the alert in the point product console"**

---

# الشكل النهائي

```text
                    EVENTS
                       ↓

        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
       EDR            IDS          Firewall
        ↓              ↓              ↓
      Alerts         Alerts        Alerts
        └──────────────┼──────────────┘
                       ↓
                      SIEM
                       ↓
              Correlation / Enrichment
                       ↓
                  MASTER QUEUE
                       ↓
                    TRIAGE
                       ↓
              ┌────────┴─────────┐
              ↓                  ↓
        Investigate         Need Deep Analysis
           in SIEM                  ↓
                               Pivot to EDR/IDS
```

---

# احفظيها كـ 4 كلمات

لو السلايد دي هتدخليها في دماغك للـ SOC، ركزي على:

### Option 1 → Specialization

كل Tool ممتازة في تحليل نوع الـ Alert بتاعها.

لكن:

**Multiple Queues → Difficult Prioritization**

---

### Option 2 → Centralization

كل الـ Alerts في Queue واحدة.

لكن الأهم:

**SIEM Context + Correlation + Enrichment**

↓

**Higher Fidelity**

↓

**Better Triage**

---

# أفضل Approach عمليًا

**Centralized Triage + Specialized Investigation**

يعني:

> **Triage centrally in the SIEM, then pivot to the Point Product when deeper analysis is required.**

ودي من أهم جمل السلايد:

```text
SIEM
 ↓
Centralized Triage
 ↓
Prioritization
 ↓
Need More Context?
 ↓
Pivot to Point Product
 ↓
Deep / Specialized Investigation
```

والفكرة الأساسية هنا:

> **مش لازم مكان الـ Triage يكون هو نفس مكان الـ Deep Investigation.**
