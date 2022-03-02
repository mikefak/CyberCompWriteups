# Iowa NCCDC Team 4 (aka Team Hacker Club) Writeup - Template

* Hello, Cyber Security and Grid Engineers!
We would like to extend our most sincere thanks to you for assisting us with our power
grid. Truthfully, it has become quite difficult to maintain and keep secure from bad actors and nefarious types, so your addition to the team was a great choice on all fronts!
With it being the coldest part of the year, we want to ensure that our systems are locked
down and stable to provide power to all of our customers at a reliable, sustainable rate, and we need your help to do it. Our software contractors have been on call around the clock to assist in your efforts as well, and will issue patches upon request, so be sure to security test their software! Not that we don’t trust them, because we do, but sometimes, and this is certainly not common, their software has some very slight zero days that affect a small number of our machines, anywhere from 10% to 90% at worst, and, again, we do trust them, but we would love an external audit and some blue team help. We expect some bad actors to be attacking the systems in the not-so-distant future, so audits, upgrades, patches, and documentation need to get done as soon as possible! We thank you, and our customers thank you. 

The blurb above describes the layout of the scenario given to the 2022 Iowa NCCDC Blue-Team's. Teams of 8 (in our case, 6) are invited to compete by Iowa State University to defend a mock-corporate network against an active red team. Teams are scored based on service uptime, network usabilitity, anomalies (capture-the-flag style quetions), intrustion reports, and network documentation. Further, untouched flags pre-planted by blue team also contributed to the score total. It was all of our first time's competing in Iowa State's NCCDC.

*Brief desc of competition*


# Setup phase:
*Describe how we prepared for the comp given the environment*

All blue-team's were given an indetical set of hosts/servers several days prior to the competition. We able to add any servers to the topology that could help us in securing/accessing our network in any way, but we could not remove any servers. The team's this year were given the following servers/hosts and services to protect for this year: Controller GUI/Frontend (SSH, HTTP), Controller Server (SSH, PDCP), Substation (PDCP), three Generators (Power System Health), Billing Server (RDP). All operating systems ran linux except for the billing rdp server.
* maybe talk about how servers interconnect here*

The generators and substations ran an embedded version of linux primarily orientated toward basic management which the option of running a maintence mode that opened an ssh instance that could be connected to. Because of this, our team added an aditional 3 hosts on the network for the purpose of managing the three generators and substations.

Final topology:   
![[Pasted image 20220214175233.png]]


We were incredibly restricted with how we could secure all of the linux servers this year. Apt-get was disabled, meaning it was virtually impossible to update any insecure packages. We also had plans prior to the competition to implement a centralized IDS firewall and logging server that was crushed with these restrictions. 

This forced us to handle all firewall rules on the host level. For the linux systems, this meant setting up iptables in accordance with the scored services. For logging, we resorted to the default log files that linux had in place for the scoring services. We backed up these log files for reference during the actual competition.

On the Controller/Frontend, depreciated SSH rules were deleted and other rules were added to improve the stability of the service during the competition.

ALl essential files systems and server configurations were backed up in the case that they were altered/deleted during a red team attack. For Linux systems, this included /etc/, /home/, and scored service configs. Some config files also their permissions limited.

All of us added our flags into their required directories and did not tamper with them per the rules of the competition. This finished off the Setup Phase for Team 4 and we were ready for competition day.

# Competition Day:
### Intro
The competition was held on 2/5, where the red-team phase and start of competition started at 8 am and went until 4 pm. This gave us 8 hours to juggle with red team, flags, anomalies, services, etc. We all met up prior to the competition time and got ready for some red team action!

### Services
Despite our teams inexperience, along with being down two players from the maximum team cap, we actually got the highest service uptime in comparison to all teams at 95.7% availability. We did not often see a whole lot of services going down throughout the 8 hours. Our firewalls, surprisingly, did not bring us down at all throughout the competition. 

One of the greates things that brought us down was 

### Lost Flags
*Describe how we lost what flags and which ones were planted*
*
### Anomalies

*Refer to Anomalies folder for individual writeups*

### What worked, What didn't 
*Explain things we should and should not do next year*

### Conclusion


*Special Thanks to the team:

George and Yusuf (Generators), Petar (Substation), Aggie (Billing),  Mateusz (Controller Server),  Michael (Captain, Controller Server)

Writeup by Michael, Anomaly entries by George



