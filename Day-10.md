<div align="center">

# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 10 - Two Sides of Monitoring

</div>

---

## Module Overview

في الجزء ده هنتعلم:

- Two Sides of Monitoring
- Network Monitoring
- Endpoint & Application Monitoring
- What Can You See on Your Network?
- How Did We Get These Answers?

> **Monitors: Network and host data is captured and centralized.**

---

# Two Sides of Monitoring

في أول شرط من شروط الـ **Defensible Network** كان بيتكلم عن **Visibility**، يعني لازم يكون عندنا رؤية واضحة لكل اللي بيحصل داخل الشبكة.

عندنا طريقين للمراقبة.

يعني الكتاب مقسمها لطريقتين، لكن ده **لا يعني إن التقسيمة دي قانون ثابت**، ده مجرد تقسيم بيساعدنا نفهم ونرتب أفكارنا.

---

## 1. Network Monitoring

ده معناه مراقبة الاتصالات اللي بتحصل داخل الشبكة.

وإحنا هنا مهتمين نعرف:

- مين بيكلم مين؟
- بأي بروتوكول؟
- وبأي طريقة؟

### مصادر البيانات

### 1. Firewall Logs

أعرف مين اتسمح له يدخل.

ومين اترفض.

ومين حاول يعمل **Connection**.

---

### 2. DNS Logs

أعرف الجهاز عمل **DNS Resolution** لأنهي **Domain**.

---

### 3. Proxy Logs

أعرف المستخدمين دخلوا على أنهي مواقع.

---

### 4. IDS / IPS

تكتشف الـ **Suspicious Traffic** أو الهجمات المعروفة.

---

### 5. Packet Capture (PCAP)

أشوف الـ **Packets** نفسها وهي بتعمل الاتصال.

---

## 2. Endpoint / Application Monitoring

هنا بدل ما نبص على الشبكة...

بنبص على الجهاز نفسه (**Endpoint**).

وهنا نسأل:

**إيه اللي بيحصل داخل الجهاز؟**

---

### 1. EDR

أدوات الـ **Endpoint Detection and Response**، زي:

- Microsoft Defender for Endpoint

ومن خلالها أراقب:

- User Activity
- Processes
- Memory
- File Changes

---

### Application Monitoring

الكتاب ضامم الـ **Application Monitoring** مع الـ **Endpoint Monitoring**، لأن مش كل حاجة لازم تكون جهاز كامل.

ممكن نراقب التطبيق نفسه.

وغالبًا بيعتمد على:

- Operating System Logs
- Application Logs

---

## 💡 Important Note

الكتاب بيقول:

> **This distinction is not a true delineation.**

يعني التقسيمة دي **مش حقيقية بشكل صارم**.

والفكرة اللي المفروض أطلع بيها هي:

**هل عندي Visibility كافية عشان أكتشف الـ Attack؟**

ودول هما الحاجتين الأساسيتين اللي بيحتاجهم الـ **SOC** في شغله.

---
# What Can You See on Your Network?

الجزء ده مهم لأنه بيخليني بدل ما أبص على الشبكة إنها مجرد أجهزة وكابلات، أبص لها بطريقة مختلفة وأسأل:

- أنا شايف إيه؟
- وهل اللي أنا شايفه كفاية إني أكتشف أي **Attack**؟

الفكرة الأساسية هي:

قبل ما أدافع عن الشبكة، لازم أعرف أنا أصلاً شايف إيه منها.

لأن مستحيل أكتشف **Attack** حصل في مكان أنا معنديش أي **Logs** أو **Monitoring** ليه.

عشان كده الصفحة دي بتسأل شوية أسئلة:

---

## 1. Can you see high-level bandwidth statistics and traffic flow?

يعني هل أقدر أعرف حركة الـ **Traffic** ماشية إزاي؟

زي مثلاً:

- مين بيبعت لمين؟
- أي جهاز بيستهلك **Bandwidth** أكتر؟
- حجم البيانات الداخلة والخارجة.
- حركة الـ **Traffic Flow** داخل الشبكة.

وده بيساعدني أفهم سلوك الشبكة بشكل عام.

---

## 2. Do you know which ports are actually in use?

لازم أعرف الـ **Ports** اللي شغالة عندي وعليها **Services**.

لأن لو ظهر **Port** غريب أو غير متوقع، أعرف إن ده ممكن يكون:

- Malware
- Reverse Shell
- Unauthorized Service

وده بيساعدني أكتشف أي نشاط غير طبيعي.

---

## 3. Which protocols are actually being used on those ports?

البورت **مش معناه البروتوكول**.

لأن الـ **Attackers** أحيانًا بيستخدموا بروتوكولات مختلفة على Ports معروفة.

مثال:

ممكن يستخدم **SSH** على **Port 443** علشان يعدي من خلال الـ **Firewall**.

علشان كده لازم أعرف البروتوكولات اللي شغالة فعليًا، مش مجرد أرقام الـ Ports.

---

## 4. What applications are being accessed with those services?

يعني الـ **User** فاتح إيه؟

وده مهم لأن ممكن الموظف يبعت ملفات الشركة على:

- Dropbox
- Google Drive

أو يكون فيه **Malware** بيستخدم اتصال **HTTPS** من غير ما تلاحظ لو إنت شايف إن كله مجرد HTTPS.

علشان كده لازم أعرف التطبيقات والخدمات اللي بيستخدمها المستخدم.

---

## 5. Do you know which domains are being visited and by whom?

مثلاً:

```text
PC-17  ───► evil.com
```

كده أنا عرفت:

- الجهاز المصاب.
- الـ **Domain** اللي زاره.

وده غالبًا بيعتمد على:

- DNS Logs
- Proxy Logs
- Web Logs

---

## 6. Can you retrieve the full packet data from the transaction?

وده أعلى مستوى من الـ **Visibility**.

واسمه:

**Full Packet Capture (Full PCAP)**

ودي مش مجرد معرفة مين بيكلم مين.

لكن بنحتفظ بكل بيانات الاتصال، زي:

- Packet Headers
- Requests
- Responses
- Payloads

وده بيساعد جدًا في التحقيقات (**Incident Investigation**).

لكن مش كل الشركات تقدر تطبقه، لأنه محتاج:

- Storage كبيرة.
- Processing قوية.
- تكلفة عالية.

---

## 7. Can you detect suspicious encrypted traffic?

دي نقطة مهمة.

دلوقتي أغلب مواقع الـ **Web** بتستخدم **HTTPS**.

وده بيخلي الـ **Request** والـ **Response** مشفرين.

لكن ما زال عندي معلومات أقدر أشوفها، زي:

- حجم البيانات.
- الـ Certificate.
- الـ Domain.
- الـ IP Address.
- توقيت الاتصال.

ومن خلال المعلومات دي أقدر أعرف لو فيه نشاط غير طبيعي أو اتصال مشبوه.

---
---

# How did we get these answers?

بعد كل الأسئلة اللي فاتت، ييجي السؤال المهم:

**إزاي عرفنا كل المعلومات دي أصلاً؟**

الإجابة ببساطة:

لأن عندنا **Monitoring Tools** بتجمع بيانات من أماكن مختلفة داخل الشبكة.

بدون الأدوات دي، مستحيل أجاوب على الأسئلة اللي فاتت.

يعني لازم يكون عندي مصادر بيانات مختلفة، وكل مصدر بيجاوب على سؤال معين أثناء الـ Investigation.

أمثلة على مصادر البيانات:

- DNS Logs
- Firewall Logs
- Proxy Logs
- IDS / IPS
- Packet Capture
- EDR
- Windows Event Logs
- Linux Logs
- Web Server Logs

بعد كده البيانات دي كلها بتتجمع في مكان مركزي غالبًا:

- **SIEM**

وده اللي بيخلي الـ SOC Analyst يقدر يربط الأحداث ببعض أثناء التحقيق.

---

## مثال بسيط

لو ظهر Alert إن جهاز اتصل بـ **evil.com**.

المحقق ممكن يستخدم أكثر من مصدر بيانات:

- **DNS Logs** ➜ الجهاز عمل Resolve لأنهي Domain؟
- **Firewall Logs** ➜ هل الاتصال خرج فعلاً؟
- **Proxy Logs** ➜ المستخدم فتح إيه؟
- **Packet Capture** ➜ إيه البيانات اللي اتبعت؟
- **EDR** ➜ إيه الـ Process اللي عمل الاتصال؟

لما أجمع كل المصادر دي مع بعض، أقدر أفهم الصورة كاملة بدل ما أشوف جزء واحد فقط.

---

## 💡 Important Note

الكتاب بيركز جدًا على فكرة إن:

**أي Tool داخل الـ SOC بيجاوب على نوع معين من الأسئلة.**

مفيش Tool واحدة تعرف كل حاجة.

وده السبب إن الـ SOC بيعتمد على دمج مصادر بيانات مختلفة، ثم إرسالها إلى الـ SIEM، وبعدها يبدأ الـ Analyst عملية الـ Investigation.

---

## الخلاصة

الفكرة الأساسية من الجزء ده إن كل الأسئلة اللي سألناها عن الشبكة (مين بيتكلم مع مين؟ إيه البروتوكولات المستخدمة؟ إيه الـ Domains اللي تم الوصول ليها؟ هل أقدر أشوف الـ Packets؟...) مش هنعرف نجاوب عليها إلا لو عندنا مصادر بيانات مناسبة. كل أداة Monitoring بتوفر جزء من الصورة، ولما نجمع البيانات دي في الـ SIEM ونربطها ببعض، يقدر الـ SOC Analyst يشوف الصورة الكاملة ويحقق في الـ Incident بشكل أسرع وأدق.
