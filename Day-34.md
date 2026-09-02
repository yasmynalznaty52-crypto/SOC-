# بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 34 — Cyber Threat Intelligence (CTI)

## 1️⃣ يعني إيه Cyber Threat Intelligence؟

الـ CTI هو عبارة عن اني بيجمع بيانات عن التهديدات و المهاجمين و الهجمات و احلل و اطلع منها معلومة مفيدة تساعدني في اني اخد افضل القرارات الدفاعيه

لكن TI مش بس عبارة عن ال IPS,Domains ضارة او malicious و دي اول حاجه احنا هنثبتها

---

## 2️⃣ طب يعني إيه "مش مجرد malicious ips"؟

تخيل انه عندي Threat Intelligence Feed بيقول:

```text
Malicious IP:
185.10.20.30
```

هل كده عندي Threat Intelligence؟

**مش بالضرورة.**

دي مجرد **Threat Data**.

أنا لسه محتاجة أعرف:

* الـ IP ده تبع مين؟
* بيستخدم في إيه؟
* هل هو C2؟
* هل مرتبط بـ Malware معين؟
* مين الـ Threat Actor اللي بيستخدمه؟
* بيستهدف مين؟
* بيستخدم أي Techniques؟
* هل الـ IP ده جديد ولا قديم؟
* هل عندنا أي أجهزة اتصلت بيه؟
* لو موجود عندنا، نعمل إيه؟

هنا يبدأ يظهر مفهوم **Intelligence**.

---

# الفرق المهم جدًا: Data vs Intelligence

دي من أهم الحاجات اللي عايزين نفهمها.

تخيل عندي:

```text
203.0.113.25
```

دي **Data**.

لكن لما نقول:

> الـ IP ده تم ربطه بحملة Phishing تستهدف شركات مالية، ويُستخدم كـ Command & Control server بعد إصابة الأجهزة بمالوير معين، وظهر عندنا اتصال من جهاز داخلي إليه.

هنا بقى عندنا **Intelligence**

لأننا:

```text
Data
  ↓
Analysis
  ↓
Context
  ↓
Understanding
  ↓
Action
```

---

# 4️⃣ تعريف SANS في الجزء ده

الجزء ده بيقول إن CTI باختصار:

> **Analyzed cyber threat data giving a strategic and tactical advantage over the adversary**

خلينا نفك الجملة.

## Analyzed Cyber Threat Data

يعني:

مش مجرد data خام انا بحاول احللها عشان اطلع منها معلومة مفيدة استخدمها فيما بعد

```text
Data → Analysis → Meaning
```

---

## Strategic Advantage

يعني تساعد على مستوى استراتيجي.

مثلًا:

الـ Threat Intelligence بتقول إن فيه Attack Group بيستهدف الشركات في قطاع معين باستخدام:

* Phishing
* Credential Theft
* PowerShell
* C2

الشركة ممكن بناءً على ده تقرر:

لازم نزود Detection للـ PowerShell

ونحسن Email Security

ونركز على Credential Attacks.

ده قرار **Strategic**.

---

## Tactical Advantage

يعني تساعد الـ Analyst في التحقيق الفعلي.

مثلًا عندي Alert:

```text
Host: DESKTOP-01
Destination IP: 185.x.x.x
```

واكتشف إن الـ IP ده مرتبط بـ:

```text
Malware: X
Threat Actor: Y
Campaign: Z
```

ده يساعد جدًا في الـ Investigation.

وده **Tactical**

---

# 5️⃣ طيب ليه Threat Intelligence مهمة للـ SOC؟؟؟

دي اهم نقطة بالنسبالي كSOC analyst

مثلا نفترض ان SIEM عندي طلع Alert و فيه ip خارجي احد الاجهزة الداخليه عندي اتصلت بيه لو مفيش Threat intelligence هقول تمام... وبعدين؟

لكن لو انا عندي Threat intelligence هيحصل كده:

```text
        ↓
Known Malicious IP
        ↓
Associated with Malware X
        ↓
Known C2 Infrastructure
```

فجأة الـ Alert بقى أخطر وأوضح و ده هنسميه **Enrichment**

---

# 6️⃣ Enrichment

سبق و قولنا انها عبارة عن اني بضيف معلومات جديدة للمعلومات اللي عندي عشان تبقي واضحه

كنا قلنا:

```text
Event
 ↓
SIEM
 ↓
Enrichment
 ↓
Analytics
 ↓
Alert
```

Threat Intelligence ممكن تكون جزء من الـ Enrichment.

مثلاً عندي:

```text
IP = 185.100.20.30
```

الـ SIEM ممكن يجيب معلومات إضافية:

```text
Malicious = YES
Threat Actor = X
Malware = Y
Confidence = High
First Seen = ...
Last Seen = ...
```

فبدل ما انا اشوف مجرد IP، يشوف **Context**

---

# 7️⃣ "Helps prioritize defensive resources"

**Helps prioritize defensive resources**

يعني ايه؟

يعني انه عندنا موارد محدوده فمثلا لو انا استلمت عدد alerts كبيرة فاكيد مش هقدر اتعامل معاهم بنفس الاولوية و هنا تظهر اهمية ال TI انه كمان بيحددلي اولوية ال alerts زي مثلا:

### Alert A

اتصال بـ Google.

→ غالبًا طبيعي.

### Alert B

اتصال بـ IP مرتبط بـ C2.

→ مهم جدًا.

### Alert C

اتصال بـ Domain مرتبط بحملة Malware حديثة.

→ Critical.

فال CTI بتحدد ايه اللي يستحق الاهتمام الاول

---

# 8️⃣ Offense Informs Defense

دي جملة مهمه و هي ان اللي بيعمله المهاجم هو اللي يحدد اللي انا هعمله ك blue team

لو اكتشفنا إن Attackers بيستخدموا:

```text
Phishing
↓
Malicious Attachment
↓
PowerShell
↓
C2
```

إحنا كـ Blue Team نقول:

طيب...

نعمل Detection على:

```text
Email attachment
+
PowerShell execution
+
Suspicious outbound connection
```

وبالتالي:

```text
Attack knowledge → Defensive controls
```

وهو ده جوهر Threat Intelligence

---

# 9️⃣ الـ Venn Diagram

الكتاب بيقول:

```text
Intelligence
       +
Threat Intelligence
       +
Cyber Threat Intelligence
```

وده بيمهد لنا إن CTI عبارة عن مجموعة طبقات ومفاهيم داخلة في بعض

خلينا نفهمهم من البداية

---

## 🔵 Intelligence

كلمة Intelligence بشكل عام معناها:

معلومات تم جمع وتحليل بهدف مساعدة شخص أو جهة على اتخاذ قرار

مثال خارج الـ Cyber:

لو دولة عندها معلومات إن دولة أخرى بتحضر لهجوم

المعلومة الخام مش كفاية

لازم:

* تجمع البيانات
* تحللها
* تفهم النوايا
* تحدد المخاطر
* تستخدم النتيجة في اتخاذ القرار

ده **Intelligence**

---

## 🟢 Threat Intelligence

لما نركز الـ Intelligence على Threats:

يبقى:

**Threat Intelligence**

يعني معلومات وتحليلات تساعدنا نفهم التهديدات والمخاطر

---

## 🔴 Cyber Threat Intelligence

لما الـ Threats دي تكون في عالم الـ Cyber:

**Cyber Threat Intelligence**

يعني:

Intelligence متعلقة بالـ Cyber Threats والـ Adversaries والـ Attacks.

وتساعدنا نفهم:

* مين المهاجم؟
* بيهاجم مين؟
* بيستخدم إيه؟
* إزاي بيدخل؟
* إزاي بيتحرك؟
* إزاي يحافظ على وجوده؟
* إزاي نكتشفه؟
* إزاي نمنعه؟

---

# 🔟 مثال يوضح الكلام كله

تعالي نفترض إن حصل عندنا:

```text
Alert
User clicked suspicious link
```

الـ SOC Analyst يبدأ Investigation.

يلاقي:

```text
Domain:
evil-example.com
```

دي مجرد **Observable**.

نستخدم Threat Intelligence.

نلاقي:

```text
Domain → Malicious
Domain → Phishing campaign
Campaign → Credential harvesting
Actor → Threat Group X
```

بعد كده نكتشف:

**User entered credentials**

وهنا Threat Intelligence ساعدتنا نفهم:

إيه اللي حصل؟

وكمان:

المهاجم بيعمل إيه؟

و:

إيه الإجراءات اللي المفروض نعملها؟

مثلاً:

* Block domain
* Reset credentials
* Search for other users who visited domain
* Hunt for related indicators
* Update detections
* Add relevant IOCs to monitoring

وده هو الفرق بين:

> "عندي IP ضار"

وبين:

> "عندي Intelligence تساعدني أفهم الهجوم وأتصرف ضده."

---

# 1️⃣1️⃣ طيب إيه علاقة الكلام ده بـ MISP؟

سبق و شرحنا the hive و قولنا ان وظيفته هي incident management:

يعني:

```text
Alert
 ↓
Case
 ↓
Investigation
 ↓
Tasks
 ↓
Observables
 ↓
Resolution
```

أما:

## MISP

وظيفته الأساسية:

**Threat Intelligence Platform**

يعني يساعد في:

```text
Threat Data
 ↓
Organize
 ↓
Share
 ↓
Correlate
 ↓
Use as Intelligence
```

فخلي العلاقة كده:

| الأداة           | الوظيفة الأساسية              |
| ---------------- | ----------------------------- |
| TheHive          | Incident Management           |
| MISP             | Threat Intelligence           |
| Elastic / Splunk | SIEM                          |
| EDR              | Endpoint Detection & Response |

ودي نقطة مهمة جدًا لأن SEC450 بيبني الـ SOC عندك Tool by Tool.

---

# 🧠 أهم Concept في الجزء ده

لو عايزين نخرج من الصفحة دي بفكرة واحدة بس، خليها:

**Cyber Threat Intelligence ليست مجرد IOCs، وإنما بيانات تم تحليلها وإعطاؤها Context يساعد الـ Blue Team على اتخاذ قرارات أفضل وفهم الـ Adversary.**

---

# 📌 إيه اللي اركز عليه؟

## CTI:

> **Analyzed cyber threat data that provides strategic and tactical advantage over the adversary.**

وكمان:

> **Offense informs defense**

وكمان:

> **CTI helps prioritize defensive resources.**

افهم:

الفرق بين:

```text
Raw Data
   ↓
Analysis
   ↓
Context
   ↓
Intelligence
   ↓
Decision
   ↓
Defense
```

وده أهم من حفظ التعريف حرفيًا.

---

# 🔗 نربطها بكل اللي اخدناه

إحنا كده بنبني الصورة الكبيرة للـ SOC:

```text
              THREAT ACTOR
                   ↓
              Cyber Attack
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
      Events                Alerts
        ↓                     ↓
       SIEM ←──── Threat Intelligence
        ↓
      Triage
        ↓
   Investigation
        ↓
     TheHive
        ↓
     Incident
        ↓
    Response
```

فـ Threat Intelligence مش أداة منفصلة وخلاص.

هي بتدي الـ SOC Context يخليه يفهم الـ Alerts والـ Attacks بشكل أفضل.

وده بالضبط السبب إن SANS حاطاها بعد TheHive وقبل SIEM & Automation.

---

# 🎯 الخلاصة السريعة

**TheHive** سألتك:

> "إحنا هنتعامل مع الـ Incident إزاي وننظمه؟"

**Threat Intelligence** بتسألك:

> "إحنا عارفين إيه عن الـ Threat والـ Attacker اللي بنتعامل معاه؟"

**SIEM** بيسألك:

> "إيه اللي بيحصل في بيئتنا؟"

والـ SOC Analyst بيربط التلاتة مع بعض.
