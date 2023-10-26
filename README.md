# Storm-Botnet-Forensic-Research-Report

![image](https://github.com/MikolajMroz/Storm-Botnet-Forensic-Research-Report/assets/98950042/a5795c65-209f-4b45-97e2-253831ae08d8)


## Introduction
Microsoft London, a subsidiary of the world-renowned Microsoft firm, have commissioned a consultation looking into the recently resurfaced threat of the “Storm” botnet. This report aims to investigate the history and inner workings of the virus as well as the various processes required to mitigate its impact on modern computer systems. This will initially look at detailing the various Digital Forensics Framework (DFF) steps tailored for this re-emerging threat, delving into the possible data sources where the threat can be detected, the potential impact both physical and financial, as well as the likelihood of effective countermeasures. 
A critical analysis of the technology behind the Storm botnet will also be discussed to weigh the likelihood of shutting it down using currently available tools and techniques, investigating the causes of its previous fall in popularity and the feasibility of reusing and modernising the previously successful methods.

The investigation will follow the standard Digital Forensics Framework, preparing the client with all the information necessary to understand the tools and techniques that will be used during a practical examination of their systems. The goal of this investigation is to create a strategy to prevent the virus from affecting Microsoft London’s infrastructure, also deterring future attacks of a similar nature using appropriate enterprise tools and tried-and-tested methods.

## Background
The ‘Storm’ Botnet first emerged around January of 2007 from an infectious email spread around from user to user (Appendix 1A). To garner as many clicks from its victims as possible, the email was typically titled like a provocative and attention-grabbing news article such as “230 dead as storm batters Europe”, hence its name. This proved to be an effective method of attracting recipients to click on the email, as one to fifty million PCs were estimated to be part of the botnet (Naughton, 2007). The composition of the virus is quite unique in that it functions as a hybrid of multiple common types of computer virus: unsuspecting users would be coerced into opening the email by its title and click on the fake news link - a form of phishing - which would then install a binary onto the computer to connect itself to the botnet using the hard-coded data in this file. Once it has been installed and the computer has been compromised, it would act as a worm and self-replicate by sending more emails to the victims’ contacts, repeating the cycle. 

Each infected PC would act as a “Zombie” device, connected peer-to-peer (P2P) via the Overnet/eDonkey protocol to other infected computers which can be made to act as one single entity. Botnets such as this are typically used by attackers to steal large amounts of personal data from their victims which can be sold for huge sums of money on the black market. It was uncovered later in October of the same year that chunks of the botnet were being sold in secret, allowing them to use hundreds and thousands of computers to do their bidding, typically done so to produce large DDOS (Direct Denial of Service) attacks to bring down company infrastructure and services (Naraine, 2007).

Storm also uses obfuscation techniques to make itself harder to detect and remove. The most notable of these techniques are its abilities to lie dormant for extended periods of time on the computer’s storage, allowing it to quickly go into hiding after performing an attack. Each device on the botnet is connected peer to peer which works in tandem with its grouped structure, often compared to an ant colony where each device has a separate duty to perform for the attacker. Some computers will be used to spread the virus further, and others will act as control centres with the duty ready to be passed onto another device if it ever gets shut down (Schneier, 2007). The virus was also built to be very lightweight, making it difficult to detect its presence or any abnormal behaviour and makes use of Fast Flux, frequently changing its IP and DNS information to make itself very difficult to trace and counter (Vuong & Alam, 2010).

This new 2022 variant of Storm (Storm 2022) acts in a similar fashion to the one released in 2007, with a couple major noted differences. Firstly, it can target new versions of Windows as well as mobile devices, suggesting it has been modernised to impact as many people as possible using the latest technology. Storm 2022 also propagates through local networks, not just through email client worms, making it especially dangerous for larger enterprise networks. Assuming this version also makes use of features from the 2007 release, this modernised Storm virus has the potential to cause considerable damage to virtual infrastructure and affect the physical world if a solid strategy to counter it is not put into effect. 

## Network Investigation
As no specific network diagram or topology has been provided by the client, this investigation analyses the potential data sources and effects of a botnet infection on a typical small business network. This includes looking into typical network devices such as servers, routers, computers, firewalls, mobile devices, and any connected intrusion detection or prevention systems (Appendix 1B).

## Identification of Sources - Storage
By researching the history and behaviour of the virus, several high and low-level sources could be identified. Storm’s use of a P2P structure means most evidence will be found through network traffic analysis, though the virus has components that may allow it to be found on the applications found on the computer system in places like storage and memory.
### Computer Drives
Once of the best sources of evidence would be any affected hard drives, where the virus may be saved. 
### Computer Memory (RAM)
The only known instance of the worm in memory is the presence of the services.exe process, which it uses to communicate with the rest of its bot network.
### Emails
The Storm worm botnet is known to have propagated through emails, making them a prime source of information on the subject and to validate the virus’ presence and subsequently track its spread. 

### Mobile Phones
Mobile Phones can store a large amount of relevant information on their flash memory (equivalent to PC RAM) and internal and external storage where any malicious files may be saved. More relevant to this investigation however, messages and contacts can be retrieved from the phone’s SIM card and further information can be gathered from the service provider in the form of call logs, message logs, and location data. This can help determine if the worm spreads through text messages as well or just emails, and its undocumented impact on phone storage and memory can be investigated.

## Identification of Sources – Internet Devices
One of the biggest signs of an ongoing botnet infection is abnormal network traffic. This can range from anything from an increase in incoming or outgoing traffic, high server CPU load, and abnormal packets being accepted into the network. Particularly in the case of a P2P botnet, analysing abnormal network behaviour is paramount for the success of the investigation.

### Routers
The contents of router RAM contain vital information about not only the setup of the device and whether it was correctly set up to handle the attack, but also stores information about the TCP and UDP traffic that passed through the router, routing tables, user accounts, and processor routines. 

### Intrusion Detection/Prevention Systems (IDS/IPS)
IDS and IPS systems both make use of alerts to inform network administrators of any ongoing anomalous behaviour on the network. The source and destination of flagged packets can be investigated, giving clues as to which devices may be affected or targeted by the virus.

### Internet Packets
Storm makes use of the Overnet protocol to communicate with peers. This protocol as well as any outstanding packet sources can be investigated in real time, capturing baseline network activity and comparing it to anomalous network activity on an individual packet level.

### Honeypots
Honeypot devices, or in other words, computers that attempt to draw the virus to them in a controlled manner for further analysis, are a very effective way of providing the investigation with the necessary information about the inner workings of the re-emerging botnet. This is not a standard business network device and would require setup prior to the investigation.

## Acquisition
Once the forensic investigation has formally begun, the volatile sources considered in the section above must have their relevant RAM data exported onto forensically secure storage, ready for investigation in the laboratory. This is to ensure that the data stored there at the beginning of the investigation is not lost after the devices are shut off or restarted. Mobile phones will need to be confiscated in a tamper-proof forensic bag in order to have their RAM dumps taken in the lab.

After the RAM data has been gathered, the next stage of the acquisition process can begin - live network capture and honeypot setup. The honeypot device will be set up on an external-facing part of the network (such as the DMZ) to attract the botnet, as it not only propagates through emails but spreads across networks as well. It is because of this that any unnecessary parts of the network should be shut off from the internet to prevent the botnet from spreading if they have not been infected already. Once sufficient evidence has been gathered, the honeypot data will be exported, and the device removed from the network.

If the business network does not already make use of an IDS or Packet Sniffer that saves information about all the packets that pass through (like Snort or Wireshark), a baseline reading will need to be taken of standard network traffic before the network packet investigation begins. This will then be compared to network traffic with the honeypot set up, capturing anomalous data from the internet headed towards the honeypot which will be exported onto forensically safe drives, and compared and investigated offsite.

Finally, digital images of the hard drives on the network (PC, Server, Mobile Phone storage) will be collected with the use of a forensic imaging tool, saved on forensically secure drives, and investigated in the lab to look for signs of infection or botnet activity. It is at this point that server logs and router data will be exported as well.

## Preservation 
A number of steps must be performed in order to preserve the integrity of the data from this investigation. 
Firstly, a Chain of Custody document will be produced to ensure every handler of the confiscated phone as well as the forensic images and logs stored on the forensic drives is authorized to do so and has their actions recorded in the relevant documents. An agreement form will be created for the client to sign to allow a full investigation into their network should they choose this approach.

An MD5 hash of each gathered image and log file will be taken prior to analysis to ensure integrity of the gathered data, only working on read-only, unalterable copies. Each time these files are analysed or otherwise opened; the hash will be checked against the original to make sure no changes were made that would void the evidence collected. 
Any hard drives and storage mediums used throughout the investigation, particularly those used to store the gathered information, will be forensically wiped and formatted appropriately before anything is saved on them to prevent any lingering data on them from interacting with the data taken from the botnet investigation.

## Analysis 
To understand the acquired data, in-depth analysis must be undertaken through the use of various tools and techniques.
During Storm’s first launch, it links up to a number of peer-to-peer hosts through the data hard coded into its initial state which downloads further executable files, named game0.exe through to game5.exe, each of which has a different function to perform as the virus communicates with the botnet at each stage (Stewart, 2007).
game0.exe 	-	Backdoor
game1.exe	-	SMTP Relay
game2.exe	-	Email Address Stealer
game3.exe	-	Email Virus Spreader
game4.exe	-	DDoS Attack tool
game5.exe 	-	Updated Storm Copy Dropper

The virus is also known to store its code in system32/wincom.sys via a kernel rootkit, which then transfers information to the services.exe system process on Windows houses the code required to link the device to the rest of the botnet. 
Using the information above, it is possible to locate these files using digital image and RAM dump forensics, one method being brute force searching. This is done by searching for particular file names and extensions and can easily be automated through tools like GREP and Autopsy. For this investigation, the main search terms for looking through storage mediums will be “game0.exe – game5.exe” and “services.exe”, the details and inner workings of which can be analysed and noted.
The most significant part of analysis comes from the captured network packets from the honeypot system, IDS, and other network devices. By finding the source addresses of any attacks and recognising a pattern in their payload data, it is possible to remove any unnecessary or unorthodox traffic from the displayed packets through the use of Wireshark filters. This not only helps make the gathered information much easier to investigate, whether it is done manually or through software, but it helps visualise the magnitude of malicious packets entering the network.

While analysing the network traffic, there are specific patterns that will be studied that signify the presence of this botnet. 
-	Constantly changing source IP addresses, suggesting Storm’s signature use of  Fast Flux to repeatedly change its network information, DNS records, and proxies (Mukamurenzi, 2008). 
-	The use of TCP and UDP to send abnormal amounts of traffic through ports 20/21 (File transfer), 25 (Mail) and UDP traffic, both of which can be filtered and shown in WireShark.
-	UDP eDonkey packets containing two hashes, which the botnet uses to communicate with (Appendix 1C).
-	High bandwidth usage, which Intrusion Detection Systems are quick to flag.
-	SMTP traffic containing links to unfamiliar sites, though it is standard to encrypt emails nowadays and this information may be found elsewhere, such as an exported list of emails.

## Discussion
Overall, the content of this report effectively outlines the potential data sources in the event of a botnet infection and guides the client through the steps they should take in a true-to-life forensic investigation. However, due to the lack of information from the client regarding the structure of the network and currently employed software, the report remains fundamentally limited in its scope and practicality, giving only a glimpse into the work that must be performed in a full forensic investigation. This also means that a couple of liberties had to be taken, particularly with the structure of the network, which means that the chosen network structure may not perfectly fit that of the client and may be of limited use at this stage. 

Regardless, there are some outstanding aspects of note with the chosen framework and techniques in relation to the Storm’s tendency to obscure itself from searches and captures. The process of capturing traffic originating from the botnet is relatively straightforward, including gathering data from IDS, IPS, honeypots, and general internet traffic. The difficulty comes from deciphering and understanding the source and payload of which is altered frequently by the greater botnet, keeping in mind that not every botnet will behave in the same way as any other. This equally applies to the data gathered from storage devices and memory, which, while stored in the exact same place as always in this example, will most likely house different data (IP addresses, ports, payloads, malicious code) with each different botnet or even version of Storm and brings its own challenges.

The most effective way to prevent a botnet attack will always be to follow standard defence-in-depth procedures for large enterprises. This includes shutting down all ports on the network until they are absolutely required for use, keeping software up to date (preferably on an update schedule), and closely monitoring the internet traffic that flows through the network as demonstrated with Intrusion Detection Systems and packet analysis tools like Wireshark. It is also vital to have a plan ready in the event of an attack, also called an Incident Response Plan to ensure all employees know exactly what to do and who to go to in a cyber emergency. For best results, it is recommended to use specific anti-botnet software solutions, more of which are appearing with each year.

Though the strategy outlined in this report is best suited for investigating the impact of a botnet infection and understanding the potential data sources, academic research is currently underway into bespoke botnet prevention methods to prevent a repeat of Storm’s success in 2007 and shows great promise. A report done by the students at University of Michigan clearly determines the most important aspects of P2P prevention being the distinction between standard internet traffic and that of Storm, suggesting machine learning as a solution (Zeng & Shin, 2009). A recent article from the journal “Mathematical Problems in Engineering” discusses a new, comprehensive evaluation method for botnet detection (Xing, Shu, Zhao, Li, & Guo, 2021), and finally, Thangapandiyan and Anand propose an efficient botnet detection system specifically built for P2P botnets (2016) to great success.
While the general steps taken throughout most digital forensic investigations remain the same, there is little information available about the process of discovery and analysis in relation to botnets under forensics, which impacts the practical side of the standard forensic process. In other words, P2P botnets require further academic analysis to help create a more robust P2P botnet-centric forensic methodology, considering their unique polymorphic properties and lightning-fast spread through networks.

## Conclusion
In conclusion, the Storm 2022 variant has the potential to cause widespread damage across the client’s network if the correct precautionary measures are not taken. The virus has new, modernised features specifically targeted towards impacting modern businesses and technologies which must be accounted for when implementing a relevant defence, particularly on the internet-facing aspects of the network which will be the client’s primary concern when implementing the proposed defence strategy. 
Work is currently underway around the world to improve the currently limited availability of anti-botnet tools which aim to deter their use by attackers and improve the safety of networks around the world, though the subject of P2P botnets considered in the forensic process is currently lacking in development.

## References
Mukamurenzi, N. M. (2008). Storm Worm: A P2P Botnet. Trondheim: Norwegian University of Science and Technology.

Naraine, R. (2007, October 15). Storm Worm botnet partitions for sale . Retrieved from ZDNET: https://www.zdnet.com/article/storm-worm-botnet-partitions-for-sale/

Naughton, J. (2007, October 21). In millions of Windows, the perfect Storm is gathering. Retrieved from The Guardian: https://www.theguardian.com/business/2007/oct/21/1

Schneier, B. (2007, October 17). The Storm Worm. Retrieved from Schneier on Security: https://www.schneier.com/blog/archives/2007/10/the_storm_worm.html

Stewart, J. (2007, February 7). Storm Worm DDoS Attack. Retrieved from Secureworks: https://www.secureworks.com/research/storm-worm

Thangapandiyan, M., & Ananad, P. R. (2016). An efficient botnet detection system for P2P botnet. Chennai: IEEE.

Vuong, S., & Alam, M. (2010, June 9). Advanced Methods for Botnet Intrusion Detection Systems. Intrusion Detection Systems, 55-80. Retrieved from InTechOpen: https://www.intechopen.com/chapters/14357

Xing, Y., Shu, H., Zhao, H., Li, D., & Guo, L. (2021). Survey on Botnet Detection Techniques: Classification, Methods, and Evaluation. Mathematical Problems in Engineering, 24.

Zeng, Y., & Shin, K. G. (2009). On Detection of Storm Botnets. Ann Arbor: University of Michigan.

## Appendices

Appendix 1A - A diagram of a typical P2P botnet. Note the lack of a centralized control point.
![image](https://github.com/MikolajMroz/Storm-Botnet-Forensic-Research-Report/assets/98950042/cbb098f4-599e-4774-a589-ceb036042379)

Appendix 1B - An example small business network 
![image](https://github.com/MikolajMroz/Storm-Botnet-Forensic-Research-Report/assets/98950042/ec359bd4-767e-4ac4-bd02-95ccf019cfa5)

Appendix 1C - eDonkey transmission from Storm (via https://www.secureworks.com/research/storm-worm) 
![image](https://github.com/MikolajMroz/Storm-Botnet-Forensic-Research-Report/assets/98950042/2ae5af17-052f-4b1e-b9f8-4515b3490586)


