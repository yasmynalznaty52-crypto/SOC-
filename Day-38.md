# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 38 — Good vs. Bad Cyber Threat Intelligence

الصفحة دي بتتكلم عن الفرق بين إن يكون معايا **IOCs بس** وبين **IOCs + Context**.

---

## 1️⃣ الأول: يعني إيه IOC؟

الـ **IOC = Indicator of Compromise**

هو عبارة عن حاجة أو دليل أنا لقيته، زي مثلًا:

* IP Address
* File Hash
* Domain
* File Name
* Email Address
* وغيرها من الحاجات

وبرضو بيكون اسمه زي سبق ما قولنا إنه **Observable**، وهي يعني معلومة أنا لقيتها عندي في الـ logs وأقدر أعمل عليها match.

ولكن برضو مقدرش أقول على الـ **Observable لوحده إنه CTI**.

---

## 2️⃣ Poor CTI — الـ IOC من غير Context ❌

الكتاب بيدينا مثال:

> hxxp://malwareC2[.]net was associated with a Trojan.SuperMalware campaign in June 2020.

المعلومة دي بتقول:

```text
IOC:
malwareC2[.]net

Associated with:
Trojan.SuperMalware

Time:
June 2020
```

هي أحسن من إن حد يديلك الـ domain لوحده، لكن لسه برضو الـ **Context قليل جدًا**.

بس يعني تخيل معايا إن الـ SIEM طلعلي بس ده:

```text
Alert:
Internal host communicated with
malwareC2[.]net
```

أنا كده هسأل:

* إمتى الـ campaign حصلت؟
* مين الـ Threat Actor؟
* الـ domain كان بيعمل إيه؟
* هل هو C2؟
* إيه الـ malware؟
* إيه طريقة الدخول؟
* هل الـ domain لسه malicious؟
* أعمل إيه بالجهاز اللي اتصل بيه؟

لأن كل الأسئلة دي مش متوفرة في المعلومات اللي طلعها الـ SIEM.

---

## 3️⃣ Excellent CTI — الـ IOC + Context

الجزء التاني من الصفحة بقى مليان **Context**.

تعالى نفكها:

### وقت الهجوم

**On 6/10/2020**

كده يعني عندي **Time Context**.

### مصدر الهجوم

```text
spoofed email[@]spoofedomain[.]com
```

يعني الـ attacker استخدم **spoofed email**.

### نوع الهجوم

> "Invoice" themed emails

يعني **phishing email** متعلق بـ invoice.

وده بيديني context عن الـ **Initial Access**.

### Malicious URL

```text
hxxp://totallynotlegit[.]com/
probablymalware[.]exe
```

ده **Observable** مهم.

### Malware

> detected as Trojan.SuperMalware

دلوقتي عرفت الـ malware المرتبط بالـ file.

### 🧬 Hash

**MD5: 32 characters**

الـ hash بيساعدني أحدد الـ **exact file**.

### MITRE ATT&CK

السلايد بتقول:

> (T1566.002)

وده:

> **Phishing: Spearphishing Attachment**

يعني السلوك اتربط بـ **MITRE ATT&CK technique**.

### Persistence

الـ malware:

> creates a Scheduled Task named DoingBadStuff

ومكتوب:

> (T1053.005)

يعني:

> **Scheduled Task/Job: Scheduled Task**

### C2

بعد كده:

> begins C2 over port 443

إذن عرفت:

```text
Malware
   ↓
Persistence
   ↓
C2
```

والـ C2 مرتبط بـ:

```text
malwareC2[.]net
```

والـ technique:

> T1071.001

وهي **Web Protocols** ضمن **Command and Control**.

---

## 4️⃣ الفرق

### ❌ Poor CTI

```text
malwareC2[.]net
      ↓
"Known bad"
```

أنا كـ SOC Analyst:

> طب أعمل إيه؟

أنا محتاجة **Context** لأن عندي حاجات كتير المفروض أكون عارفاها وأسألها زي سبق وقلنا، وبكده أنا هاخد وقت أدور عليه، وده معتقدش إنه في صالح الـ organization.

### ✅ Good CTI

```text
Spoofed Email
      ↓
Invoice-themed phishing
      ↓
Malicious Attachment / URL
      ↓
Malware
      ↓
Scheduled Task
      ↓
C2 over 443
      ↓
malwareC2[.]net
```

دلوقتي أنا فاهمة **القصة كاملة**.

---

## 5️⃣ ودي أهم جملة في الصفحة

> IOC = Observable + Context

يعني:

```text
IOC
 =
Observable
 +
Context
```

### Observable

هو الحاجة اللي الـ **SIEM / IDS** يقدر يعمل عليها match.

مثلاً:

* IP
* Domain
* URL
* Hash
* Email

### Context

المعلومات اللي بتشرح:

> Why is this observable bad?

زي:

* Associated malware
* Threat Actor
* Campaign
* Date
* First seen / Last seen
* TTP
* Attack stage
* Related infrastructure
* Target
* Description
* Confidence
* Source

---

## 6️⃣ ليه الـ Context مهم جدًا للـ SOC Analyst؟

تخيل الـ SIEM قالي:

```text
Connection to known malicious IP
```

لو عندك بس:

```text
IP = 1.2.3.4
```

هتبدأي من الصفر.

لكن لو الـ CTI قالت:

```text
1.2.3.4
↓
C2 infrastructure
↓
Associated with Malware X
↓
Used by Threat Actor Y
↓
Targets organizations in our sector
↓
First observed: June 2020
↓
Known TTP: PowerShell → C2
```

ساعتها تقدري تقولي:

> أيوه، الـ alert ده محتاج investigation.

وتعرفي تدوري على:

* Same IP
* Same domain
* Same malware
* Same TTP
* Same threat actor
* Same behavior

---

## 7️⃣ وده بيربط جدًا بكلامنا عن الـ Intelligence

```text
Information
     ↓
Investigation
     ↓
Enrichment
     ↓
Analysis
     ↓
Context
     ↓
Intelligence
```

الصفحة دي بتقول:

> الـ CTI الجيدة لازم تقدم الـ Context ده.

يعني مش:

> "خدي 10,000 IPs واعملي block."

لأ.

لكن:

> "ده الـ IP، وده ليه malicious، وده الـ campaign، وده الـ malware، وده الـ TTP، وده الـ threat actor، وده الزمن، وده الـ relevance."

---

## 8️⃣ الجملة الأخيرة مهمة جدًا

الكتاب بيقول تقريبًا:

لو الـ **Threat Intelligence Platform** عندي معندهاش **Description attribute** للـ IOC، فأنا كده عندي **Observable Aggregator** مش TIP حقيقي.

يعني لو MISP/TIP عندك مجرد:

```text
IP 1
IP 2
IP 3
Domain 1
Hash 1
Hash 2
```

فده مجرد تجميع **Observables**.

لكن الـ TIP المفروض يقولك:

```text
IOC
 ↓
What is it?
Why is it malicious?
Who uses it?
When was it seen?
What malware?
What campaign?
What TTP?
What should I do?
```

وده اللي يخلي الـ **Intelligence useful**.

---

# ربط الصفحة كلها ببعض

```text
             CTI
              │
              ↓
       ┌──────────────┐
       │  Observable  │
       │ IP / Domain  │
       │ Hash / URL   │
       └──────┬───────┘
              +
       ┌──────────────┐
       │   Context    │
       │ Who?         │
       │ Why?         │
       │ When?        │
       │ How?         │
       │ TTP?         │
       │ Malware?     │
       └──────┬───────┘
              ↓
       Useful CTI
              ↓
      Analyst Decision
              ↓
     Defensive Action
```

---

# ⭐ الخلاصة

### Bad CTI:

> "ده IP وحش."

### Good CTI:

> "ده IP مرتبط بـ Threat Actor X، استخدمه كـ C2 في Campaign Y، ضد نوع المؤسسات Z، وظهر مع Malware A، باستخدام TTPs معينة."

وساعتها لما يطلعلي **Alert** عليه، مش هتعامل معاه كـ IP وخلاص؛ عندي **Context** يساعدني أفهم الـ alert وأقرر هل هو فعلًا **relevant/malicious** وإيه الخطوة اللي بعدها.
