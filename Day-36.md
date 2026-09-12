Threat Definition
1️⃣ يعني إيه Threat؟

Rob M. Lee عرّف الـ Threat إنه:

Combination of Intent + Capability + Opportunity

يعني لازم يكون عندي 3 حاجات مع بعض:

Threat
  │
  ├── Intent
  ├── Capability
  └── Opportunity

لو واحدة منهم ناقصة → غالبًا الشخص/الجهة مش Threat فعلي بالنسبة لمنظمتك.
2️⃣ Intent — النية 
دي معناها هل ال attacker عنده النية او الرغبة انه يهاجمني اصلا ؟
يعني هل ال malicious actor عايز يستهدف ال organization بتاعتي انا بالاخص ؟
مثلا انا الشركة او المنظمة بتاعتي هي منظمة بنكية او ليها علاقة بالتحويلات البنكيه و في threat actor هدفه انه يسرق المعلومات البنكية و ال credentials بتاعت العملاء ده كده عنده النية 
لكن لو في شخص عادي بيعمل scan علي اي منظمة و انا من حظي وقعت معاه ده هنا معندوش النية لانه بيعمل سكان علي ايه جهة عشان يلاقي vulnerability و مش بالضرورة عنده نية تجاهي 
انا بقي ك soc لو لقيت في ال threat intel عندي انه في threat actor X بيستهدف المنظمات ال financial و انا اصلا منظمة مالية او بنكية يبقي هنا في احتمال كبير ان ال intent ممكن تكون relevant 
3️⃣ Capability — القدرة 
هنا بقي بيسأل هل ال attacker عنده الوسائل او الادوات اللي تخليه ينفذ الهجوم عليا ؟ 
يعني عنده :
-malware
-exploits
-phishing infrastructure
-botnet
-stolen credintials
-tools
-technical skills
مثال:

Attacker عايز يسرق credentials:

Intent:
"I want to steal credentials" ✅

Capability:
He has phishing malware / infrastructure ✅

إذن عنده capability

لكن لو شخص عنده نية يهاجمك، بس معندوش أي وسيلة لتنفيذ الهجوم، فـ threat level مختلف جدًا
4️⃣ Opportunity — الفرصة
دي اهم حاجه في الموضوع و هي هل فيه opening او نقطة ضعف يقدر المهاجم ده يستغلها و ينفذ الهجوم ؟
ممكن تكون:



 Software vulnerability 

 Misconfiguration 

 Exposed service 

 Weak password 

 Phishing-prone employee 

 Unpatched system 

 Exposed SSH 

 Stolen credentials 



مثال:



عندي:



Internet
   ↓
SSH exposed
   ↓
Weak password
   ↓
Server

دي Opportunity.



الـ attacker عنده فرصة يدخل
5️⃣ لازم التلاتة يكونوا موجودين

وده أهم جزء في الصفحه:



Intent
   +
Capability
   +
Opportunity
   =
Threat

مثال كامل:

Attacker A

Intent:

عايز يسرق بيانات الشركة ✅



Capability:

عنده ransomware + stolen credentials ✅



Opportunity:
 عندي VPN server vulnerable ومش patched ✅



إذن:



Intent      ✅
Capability  ✅
Opportunity ✅
──────────────
Threat      ✅
6️⃣ طب لو واحدة ناقصة؟

هنا الفكرة المهمة جدًا:

Intent موجود + Capability موجودة + Opportunity مش موجودة



Attacker wants to attack you
        +
has the tools
        +
BUT your systems are well secured
        ↓
No opportunity

هو potential threat، لكن معندوش طريق واضح حاليًا لتنفيذ الهجوم
Opportunity موجودة + Capability موجودة + Intent مش موجود

مثلًا:



عندك vulnerability خطيرة جدًا، والـ attacker عنده exploit.



لكن هو مش مهتم أصلًا بمنظمتي



Capability ✅
Opportunity ✅
Intent ❌

فمش كل vulnerability معناها إن فيه threat فعلي



ودي نقطة مهمة جدًا في الـ SOC
7️⃣ وهنا بنوصل لـ Threat Intelligence

الصفحه اللي قبل دي



كنا بنقول:



Raw Data
   ↓
Analysis
   ↓
Context / Requirement
   ↓
Assessment
   ↓
Decision

دلوقتي Rob بيضيف مفهوم الـ Threat



تعريفه لـ Threat Intelligence تقريبًا:

تحويل raw data إلى information/intelligence تساعد في تحقيق requirement، فيما يتعلق بـ adversaries عندهم Intent + Capability + Opportunity لإحداث ضرر

يعني مش مجرد:



IP = 185.x.x.x

ولا:



Malware = ransomware

لكن نسأل:

هل الـ adversary ده يمثل Threat بالنسبة ليا؟ وليه؟
8️⃣ مثال SOC كامل 

تخيل انه في Threat Intelligence Feed قالت:



IP: 10.50.20.30

Associated with:
Threat Actor X

دي لوحدها raw information



الـ SOC يعمل Analysis:

Step 1 — Intent

Threat Actor X معروف إنه بيستهدف:



Financial organizations

وأنا organization مالية



Intent ✅

Step 2 — Capability

الـ threat actor معروف باستخدام:



Phishing
PowerShell
Credential Theft
C2



Capability ✅

Step 3 — Opportunity

اكتشف إن عندي:



Internet-facing vulnerable server

أو employee وقع في phishing



Opportunity ✅

إذن:



Intent      ✅
Capability  ✅
Opportunity ✅
       ↓
Threat to our organization

وهنا الـ SOC يقدر ياخد decision:



 Increase monitoring 

 Hunt for related IOCs 

 Block malicious infrastructure 

 Patch vulnerability 

 Investigate affected hosts 

 Reset compromised credentials 



وده بالضبط اللي بيخلي Threat Intelligence مفيدة
9️⃣ أهم نقطة في الصفحه كلها

لازم اخلي بالي من الفرق ده:

Vulnerability ≠ Threat

وجود vulnerability عندك:



Vulnerability
      ↓
Opportunity

لكن لوحدها مش Threat ده مجرد عنصر من عناصره التلاته



لازم يكون فيه adversary عنده:



Intent
+
Capability
+
Opportunity

عشان نقول إن عندنا Threat حقيقي بالنسبة للـ organization
🔟 وربطها بالـ Intelligence → Threat Intelligence → Cyber Threat Intelligence

دلوقتي الصورة اللي كانت ملخبطة قبل كده هتبقى أوضح:



Intelligence
      ↓
Threat Intelligence
      ↓
Cyber Threat Intelligence

Intelligence

أي intelligence تساعدني آخد قرار 



مثال:

Traffic is heavy → leave home earlier.

Threat Intelligence

Intelligence مرتبطة بالـ threats.



مثال:

Threat Actor X is targeting banks.

Cyber Threat Intelligence

Threat Intelligence مخصوصة بالـ cyber threats:



Threat Actor
Malware
Phishing
C2
Exploits
Credentials
IOCs
TTPs

والهدف في النهاية:

أخد defensive decisions أفضل
نفهمها بالشكل ده



THREAT =
Intent + Capability + Opportunity

Intent

عايز يعمل إيه؟

Capability

يقدر يعمل إيه؟ / عنده إيه؟

Opportunity

عنده فرصة يدخل منين؟

⭐ مثال للفهم



Intent:
I want to attack your organization.

Capability:
I have the tools/skills to attack.

Opportunity:
You have a weakness I can exploit.

        ↓

THREAT



 اهم حاجه اعرفها

Threat = Intent + Capability + Opportunity

والـ 3 معاني:



Intent → desire to attack 

Capability → means/tools to attack 

Opportunity → opening/weakness to attack 

مش أي attacker أو vulnerability يعتبر Threat بالنسبة لي.



لازم نسأل:

هل عنده نية؟ هل عنده القدرة؟ هل عنده فرصة؟

ولو التلاتة موجودين، هنا Threat Intelligence تساعدني أحلل الموضوع وأحدد إيه القرار الدفاعي اللي المفروض آخده.



وده بيربط السلايد دي مباشرة بالسلايد اللي قبلها:

Raw Data → Analysis → Intelligence → Decision.
