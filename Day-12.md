<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

# Day 12 - Endpoint and Application Monitoring

</div>

---

# Endpoint and Application Monitoring

ويُعرف أيضًا باسم:

> **Continuous Security Monitoring**

وهو عبارة عن مراقبة مستمرة لكل الأحداث الأمنية اللي بتحصل داخل الأجهزة (Endpoints).

الفكرة إن المراقبة بتكون **24/7**، وأي تغيير يحصل على الجهاز بيتسجل مباشرة.

لكن إحنا مش بنراقب كل حاجة، إحنا بنركز على الأحداث المهمة أمنيًا، زي مثلًا:

- تشغيل PowerShell.
- تسجيل دخول باستخدام حساب Administrator.
- تشغيل Process جديدة.
- تعديل ملفات النظام.
- تغيير إعدادات الـ Registry.

وكمان الفكرة مش مجرد إننا بنجمع Logs، لكن بنجمعها ونراقبها باستمرار، ولو حصل نشاط غير طبيعي يتم إنشاء **Alert**.

---

# Typical Endpoint Data — Data at Rest

البيانات هنا موجودة داخل الجهاز نفسه (**Data at Rest**) يعني ملفات، برامج، أو Logs مخزنة على الجهاز، وليست البيانات التي تتحرك عبر الشبكة.

---

## 1] Configuration and Baseline Monitoring

أول حاجة هي مراقبة إعدادات الجهاز.

زي مثلًا:

- هل الـ Firewall شغال؟
- هل الـ Antivirus شغال؟
- هل الـ Audit Policy مفعلة؟

كل دي تعتبر **Configuration**.

أما الـ **Baseline** فهي من أهم المصطلحات في الـ SOC.

ومعناها:

> **الشكل الطبيعي أو المتوقع للجهاز.**

قبل ما الجهاز يدخل بيئة الإنتاج (Production)، الشركة بتحدد:

- البرامج المسموح بها.
- الخدمات المسموح بها.
- إعدادات النظام.
- الـ Security Policies.
- قيم الـ Registry الطبيعية.

وبعد كده أي تغيير عن الـ Baseline يعتبر شيء يستحق المراجعة.

---

## 2] Vulnerability Scanning

وهو الفحص المستمر للثغرات الأمنية.

بنستخدم أدوات مثل:

- Nessus

علشان نعرف:

- الأجهزة الضعيفة.
- الثغرات الموجودة.
- مين محتاج تحديثات (Patches).

وكل ده قبل ما الـ Attackers يستغلوا الثغرات دي.

---

## 3] File / Registry Integrity Monitoring

ودي من أهم أنواع المراقبة.

كلمة **Integrity** معناها سلامة الملفات والإعدادات.

يعني:

- هل الملف اتغير؟
- ولا لسه زي ما هو؟

لو ملف مهم اتغير، أو اتضافت قيمة جديدة في الـ Registry، بيتم إنشاء Alert.

وده مهم لأن الـ Malware غالبًا بيعدل الـ Registry علشان يحقق **Persistence** ويشتغل بعد كل إعادة تشغيل.

مثلًا باستخدام:

- Startup Keys
- Registry Run Keys

---

## 4] Running Processes and Services

يعني مراقبة:

- البرامج (Processes).
- الخدمات (Services).

اللي شغالة على الجهاز.

ولو ظهر Process غريب أو Service غير معروفة، زي:

- Mimikatz

يبقى ده مؤشر يستحق التحقيق.

---

## 5] Autostart Items

ودي سبق واتكلمنا عنها.

وهي البرامج أو الخدمات اللي بتشتغل تلقائيًا أول ما الجهاز يفتح.

ولو الـ Malware ضاف نفسه هنا، هيشتغل بعد كل Restart.

وده يعتبر أحد أساليب الـ **Persistence**.

ومن الأماكن المهمة اللي لازم تتراقب:

- Startup Folder
- Registry Run Keys
- Scheduled Tasks
- Windows Services

---

## 6] Application Logs

ودي الـ Logs الخاصة بالتطبيقات.

زي مثلًا:

- SQL Server
- IIS
- Apache

وغيرها من التطبيقات.

---

## 7] Access and Authentication Logs

ودي من أهم أنواع الـ Logs.

لأنها بتوضح:

- مين سجل دخول؟
- مين فشل في تسجيل الدخول؟
- مين استخدم صلاحيات Administrator؟

وده مهم لأن كثير من الهجمات بتبدأ عن طريق:

- Brute Force
- Credential Theft

---

## 8] Activity Audit Logs

ودي عبارة عن Logs لكل نشاط مهم حصل على الجهاز من الناحية الأمنية.

---

## 9] Other Security-Relevant Activity

أي نشاط له علاقة بالأمن يتم تسجيله.

زي مثلًا:

- توصيل USB.
- تشغيل PowerShell.
- تفعيل أو تعطيل Firewall.
- إنشاء User جديد.
- تغيير صلاحيات.

---

## 💡 Note

طيب إزاي نحقق كل ده؟

عن طريق:

- تفعيل **Strong Audit Policy**.
- تشغيل الـ Logging المناسب.
- تجميع كل الـ Logs.
- إرسالها إلى الـ SIEM.

وهنا يبدأ الـ SIEM يعمل:

- Correlation
- Detection
- Alerting

---

# Endpoint Event Collection Illustrated

الجزء ده بيجاوب على سؤال مهم جدًا:

> **إزاي البيانات دي بتوصل للـ SOC؟**

وده الفرق بينه وبين السلايد اللي فات.

السلايد السابق كان بيجاوب على:

> **What do we collect?**

أما السلايد ده بيجاوب على:

> **How do we collect it?**

الفكرة الأساسية إن كل جهاز بيجمع الـ Events، ويحوله إلى Logs، وبعد كده يبعتها للـ SIEM.

---

# Endpoint Collection Sources

يعني إيه المصادر اللي بتطلع Logs من الجهاز؟

---

## 1] Security Suite Logging

ودي برامج الحماية الموجودة على الجهاز.

زي:

- Microsoft Defender

ودي بتسجل:

- Malware Detection
- Virus Detection
- Security Events

وبتحولها إلى Logs.

---

## 2] EDR / XDR / Endpoint Protection

الـ **EDR** بيجمع كل نشاط بيحصل على الجهاز.

زي مثلًا:

- Process Started
- Process Ended
- File Changes
- Registry Changes
- Network Connections

أما الـ **XDR** فهو بيكمل نفس الفكرة، لكنه بيربط بيانات الـ Endpoint مع:

- Network
- Email
- Cloud
- Identity

علشان يدي صورة أشمل للهجوم.

---

## 3] Antivirus

برامج مكافحة الفيروسات كمان بتولد Logs.

لكن عادةً البيانات اللي بتطلعها أقل من الـ EDR.

---

## 4] HIDS / HIPS

**HIDS (Host Intrusion Detection System)**

برنامج موجود على الجهاز يكتشف الأنشطة المشبوهة.

أما **HIPS (Host Intrusion Prevention System)**

فهو يكتشف الهجوم، ويقدر يمنعه أيضًا (**Detect + Prevent**).

---

## 5] Vulnerability Scanner

ودي أدوات فحص الثغرات الأمنية.

واتكلمنا عليها قبل كده.

---

## 6] File Integrity Monitoring (FIM)

ودي مسؤولة عن مراقبة الملفات المهمة واكتشاف أي تغيير يحصل فيها.

واتكلمنا عليها قبل كده.

---

## 7] Application Control

ودي مسؤولة عن تحديد:

مين من البرامج مسموح له يشتغل،

ومين ممنوع يشتغل.

---

## 8] Operating System Logs

ودي الـ Logs الخاصة بنظام التشغيل.

سواء:

- Windows Logs
- Linux Logs

وبتسجل أحداث زي:

- Login
- Logout
- Shutdown
- Service Started
- System Events

وكلها معلومات مهمة جدًا أثناء التحقيق.

---

## 9] Application Logs

ودي الـ Logs الخاصة بالتطبيقات المختلفة.

---

## 10] Authentication Logs

ودي بتسجل كل عمليات المصادقة (Authentication).

---

## 11] Service and Process Logging

ودي بتسجل:

- إمتى الـ Process بدأت.
- إمتى انتهت.
- إمتى Service اشتغلت.
- إمتى Service وقفت.

---

## 12] Autorun Items

ودي مسؤولة عن مراقبة البرامج اللي بتشتغل تلقائيًا مع بداية تشغيل الجهاز.

---

## 13] Application Access and Audit Logs

ودي بتسجل عمليات الوصول للتطبيقات والأنشطة المهمة اللي بتحصل بداخلها.

---

## 💡 طيب إزاي الـ Logs دي بتوصل للـ SIEM؟

عندنا طريقتين أساسيتين:

### 1] Log Agent

وده برنامج صغير بيتثبت على الجهاز.

وظيفته إنه يجمع الـ Logs، ويبعتها للـ SIEM.

---

### 2] EDR

وفي بعض البيئات، الـ EDR نفسه بيجمع البيانات، وبعدين يرسلها مباشرة إلى الـ SIEM أو إلى منصة الـ EDR، ومنها يتم ربطها بالـ SOC.

---

# الخلاصة

الفكرة الأساسية في السلايد هي أن **Endpoint Monitoring** لا يعتمد على مصدر واحد، بل يعتمد على مجموعة كبيرة من الأدوات والخدمات الموجودة على الجهاز، مثل الـ **EDR**، و**Antivirus**، و**HIDS/HIPS**، و**Vulnerability Scanner**، و**File Integrity Monitoring**، وسجلات نظام التشغيل، وسجلات التطبيقات. كل أداة من هذه الأدوات تولد **Logs** عن الأنشطة الأمنية التي تراها، ثم يتم تجميع هذه اللوجات وإرسالها إلى الـ **SIEM** (إما بواسطة **Log Agent** أو بواسطة حلول مثل **EDR**). وبهذا يصبح لدى فريق الـ **SOC** مكان مركزي يحتوي على جميع أحداث الأجهزة، مما يسمح بالبحث، والتحليل، وربط الأحداث (**Correlation**)، واكتشاف الهجمات بسرعة.
