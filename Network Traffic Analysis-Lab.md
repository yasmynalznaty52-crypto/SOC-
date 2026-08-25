1. الفكرة الأساسية: ليه أصلاً بنحلل Network Traffic؟

في الـSOC عندنا مصادر كتير للـvisibility:

Firewall logs
DNS logs
EDR logs
Proxy logs
SIEM alerts
IDS/IPS alerts

لكن المشكلة إن الـlogs غالبًا بتدينا جزء من الصورة فقط.

مثلاً الـFirewall ممكن يقولك:

192.168.1.16 → DNS → malicious-tld.com

أنتِ عرفتي:

مين بعت؟ → 192.168.1.16
راح فين؟ → malicious-tld.com
إمتى؟ → Timestamp
نوع الطلب؟ → DNS

لكن إيه اللي اتبعت فعليًا؟
ممكن ما تعرفيش.

وهنا يأتي دور:

Network Traffic Analysis = تحليل الـPackets والـNetwork Communication نفسها.

2. أهم مثال: DNS Tunneling

عندنا جهاز:

WIN-016
192.168.1.16

وبيعمل:

aj39skdm.malicious-tld.com
msd91azx.malicious-tld.com
cmd01.malicious-tld.com
cmd01.malicious-tld.com
إيه اللي يخلي الموضوع Suspicious؟

لاحظي:

aj39skdm
msd91azx
cmd01

كل مرة Subdomain مختلف، لكن نفس الـdomain:

malicious-tld.com

ده ممكن يكون indicator على:

DNS Tunneling / DNS C2

لأن المهاجم ممكن يستغل DNS في نقل بيانات أو أوامر.

3. DNS Tunneling ببساطة

طبيعيًا:

PC
 ↓
DNS Query
 ↓
DNS Server
 ↓
IP Address

مثلاً:

google.com
     ↓
142.250.x.x

لكن المهاجم ممكن يعمل:

Data
 ↓
Encode
 ↓
DNS Query
 ↓
attacker-domain.com

مثلاً:

aj39skdm.attacker.com

ثم:

msd91azx.attacker.com

وهكذا.

وبالتالي الـDNS نفسه أصبح قناة اتصال.

4. ليه TXT مهم؟

في المثال:

QTYPE=TXT

الـTXT record يقدر يحمل text data.

المهاجم ممكن يستخدمه لإرسال:

C2 Commands

للجهاز المصاب.

مثلاً:

DNS Query
cmd1.evilc2.com

والـresponse يرجع:

TXT:
SSBsb3ZlIHlvdXIgY3VyaW91c2l0eQ==

دي Base64.

لو فكيناها هتطلع:

I love your curiousity

يعني الـDNS response نفسه كان يحمل data.

وده أهم درس هنا:

الـDNS log ممكن يقولك إن Query حصل، لكن Packet Capture ممكن يكشف المحتوى الموجود داخل الـDNS response.

5. Logs vs Packet Capture

دي من أهم الحاجات في اللاب.

Logs

بتديك metadata غالبًا:

Source IP
Destination IP
Port
Protocol
Timestamp
Domain
Action

لكن ممكن ما يكونش فيها:

Packet payload
Full headers
Sequence numbers
Fragment offsets
MAC-level details
Packet Capture / PCAP

بتديك تفاصيل الـpacket نفسها.

مثلاً:

Ethernet Header
       ↓
IP Header
       ↓
TCP/UDP Header
       ↓
Application Header
       ↓
Payload

وده السبب إن:

Logs tell you that communication happened.
Packet analysis can tell you what happened inside that communication.

6. TCP/IP Stack — لازم تفهميه

اللاب بدأ بعد كده يشرح:

What exactly can we monitor?

باستخدام TCP/IP model.

فكري فيها كده:

Application
     ↓
Transport
     ↓
Internet
     ↓
Link

كل Layer بتضيف معلومات للـpacket.

🟦 7. Application Layer

هنا بنشوف:

Application protocol
Application headers
Payload

مثلاً HTTP:

GET /downloads/suspicious_package.zip HTTP/1.1
Host: www.example.com
User-Agent: curl/7.85.0

من الـlog ممكن تعرفي:

Client requested:
suspicious_package.zip

والـserver رد:

HTTP/1.1 200 OK
Content-Type: application/zip

إذن:

الملف اتطلب واتقبل.

لكن السؤال المهم:

هل نعرف محتوى الـZIP من الـHTTP logs؟

لا.

الـlogs ممكن تقول:

filename = suspicious_package.zip
size = 10 MB
status = 200

لكن مش بالضرورة تشوف:

What's inside the ZIP?

وهنا نحتاج:

Packet Capture

علشان ممكن نستخرج الـpayload ونحلل الملف.

🟨 8. Transport Layer

أشهر protocols:

TCP
UDP

هنا عندنا حاجات زي:

Source Port
Destination Port
Sequence Number
Acknowledgment Number
TCP Flags
Window Size

مثلاً:

192.168.1.45:51432
        ↓
172.217.22.14:443
9. TCP 3-Way Handshake

دي لازم تكون ثابتة عندك جدًا في SOC.

Client                    Server

   SYN  ────────────────→

        ←──────── SYN/ACK

   ACK  ────────────────→

يعني:

1️⃣ SYN

Client:

"عايز أفتح connection."

2️⃣ SYN/ACK

Server:

"تمام، أنا موافق."

3️⃣ ACK

Client:

"تمام، نبدأ communication."

10. Sequence Number مهم ليه؟

في المثال الطبيعي:

Seq=1
Seq=1
Seq=1

وبعدين:

Seq=1

لكن ظهر packet من:

192.168.99.200

وفيه:

Seq=34567232

هنا عندنا حاجة suspicious.

ليه؟

لأن الـattacker ممكن يحاول:

Inject packets into an existing TCP session

وده ممكن يرتبط بـ:

TCP Session Hijacking

الفكرة:

Victim
   ↓
Existing TCP Session
   ↓
Attacker injects packet

والـSequence Number غير المتوقع ممكن يكون Indicator يستحق التحقيق.

🟥 11. Internet Layer

هنا بنتعامل أساسًا مع:

IP

ومن أهم المعلومات:

Source IP
Destination IP
TTL
Fragment Offset
Total Length

غالبًا الـlogs بتديك:

SRC
DST
TTL

لكن في حالات معينة نحتاج تفاصيل أكتر.

12. IP Fragmentation

لو الـpacket أكبر من الـMTU، ممكن تتقسم:

Original Packet
       ↓
Fragment 1
Fragment 2
Fragment 3

كل fragment عنده معلومات تساعد في إعادة تجميع الـpacket.

13. Fragmentation Attacks

المهاجم ممكن يستغل fragmentation علشان:

IDS Evasion

يخلي الـIDS يشوف fragments بشكل مختلف عن الطريقة اللي الـdestination هيعيد بيها تجميعها.

مثلاً:

Fragment 1
Fragment 2
Fragment 3

لكن بعض الـfragments ممكن تعمل:

Overlapping

زي المثال:

Fragment 2:
Offset = 1480

Fragment 3:
Offset = 1480

فالاتنين بيبدأوا في نفس المكان.

ده ممكن يعمل:

Overlapping byte ranges

ويؤدي إلى اختلاف في إعادة التجميع.

وده ممكن يستغله attacker لـ:

IDS/IPS Evasion

🟩 14. Link Layer

هنا عندنا:

MAC Addresses

مثلاً:

Source MAC
Destination MAC

وده مهم جدًا في:

ARP Poisoning / ARP Spoofing

15. ARP Poisoning

طبيعي:

Who has 192.168.1.10?

192.168.1.10 is at
00:11:22:33:44:55

لكن attacker يقول:

192.168.1.10 is at
aa:bb:cc:dd:ee:ff

مع إن ده مش الـMAC الحقيقي.

النتيجة؟

الأجهزة ممكن تبدأ تبعت traffic للـattacker بدل الجهاز الحقيقي.

وده ممكن يسمح بـ:

Man-in-the-Middle (MITM)

⭐ أهم Attack Techniques في الجزء ده

احفظي الربط ده:

Network evidence	ممكن يشير إلى
Excessive DNS queries	DNS tunneling / C2
Random-looking subdomains	DNS tunneling
DNS TXT responses	C2 / data transfer
Suspicious HTTP payload	Malware download
Abnormal TCP sequence	Session hijacking / injection
Overlapping IP fragments	Fragmentation attack / IDS evasion
Conflicting ARP replies	ARP poisoning
Same MAC associated with multiple IPs/interfaces	ARP spoofing
16. Sources of Network Traffic

اللاب قسم المصادر إلى نوعين:

Network Traffic Sources
        │
   ┌────┴────┐
   │         │
Endpoint   Intermediary
🟦 Endpoint

دي الأجهزة اللي بتبدأ وتنهي الـtraffic.

أمثلة:

PCs
Servers
IoT
Printers
Phones
Tablets
Cloud resources

مثلاً:

PC → Web Server

الـPC هنا Endpoint.

🟧 Intermediary

دي الأجهزة اللي الـtraffic بيعدي من خلالها.

أمثلة:

Firewall
Router
Switch
Proxy
IDS
IPS
Access Point
WLC

مثلاً:

PC
 ↓
Switch
 ↓
Firewall
 ↓
Internet
 ↓
Server

الـSwitch والFirewall هنا Intermediary.

17. North-South Traffic

دي مهمة جدًا.

فكري فيها:

Internet
   ↕
Firewall
   ↕
LAN

Traffic داخل أو خارج الشبكة.

يعني:

Traffic crossing the network boundary

مثلاً:

PC → Internet
Internet → PC

أمثلة protocols:

HTTPS
DNS
SSH
VPN
SMTP
RDP

وغالبًا الـfirewall بيكون عنده visibility كويسة عليها.

18. East-West Traffic

دي traffic داخل الشبكة نفسها.

مثلاً:

PC1 → Server
PC1 → PC2
Server1 → Server2

وده مهم جدًا في الـSOC.

ليه؟

لأن المهاجم بعد ما يدخل الشبكة ممكن يبدأ:

Initial Compromise
       ↓
Internal Recon
       ↓
Credential Access
       ↓
Lateral Movement
       ↓
Other Systems

وده كله ممكن يكون:

East-West Traffic

🔥 دي نقطة مهمة جدًا في SOC

ناس كتير تركز على:

Internet ↔ Internal Network

لكن attacker بعد ما يدخل:

Internal Host
     ↓
Internal Host
     ↓
Domain Controller
     ↓
File Server

فلو أنتِ مش بتراقبي:

East-West traffic

ممكن تفوتي جزء كبير من الـattack.

19. أشهر East-West Services

احفظي categories دي:

Directory / Identity

مثل:

LDAP
Kerberos
Active Directory
File Sharing

مثل:

SMB
Infrastructure

مثل:

DNS
DHCP
ARP
Monitoring / Management

مثل:

SNMP
RDP
SSH
Backup / Replication

Traffic بين servers.

20. HTTPS Flow

في حالة TLS inspection:

Client
   ↓
NGFW / Web Proxy
   ↓
Internet Web Server

لكن فعليًا فيه 2 TCP/TLS sessions:

Client ←→ Proxy
Proxy  ←→ Web Server

الـproxy يعمل كأنه:

Server بالنسبة للـclient

وفي نفس الوقت:

Client بالنسبة للـreal web server

وبالتالي يقدر يعمل:

TLS Decryption
      ↓
Inspect Content
      ↓
Allow / Block

وده مفيد جدًا للـSOC لأنه بيزود visibility.

21. External DNS Flow

في corporate network غالبًا الـclient مش بيروح مباشرة للـInternet DNS.

غالبًا:

Client
  ↓
Internal DNS Server
  ↓
Firewall
  ↓
External DNS
  ↓
Internet

والـresponse:

External DNS
      ↓
Firewall
      ↓
Internal DNS
      ↓
Client

وده مهم لأن الـInternal DNS ممكن يكون نقطة ممتازة للمراقبة.

مثلاً:

Host → Internal DNS

وبعدين:

Internal DNS → malicious domain

ده ممكن يساعدنا نكتشف:

Malware / C2 / DNS tunneling

22. SMB + Kerberos

دي مهمة جدًا لو هتكملي Blue Team / SOC.

لما المستخدم يفتح:

\\FILESERVER\MARKETING

مش الموضوع مجرد:

Client → File Server

فيه authentication.

الـflow بشكل مبسط:

User
 ↓
Domain Controller
 ↓
Kerberos
 ↓
Ticket
 ↓
File Server
 ↓
SMB
 ↓
File Share
23. Kerberos ببساطة

لما المستخدم يعمل login:

User
 ↓
Domain Controller / KDC

يحصل على:

TGT — Ticket Granting Ticket

وبعدين لما يريد الوصول إلى service:

FILESERVER

يستخدم الـTGT للحصول على:

Service Ticket

ثم:

Client
   ↓
Service Ticket
   ↓
FILESERVER
   ↓
SMB Session

وبالتالي يقدر يدخل:

\\FILESERVER\MARKETING
🧠 الخلاصة الكبيرة لللاب

أهم فكرة مش إنك تحفظي كل الـpackets.

الفكرة إنك تفهمي:

Logs
 ↓
Alert
 ↓
Need more visibility?
 ↓
Network Traffic Analysis
 ↓
PCAP
 ↓
Packets
 ↓
Headers + Payload
 ↓
Understand what really happened
📒 SOC Notes — احفظي الجزء ده

ممكن تحطيه في الـnotes بتاعتك بالشكل ده:

Network Traffic Analysis
Definition

Network Traffic Analysis (NTA) is the process of inspecting network communications, packets, headers, and payloads to detect suspicious activity and understand what happened during an incident.

Why do we analyze network traffic?
Monitor network performance.
Detect abnormal network behavior.
Inspect suspicious internal/external communications.
Detect malicious activity.
Reconstruct attacks.
Validate SIEM/security alerts.
Investigate data exfiltration.
Investigate malware downloads.
Detect lateral movement.
Logs vs Network Traffic
Logs

Usually provide:

Source
Destination
Port
Protocol
Timestamp
Action
Domain

But may not provide:

Full packet
Payload
Sequence numbers
Fragment offsets
Complete protocol details
PCAP

Can provide:

Headers
Packet metadata
Protocol information
Payload
Sequence numbers
Fragment information
MAC information
TCP/IP Layers
Application
    ↓
Transport
    ↓
Internet
    ↓
Link
Application

Examples:

HTTP
DNS
SMB
SMTP

Can contain:

Headers
Payload
Transport
TCP
UDP

Important TCP fields:

Source Port
Destination Port
Flags
Sequence Number
Acknowledgment Number
Window
Internet

Mainly:

IP

Important fields:

Source IP
Destination IP
TTL
Fragment Offset
Total Length
Link

Examples:

Ethernet
ARP

Important:

Source MAC
Destination MAC
🚨 Attack Detection Mapping
DNS
 ↓
DNS Tunneling / C2 / Exfiltration

TCP Sequence Numbers
 ↓
Session Hijacking / Injection

IP Fragmentation
 ↓
IDS Evasion / Fragmentation Attacks

ARP
 ↓
ARP Poisoning / MITM

HTTP Payload
 ↓
Malware Download / Data Exfiltration
Network Sources
Network Sources
│
├── Endpoint
│   ├── PC
│   ├── Server
│   ├── IoT
│   ├── Printer
│   └── Cloud
│
└── Intermediary
    ├── Firewall
    ├── Router
    ├── Switch
    ├── Proxy
    ├── IDS/IPS
    └── Access Point
Network Flows
North-South
Internet
   ↕
Firewall
   ↕
LAN

Crosses the network boundary.

Examples:

HTTPS
DNS
SSH
VPN
SMTP
RDP
East-West
Host A
  ↕
Host B
  ↕
Server
  ↕
Domain Controller

Stays inside the internal environment.

Very important for:

Lateral Movement
Internal Recon
Credential Attacks
SMB attacks
Kerberos attacks
⭐ أهم حاجة عايزاكي تطلعي بيها من اللاب

لو جالك في الـSOC Alert:

"Host is generating an unusually high number of DNS queries."

متقفليش الـcase على طول.

اعملي:

1. Identify source host
        ↓
2. Examine queried domains
        ↓
3. Check frequency / baseline
        ↓
4. Look for random subdomains
        ↓
5. Check TXT queries
        ↓
6. Investigate DNS responses
        ↓
7. Inspect PCAP if available
        ↓
8. Determine if C2 / tunneling / exfiltration

وده بالضبط الفرق بين:

Alert Triage و Deep Investigation.

الـalert يقولك:

"Something unusual happened."

لكن الـnetwork traffic ممكن يقولك:

"Exactly what happened."
