# Iowa NCCDC Team 4 (aka Team Hacker Club) Writeup

* Hello, Cyber Security and Grid Engineers!
We would like to extend our most sincere thanks to you for assisting us with our power
grid. Truthfully, it has become quite difficult to maintain and keep secure from bad actors and nefarious types, so your addition to the team was a great choice on all fronts!
With it being the coldest part of the year, we want to ensure that our systems are locked
down and stable to provide power to all of our customers at a reliable, sustainable rate, and we need your help to do it. Our software contractors have been on call around the clock to assist in your efforts as well, and will issue patches upon request, so be sure to security test their software! Not that we don’t trust them, because we do, but sometimes, and this is certainly not common, their software has some very slight zero days that affect a small number of our machines, anywhere from 10% to 90% at worst, and, again, we do trust them, but we would love an external audit and some blue team help. We expect some bad actors to be attacking the systems in the not-so-distant future, so audits, upgrades, patches, and documentation need to get done as soon as possible! We thank you, and our customers thank you. 

The blurb above describes the layout of the scenario given to the 2022 Iowa NCCDC Blue-Team's. Teams of 8 (in our case, 6) are invited to compete by Iowa State University to defend a mock-corporate network against an active red team. Teams are scored based on service uptime, network usabilitity, anomalies (capture-the-flag style quetions), intrustion reports, and network documentation. Further, untouched flags pre-planted by blue team also contributed to the score total. It was all of our first time's competing in Iowa State's NCCDC.

# Setup phase:

All blue-team's were given an indetical set of hosts/servers several days prior to the competition. We able to add any servers to the topology that could help us in securing/accessing our network in any way, but we could not remove any servers. The team's this year were given the following servers/hosts and services to protect for this year: Controller GUI/Frontend (SSH, HTTP), Controller Server (SSH, PDCP), Substation (PDCP), three Generators (Power System Health), Billing Server (RDP). All operating systems ran linux except for the billing rdp server.
* maybe talk about how servers interconnect here*

The generators and substations ran an embedded version of linux primarily orientated toward basic management which the option of running a maintence mode that opened an ssh instance that could be connected to. Because of this, our team added an aditional 3 hosts on the network for the purpose of managing the three generators and substations.

Final topology:   
![Pasted image 20220214175233](https://user-images.githubusercontent.com/75512760/156289367-135f2044-84f3-4cf5-83e0-6bc645d8cb5e.png)


We were incredibly restricted with how we could secure all of the linux servers this year. Apt-get was disabled, meaning it was virtually impossible to update any insecure packages. We also had plans prior to the competition to implement a centralized IDS firewall and logging server that was crushed with these restrictions. 

This forced us to handle all firewall rules on the host level. For the linux systems, this meant setting up iptables in accordance with the scored services. For logging, we resorted to the default log files that linux had in place for the scoring services. We backed up these log files for reference during the actual competition.

On the Controller/Frontend, depreciated SSH rules were deleted and other rules were added to improve the stability of the service during the competition.

ALl essential files systems and server configurations were backed up in the case that they were altered/deleted during a red team attack. For Linux systems, this included /etc/, /home/, and scored service configs. Some config files also their permissions limited.

All of us added our flags into their required directories and did not tamper with them per the rules of the competition. This finished off the Setup Phase for Team 4 and we were ready for competition day.

# Competition Day:
### Intro
The competition was held on 2/5, where the red-team phase and start of competition started at 8 am and went until 4 pm. This gave us 8 hours to juggle with red team, flags, anomalies, services, etc. We all met up prior to the competition time and got ready for some red team action!

### Services
Despite our teams inexperience, along with being down two players from the maximum team cap, we actually got the highest service uptime in comparison to all teams at 95.7% availability. We did not often see a whole lot of services going down throughout the 8 hours. Our firewalls, surprisingly, did not bring us down at all throughout the competition as well. Aside from services being universally down among all teams for several checks, we missed some ssh checks due to the misconfiguration of users on the controller server. This was addressed quickly and our ssh was green for the remainder of the competition.


### Lost Flags

On the controller server, we were able to witness some activity that indicated toward red teams steps toward capturing our flags.

![unknown](https://user-images.githubusercontent.com/75512760/161786000-b1a55eff-48f3-4311-8136-270f111356e7.png)

Early in the competition around 9:30, many instances of failed login attempts were captured in the ssh log file. We can see that the group permissions established seemed to have worked in our setup phase given these failed login attempts. Looking closley at the log file, we can see that the .168 IP has an unauthorized login attempt for the admin baggins.mickel.

In the debrief after the competition, red team mentioned that the one of the essential controller server services (PDCP) had a backdoor to an administrator account within the service. Our best guess is that they took advantage of this early on in the competition and captured one of the flags from there. 

![UnAuthorizedLogin](https://user-images.githubusercontent.com/75512760/161785706-e8046cf2-3df7-4ed2-8824-1e5f32f1a5d4.png)

A little after 1:30, we found that an unauthorized user, chris, was attemepting to authenticate as sudo. After seeing these logs, we quickly removed chris from the /etc/passwd file, but was unable to view any indiciation of activity he might have done. Shortly after this event, the second flag was lost on the controller server. We were able to retrieve partial credit back from our lost flags after giving the red-team our reasoning for how they were captured in the first place utalizing log information and login history tools built into Linux.

### Anomalies

*Refer to Anomalies folder for individual writeups*

### What worked, What didn't 

##### The Good:

Firewall rules not bringing us down throughout the competition was quite the surprise. This is often an aspect of ccdc, from my experience, that brings team's down a decent chunk of points. It does help that we were able to set these up in the set-up phase rather than in an active competition. Out service time being the highest among the other teams was a great aspect we saw at the end of the competition. 

Communication among the team was also great. We were able to divide up anomalies based on whoever's services were functining correctly. This also applied to our flag appeal times as well, since we were able to submit all of them on time with proper responses.

Anomaly submissions were also great. Since some of our members had prior Capture-the-flag experience, decrypting the files that Iowa gave us this year was not too big of a hastle. The flexseal anomaly was particularly interesting, more information on that in the Writeups folder...

Finally, we were able to keep our flags secured on half of the machines (Generator, Substation, Billing). Since these flags were worth a lot of points and were given to us at the start of the competition, keeping them safe was vital to securing our third place position. 

##### The Bad:

Establishing some sort of centralized form of logging this year was incredibly difficult given our limits with "apt-get". This meant that getting organized log updates for regularly scheduld "Intrusion Reports" was disorganized and difficult. If our team was able to find some sort of neat cat string output prior to the Competition, that would have helped us the receive a lot more points on these reports. Around 10 or so log entires were being added to these files every 5 mintues. Because of this, finding what we wanted wasn't particularly easy. 

Our usability score also was not the best during the competition. This was a score given to teams throughout the competition in regard to the usability of the actual website, which graded basic operations. Since it was our first time competiting, these came unannounced and unexpectedly. It also didn't help that that, after the first report score came out, the second was already locked in for grading. There was, quite literally, zero minutes we had available to troubleshoot this. Having a spare host on the topology that mimicked an end user would have helped us in seeing what the current usability was like, rather than having to wait for these reports to be submitted.

Though we did get a competitive anomaly score, It could have been a lot better. A decent bulk of the anomalies involved outputting netcat prompts into a script to solve automatically. Though most of the people with programming knowledge knew the logic of these operations, the process of receiving/sending information through netcat was not easy. Practice with these technologies, along with learning to write adaptable scripts, will prove to be useful in the future. 

Finally, our process of securing our system from planted flags were flawed. There were alternative measure that we could have used to supress the red-teams ability to plant flags that we were unable to execute in the given amount of pre-competition time which ended up hurting us later during the competition.

### Conclusion

Thank you to Iowa NCCDC for a great competition! It was exciting seeing us get 3rd place despite it being a first time of all of us on the team and we learned a lot about the structure of a CCDC competition. We are looking forward to next year!

*Special Thanks to the team:

George and Yusuf (Generators), Petar (Substation), Aggie (Billing),  Mateusz (Controller Server),  Michael (Captain, Controller Server)

Writeup by Michael and George, Anomaly entries by Michael, George, and Yusuf



