<div align="center">

# بسم الله الرحمن الرحيم

# Day 13 - Cloud Monitoring & Visibility

</div>

---

# => What about Cloud?

بعد ما اتكلمنا عن الـ **Endpoint Monitoring** والـ **Network Monitoring**، ييجي السؤال الطبيعي:

> **What about Cloud?**

طيب لو السيرفرات أو البرامج بقت على الـ **Cloud** بدل ما تكون موجودة داخل الشركة، هل هراقبها بنفس الطريقة؟

الإجابة هي: **نعم، لكن حسب نوع خدمة الـ Cloud اللي أنا بستخدمها.**

وده لأن كل نوع من خدمات الـ Cloud بيديك مستوى مختلف من التحكم (**Control**) والرؤية (**Visibility**).

كل ما مزود الخدمة (**Cloud Provider**) يتحمل مسؤوليات أكتر، كل ما تقل قدرتك على رؤية تفاصيل النظام الداخلية.

---

# => Levels of Abstraction

**مبدأ اختفاء التفاصيل (Abstraction)**

أنواع خدمات الـ Cloud بترتب كالتالي:

```
IaaS → PaaS → SaaS → FaaS
```

كل ما اتحركنا ناحية اليمين:

- يقل التحكم في النظام.
- تقل الـ Visibility.
- يزيد اعتمادنا على الـ Logs اللي بيوفرها مزود الخدمة.

---

# => Infrastructure as a Service (IaaS)

### أمثلة

- AWS EC2
- Azure Virtual Machine
- Google Compute Engine

هنا الشركة بتوفرلك:

- Virtual Machine

وأنت المسؤول عن إدارة النظام بالكامل.

يعني عندك Windows أو Linux كامل، كأنه جهاز موجود داخل الشركة.

يبقى هتراقب تقريبًا نفس اللي كنا بنراقبه في الـ Endpoint Monitoring:

- Windows Event Logs
- Linux Logs
- Sysmon
- EDR
- Antivirus
- Running Processes
- Services
- Users
- Authentication Logs
- Registry
- File Integrity Monitoring

يعني هنا بنطبق تقريبًا نفس مفهوم **Endpoint Monitoring**.

### مثال

لو عندك EC2 على AWS.

وثبت عليه:

- Sysmon
- Microsoft Defender
- CrowdStrike
- SIEM Agent

كلهم هيشتغلوا بشكل طبيعي لأن السيرفر بالكامل تحت إدارتك.

بالإضافة إلى كده، AWS نفسها بتوفر Logs خاصة بالبيئة السحابية.

زي:

- CloudWatch

وبالتالي هيبقى عندك مصدرين للبيانات:

- Operating System Logs
- Cloud Logs

وده بيديك رؤية قوية جدًا أثناء التحقيقات.

---

# => Platform as a Service (PaaS)

### أمثلة

- Azure SQL
- AWS RDS
- Azure App Service

هنا أنت **مش مسؤول عن نظام التشغيل (Operating System).**

أنت مسؤول فقط عن التطبيق أو الخدمة.

مثلاً:

Database.

لذلك أنت مش هتشوف:

- Windows Logs
- Services
- Drivers
- Processes الخاصة بالنظام

لأن مزود الخدمة هو المسؤول عنها.

بدل كده هتراقب:

- Database Logs
- Query Logs
- Login Logs
- Failed Logins
- Slow Queries
- Configuration Changes

### مثال

لو حد حاول يعمل:

- SQL Injection

أو

- DROP DATABASE

هتلاقي الأحداث دي موجودة داخل **Database Logs**.

لكن مش هتعرف تشوف عمليات الويندوز
أو الخدمات الداخلية.

# => Software as a Service (SaaS)

ودي أكتر خدمة الشركات بتستخدمها.

### أمثلة

- Microsoft 365
- Gmail
- Salesforce
- Slack
- Zoom
- Dropbox

هنا أنت معندكش سيرفر أصلاً.

أنت مجرد مستخدم للتطبيق.

يبقى هتراقب إيه؟

**Application Logs** فقط.

زي:

- Login Logs
- Failed Logins
- Downloads
- Deletes
- Permission Changes
- Location Logs
- Audit Logs
- File Sharing Events

### مثال

موظف دخل على Microsoft 365 من روسيا الساعة 3 الفجر.

هل ده Endpoint؟

لا.

هل ده Network؟

برضه لا.

ده **Application Log**.

---

## نقطة مهمة جدًا

الكتاب بيقول إن السؤال هنا مش:

> **إيه اللي أنا عايز أشوفه؟**

لكن السؤال الحقيقي هو:

> **هل الـ SaaS Provider هيسمحلك تشوفه؟**

لأن التطبيق مش بتاعك.

هو بتاع Microsoft أو Google.

ممكن يدوك كمية كبيرة من الـ Logs.

وممكن يدوك كمية محدودة.

وده بيختلف حسب الخدمة والـ License.

---

# => Function as a Service (FaaS)

ودي اسمها كمان:

**Serverless**

وأشهر مثال عليها:

- AWS Lambda

الفكرة ببساطة:

بدل ما تشتري سيرفر...

بتكتب Function صغيرة.

AWS هي اللي تشغلها.

كل مرة حد يستدعيها:

- تشتغل.
- تنفذ الكود.
- تقف.

أنت مش شايف:

- Windows
- Linux
- Services
- Processes

ولا أي حاجة من النظام نفسه.

يبقى هتراقب إيه؟

في حاجتين مهمين جدًا.

---

## 1] Execution Logs

يعني:

- الفنكشن اشتغلت كام مرة؟
- اشتغلت إمتى؟
- مين استدعاها؟
- هل معدل التشغيل طبيعي؟

### مثال

الفنكشن الطبيعي إنها تشتغل:

100 مرة يوميًا.

وفجأة اشتغلت:

100,000 مرة.

يبقى فيه نشاط غير طبيعي يستحق التحقيق.

---

## 2] Application Logs

أنت بنفسك بتكتب Logs داخل الكود.

زي:

- User Login
- Payment Started
- Payment Failed
- User Deleted File

وكل الـ Logs دي غالبًا بتتجمع في خدمات زي:

- AWS CloudWatch

وده بيختلف لأن كل نوع من خدمات الـ Cloud بيديك درجة مختلفة من التحكم والرؤية.

---

# => Management Plane Logs

وده جزء ناس كتير بتنساهم...

مع إنه من أهم أجزاء الـ Cloud Monitoring.

الـ Management Plane Logs معناها:

مين دخل على حساب AWS أو Azure نفسه؟

مش مين دخل على السيرفر.

لكن مين عمل:

- Create VM
- Delete VM
- Create Users
- Delete Users
- Change IAM Policies
- Attach Roles
- Create Storage
- Delete Resources

كل ده لازم يتسجل.

---

## ليه ده مهم؟

تخيل إن الـ attacker سرق الـ AWS Credentials.

ودخل على الـ AWS Account.

وقام يعمل:

- GPU Server

ويشغل عليه Crypto Mining.

أو يعمل عشرات الـ Servers على حساب الشركة.

لو أنا مش بجمع الـ Management Logs...

ممكن يفضل شغال أيام أو أسابيع.

والشركة تدفع فاتورة ضخمة جدًا قبل ما تكتشف اللي حصل.

علشان كده خدمات زي:

- AWS CloudTrail
- Azure Activity Logs

بتعتبر من أهم مصادر البيانات في بيئات الـ Cloud.
