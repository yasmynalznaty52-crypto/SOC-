# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

# Day 07 - SOC Process & Technology Functions

---

## SOC Process and Technology Functions

الـ **SOC** مش عبارة عن مجموعة **SOC Analysts** قاعدين يراجعوا الـ **Alerts** وخلاص.

فيه وظائف تانية كتير، لكن مش كلها بنفس الأهمية أو بنفس طبيعة الشغل.

علشان كده الكتاب قسمها لمجموعتين.

---

# 1. Core SOC Functions

ودي الوظائف الأساسية اللي أي **SOC** لازم يقوم بيها يوميًا.

ولو واحدة منهم مش موجودة، فالـ SOC مش هيقدر يشتغل بكفاءة.

## Inside the SOC System

> **ضع هنا الرسمة الأولى من السلايد (Inside the SOC System).**

```text
[ Inside the SOC System Diagram ]
```

المراحل الأساسية هي:

```text
Data Collection
        ↓
Detection
        ↓
Triage
        ↓
Investigation
        ↓
Incident Response
```

ودي تعتبر قلب الـ SOC.

---

# 2. Specialty / Auxiliary Capabilities

ودي وظائف مساعدة، ومش شرط تكون موجودة داخل فريق الـ SOC نفسه.

في شركات كبيرة بيكون ليها Teams مستقلة، وفي شركات تانية ممكن تكون Outsourced.

## Specialty Capabilities

> **ضع هنا الدياجرام الثاني.**

```text
                Threat Intelligence
                        │
                        ▼
Data Collection → Detection → Triage → Investigation → Incident Response
                        ▲
                        │
                  Forensics
                        ▲
                        │
      Self-Assessment (VA / PT / Red Team / Inventory)
```

---

### Threat Intelligence

سبق وشرحناه قبل كده.

وهو جمع وتحليل معلومات عن المهاجمين، وأساليبهم، وأهدافهم، علشان نكون مستعدين قبل حدوث الهجوم.

---

### Forensics

التحقيق الجنائي الرقمي.

ويشمل:

- Disk Forensics
- Memory Forensics
- Malware Reverse Engineering
- eDiscovery (جمع الأدلة الرقمية)

والهدف منه معرفة:

- إزاي المهاجم دخل؟
- عمل إيه؟
- سرق إيه؟
- وكان موجود قد إيه؟

---

### Self-Assessment

وده يعتبر **Umbrella Term**، يعني مصطلح شامل يضم أكثر من نشاط، مثل:

1. Vulnerability Assessment
2. Configuration Monitoring
3. Asset Inventory
4. Penetration Testing
5. Red Team

والهدف من الأنشطة دي مش الاستجابة للهجوم بعد وقوعه، لكن اكتشاف نقاط الضعف قبل ما يستغلها المهاجم، واختبار قدرة الـ Blue Team على اكتشاف الهجمات.

وفي الشركات الكبيرة، ممكن يكون لكل وظيفة Team مستقل، بينما في الشركات الصغيرة قد يقوم بنفس الأشخاص بأكثر من وظيفة أو يتم الاستعانة بشركات خارجية (**Outsourcing**).

---

# Inside the SOC System

بعد ما عرفنا الوظائف المختلفة...

الكتاب بيطلب مننا نبص للـ SOC كنظام كامل.

أي System بيتكون من:

```text
Input
    ↓
Process
    ↓
Output
```

فالـ SOC نفس الفكرة.

- الـ Input عبارة عن الأحداث (Events) والتوقيعات (Signatures).
- الـ Process هو مراحل الـ SOC المختلفة.
- والـ Output هو معالجة الحوادث وتقليل تأثيرها على الشركة.

---

# Critical SOC Information

دي مجموعة من المعلومات والوثائق الأساسية اللي لازم تكون متوفرة عند فريق الـ SOC علشان يقدر يشتغل بكفاءة أثناء أي **Incident**.

الكتاب بيأكد إن نجاح الـ SOC مش بيعتمد على الـ SIEM أو الـ Logs فقط.

لكن يعتمد كمان على فهم بيئة الشركة بشكل كامل.

لأن أثناء الـ Investigation، لو الـ Analyst ميعرفش شكل البيئة اللي شغال فيها، هيضيع وقت كبير جدًا.

---

## 1. Network Diagram

رسم مبسط يوضح:

- الأجهزة
- السيرفرات
- الـ Firewalls
- الـ Routers
- الـ Switches

وكيفية اتصالهم ببعض.

وده مهم لأنه أثناء أي Incident أول سؤال غالبًا هيكون:

> الجهاز ده موجود فين؟
>
> بيتواصل مع مين؟

---

## 2. Points of Visibility

ودي من أهم الحاجات داخل الـ SOC.

لأنها بتوضح:

**إيه اللي إحنا شايفينه؟**

و

**إيه اللي مش شايفينه؟**

ومن أمثلتها:

### TAP

جهاز بيعمل نسخة من الـ Network Traffic ويرسلها لأدوات المراقبة مثل الـ IDS.

---

### SPAN Port

ميزة موجودة في الـ Switch بتنسخ الـ Traffic وترسله لأدوات الـ Monitoring.

---

### Full Packet Capture (Full PCAP)

الاحتفاظ بنسخة كاملة من الـ Network Packets.

وده بيساعد جدًا أثناء التحقيقات.

> 💡 **Note**
>
> عدم وجود Logs لا يعني بالضرورة عدم وجود Attack.
>
> ممكن ببساطة يكون مفيش Visibility في المكان ده.

---

## 3. Data Flow Diagram

خريطة توضح حركة البيانات داخل الشركة.

وده بيساعد الـ Analyst يعرف:

هل الاتصال اللي شايفه طبيعي؟

ولا يعتبر نشاط مشبوه؟

---

## 4. Log Flow Diagram

ودي مختلفة عن الـ Data Flow Diagram.

لأنها بتوضح رحلة الـ Logs.

يعني:

مين بيبعت Logs؟

ورايحة فين؟

وده مهم جدًا لأنه لو جهاز معين مش ظاهر في الـ SIEM، نعرف السبب.

هل:

- الجهاز مبعتش Logs؟
- ولا الـ SIEM فيه مشكلة؟
- ولا الجهاز أصلًا مش مربوط بالـ SIEM؟

---

## 5. Incident Response Plan

خطة مكتوبة توضح:

لو حصل Incident...

هنعمل إيه؟

وده بيقلل وقت اتخاذ القرار أثناء الأزمة.

---

## 6. Communication Plan

بتحدد:

- مين أول شخص يتم إبلاغه؟
- مين المسؤول بعده؟
- وإمتى يتم التصعيد؟

وده يمنع ضياع الوقت أثناء الـ Incident.

---

## 7. Critical Assets List

قائمة بأهم الأصول داخل الشركة.

مثل:

- Domain Controller
- Active Directory
- Database Servers
- Email Servers

علشان الـ Analyst يعرف إيه الأجهزة الأكثر أهمية.

---

## 8. Points of Contact

قائمة بالأشخاص المسؤولين عن كل نظام.

مثل:

- Server Owner
- Database Owner
- Cloud Team
- Network Team

لأن أثناء التحقيق ممكن تحتاج تتواصل مع الشخص المسؤول مباشرة.

---

## 9. Disaster Recovery & Business Continuity

بتوضح:

إزاي الشركة هترجع أنظمتها للعمل بعد حدوث كارثة.

وإزاي تضمن استمرار العمل حتى أثناء وجود المشكلة.

---

## 10. Policies, Standards & Procedures

أي وثائق أو سياسات مهمة داخل الشركة.

ودي بتساعد الـ Analyst يعرف:

- إيه الطبيعي؟
- وإيه اللي يعتبر مخالف للسياسات؟

---

# Summary

الكتاب بيحاول يوضح إن نجاح الـ **SOC** مش بيعتمد فقط على وجود أدوات زي **SIEM** أو **EDR**.

لكن بيعتمد كمان على وجود معلومات ووثائق أساسية تساعد الـ Analysts على فهم بيئة الشركة واتخاذ القرارات بسرعة أثناء الـ Incidents.

لازم الـ Analyst يكون فاهم:

- شكل الشبكة (Network Diagram).
- حركة البيانات (Data Flow Diagram).
- رحلة الـ Logs (Log Flow Diagram).
- أماكن الرؤية (Visibility).

وكمان تكون موجودة:

- Incident Response Plan
- Communication Plan
- Critical Assets List
- Points of Contact
- Disaster Recovery Plan
- Business Continuity Plan
- السياسات والإجراءات الخاصة بالشركة.

كل المعلومات دي بتخلي استجابة الـ SOC أسرع، وأكثر دقة، وبتوفر وقت كبير أثناء التعامل مع الحوادث الأمنية.
