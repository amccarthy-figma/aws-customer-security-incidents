## Background

Security is an exercise in managing risk. Reviewing the common root causes of security incidents is an effective way to guide prioritized remediation efforts.

This repository seeks to index all publicly disclosed AWS customer security incidents with a known root cause. It will exclude incidents involving exposed data stores (e.g S3 bucket leaks, exposed managed or hosted databases).
Those incidents are already well understood, and examples can be found cataloged in places like [nagwww's s3-leaks repo](https://github.com/nagwww/s3-leaks), [upguard's reports](https://www.upguard.com/breaches), [hackmeggedon's annual rollup reports (2022)](https://www.hackmageddon.com/2022/02/21/leaky-buckets-in-2022/) and [Corey Quinn's LWIAWS](https://www.lastweekinaws.com) S3 Bucket Negligence Award.

It also excludes incidents impacting individuals, such as the periodic reports of cryptomining due to compromised credentials. [1](https://vertis.io/2013/12/16/unauthorised-litecoin-mining/) [2](https://readwrite.com/amazon-web-services-hack-bitcoin-miners-github/) [3](http://www.nvenky.in/2014/03/bitcoin-mining-closed-my-aws-account.html)

## Other Cloud Threat Trend Analysis

GCP's [November 2021 Cloud Threat Intelligence report](https://services.google.com/fh/files/misc/gcat-threathorizons-full-nov2021.pdf) found that:
> Of 50 recently compromised GCP instances, 86% of the compromised Google Cloud instances were used to perform cryptocurrency mining

Their [July 2022 report](https://services.google.com/fh/files/blogs/gcat_threathorizons_full_july2022.pdf) also highlights that:
> the most common attack vectors used across cloud providers was brute force of cloud services that are exposed to the internet and have a weak or default password ... close behind brute force attacks was the exploitation of vulnerable software

[Rich Mogull's](https://twitter.com/rmogull) summary of [a 2022 AWS re:Inforce session on ransomware](https://www.firemon.com/what-you-need-to-know-about-ransomware-in-aws/) highlight's that ransomware is a common problem for AWS customers, stemming from two common exploit vectors:
> A traditional ransomware attack against instances in AWS. The attacker compromises an instance (often via phishing a user/admin, not always direct compromise), then installs their malware to encrypt the data and spread to other reachable instances. This is really no different than ransomware in a data center since it doesn’t involve anything cloud-specific.

> The attacker copies data out of an S3 bucket and then deletes the original data. This is the most commonly seen cloud native ransomware on AWS.

## Talks

The initial data was collected for a talk at BSidesCT 2020: _Learning from AWS (Customer) Security Incidents_  [slides here](https://speakerdeck.com/ramimac/learning-from-aws-customer-security-incidents)
A follow up talk was given at OWASP DevSlop in May 2022. [video](https://www.youtube.com/watch?v=JBUgAXvcObU), [slides](https://speakerdeck.com/ramimac/learning-from-aws-customer-security-incidents-2022)

### A Note on Blameless Postmortems

This repository is in no way intended as a criticism of the listed companies. In the spirit of blameless postmortems [<sup>1</sup>](#1), our goal is to learn from incidents without an atmosphere of blame.

## Catalog of AWS Customer Security Incidents

A repository of breaches of AWS customers

| Name  | Date | Root Cause | Escalation Vector(s) | Impact | Link to details|
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| Code Spaces  | 2014, June  | AWS Console Credentials (Phishing?) | Attacker created additional accounts/access keys | Wiped S3 buckets, EC2 instances, AMIs, EBS snapshots | [Hacker puts code spaces out of business](https://threatpost.com/hacker-puts-hosting-service-code-spaces-out-of-business/106761/)  |
| BrowserStack  | 2014, November  | Shellshock on exposed, outdated prototype machine | Access keys on server, used to create IAM user, create EC2, and mount backup | Steal user data and email users | [BrowserStack analysis](http://archive.today/rsmmS)  |
| DNC Hack by the GRU  | 2016, June  | Unknown, test clusters breached | EC2 Snapshots copied to attacker AWS accounts | Tableau and Vertica Queries | [DEMOCRATIC NATIONAL COMMITTEE v. THE RUSSIAN FEDERATION](https://www.politico.com/f/?id=00000168-6161-de11-af7d-ef7327ea0000)  |
| DataDog  | 2016, July  | CI/CD AWS access key and SSH private key leaked | Attacker attempted to pivot with customer credentials | 3 EC2 instances and subset of S3 buckets | [2016-07-08 Security Notice](https://web.archive.org/web/20201128071102/https://www.datadoghq.com/blog/2016-07-08-security-notice/)  |
| Uber | 2016, October  | Private Github Repo with AWS credentials | N/A | Names and driver’s license numbers of 600k drivers, PII of 57 million users| [Uber concealed cyberattack ...](https://web.archive.org/web/20210824171652/https://www.bloomberg.com/news/articles/2017-11-21/uber-concealed-cyberattack-that-exposed-57-million-people-s-data) |
| Lynda.com | 2016, December  | Private Github Repo with AWS credentials | N/A | User data for 9.5m users, attempted extortion | [2 Plead Guilty in 2016 Uber and Lynda.com Hacks](http://archive.today/oU2ZL) |
| OneLogin | 2017, May  | AWS keys | Created EC2 instances | Accessed database tables (with encrypted data) | [May 31, 2017 Security Incident](https://web.archive.org/web/20210620180614/https://www.onelogin.com/blog/may-31-2017-security-incident) |
| Politifact | 2017, October  | "Misconfigured cloud computing server" | N/A | Coinhive cryptojacking | [Hackers have turned Politifact’s website into a trap for your PC](https://web.archive.org/web/20200806102838/https://www.washingtonpost.com/news/the-switch/wp/2017/10/13/hackers-have-turned-politifacts-website-into-a-trap-for-your-pc/) |
| DXC Technologies | 2017, November  | Private AWS key exposed via Github | 244 EC2 instance started | Cryptomining | [DXC spills AWS private keys on public GitHub](https://web.archive.org/web/20210228215919/https://www.theregister.com/2017/11/14/dxc_github_aws_keys_leaked/) |
| LA Times  | 2018, February  | S3 global write access | N/A | Cryptojacking | [Coinhive cryptojacking added to homicide.latimes.com](https://web.archive.org/web/20210413201832/https://www.tripwire.com/state-of-security/security-data-protection/la-times-website-cryptojacking-attack/) |
| Tesla | 2018, February  | Globally exposed Kubernetes console, Pod with AWS credentials | N/A | Cryptojacking | [Hack Brief: Hackers Enlisted Tesla's Public Cloud to Mine Cryptocurrency](https://www.wired.com/story/cryptojacking-tesla-amazon-cloud/) |
| imToken | 2018, June  | Email account compromise | Reset AWS account password | Minimal customer device data | [ Disclosure of Security Incidents on imToken ](https://archive.ph/bRjXi) |
| Voova  | 2019, March  | Stolen credentials by former employee  | N/A | Deleted 23 servers |  [Sacked IT guy annihilates 23 of his ex-employer’s AWS servers](https://nakedsecurity.sophos.com/2019/03/22/sacked-it-guy-annihilates-23-of-his-ex-employers-aws-servers/)  |
| Capital One  | 2019, April  | "Misconfigured WAF" that allowed for a SSRF attack  | Over-privileged EC2 Role | 100 million credit applications |  [A Technical Analysis of the Capital One Cloud Misconfiguration Breach](https://www.fugue.co/blog/a-technical-analysis-of-the-capital-one-cloud-misconfiguration-breach)  |
| JW Player | 2019, September  | Weave Scope (publicly exposed), RCE by design | N/A | Cryptojacking | [How A Cryptocurrency Miner Made Its Way onto Our Internal Kubernetes Clusters](https://web.archive.org/web/20210828044334/https://medium.com/jw-player-engineering/how-a-cryptocurrency-miner-made-its-way-onto-our-internal-kubernetes-clusters-9b09c4704205) |
| Malindo Air | 2019, September  | Former employee insider threat | N/A | 35 million PII records | [ Malindo Air: Data Breach Was Inside Job](https://www.infosecurity-magazine.com/news/malindo-air-data-breach-was-inside/) |
| Imperva | 2019, October  | “Internal compute instance” globally accessible, “Contained” AWS API key | N/A | RDS snapshot stolen | [Imperva Security Update](https://web.archive.org/web/20210620143023/https://www.imperva.com/blog/ceoblog/) |
| Cameo | 2020, February  | Credentials in mobile app package | N/A | Access to backend infrastructure, including user data | [Celeb Shout-Out App Cameo Exposes Private Videos and User Data](https://www.vice.com/en/article/akwj5z/cameo-app-exposed-private-videos-user-data-passwords) |
| Open Exchange Rates | 2020, March | Third-party compromise exposing access key | N/A | User database | [Exchange rate service’s customer details hacked via AWS](https://nakedsecurity.sophos.com/2020/03/20/exchange-rate-services-customer-details-hacked-via-aws/) |
| Live Auctioneers | 2020, July | Compromised third party software granting access to cloud environment | N/A | User database, including MD5 hashed credentials | [Washington State OAG -  Live Auctioneers](https://www.atg.wa.gov/live-auctioneers/) |
| Twilio | 2020, July  |S3 global write access | N/A | Magecart[<sup>2</sup>](#2) | [Incident Report: TaskRouter JS SDK Security Incident](https://web.archive.org/web/20210813010417/https://www.twilio.com/blog/incident-report-taskrouter-js-sdk-july-2020) |
| Natures Basket responsible disclosure | 2020, July  | Hard-coded root keys in source code exposed via public S3 bucket | N/A | N/A | [GotRoot! AWS root Account Takeover](https://web.archive.org/web/20200825004529/https://medium.com/@gchib/naturesbasket-aws-root-account-takeover-e4aa5c5e95e1) |
| Cryptomining AMI | 2020, August  | Windows 2008 Server Community AMI | N/A | Monero miner | [Cryptominer Found Embedded in AWS Community AMI](https://web.archive.org/web/20210625192906/https://www.darkreading.com/cloud/cryptominer-found-embedded-in-aws-community-ami/d/d-id/1338713/) |
| Animal Jam | 2020, November | Slack compromise exposes AWS credentials | N/A | User database | [Kids' gaming website Animal Jam breached](https://web.archive.org/web/20210122070047/https://www.theregister.com/2020/11/12/animal_jam_breached/) |
| Cisco | 2020,  December  | Former employee with AWS access 5 months post-resignation | N/A | Deleted \~450 EC2 instances | [Former Cisco engineer sentenced to prison](https://web.archive.org/web/20210304053727/https://www.zdnet.com/article/former-cisco-engineer-sentenced-to-prison-for-deleting-16k-webex-accounts/) |
| Juspay | 2021, January | Compromised old, unrecycled Amazon Web Services (AWS) access key | N/A | Masked card data, email IDs and phone numbers | [Data from August Breach of Amazon Partner Juspay Dumped Online](https://web.archive.org/web/20210127001214/https://threatpost.com/data-from-august-breach-of-amazon-partner-juspay-dumped-online/162740/) |
| 20/20 Eye Care Network and Hearing Care Network | 2021, January | Compromised credential | N/A | S3 buckets accessed then deleted | [20/20 Eye Care Network and Hearing Care Network notify 3,253,822 health plan members of breach that deleted contents of AWS buckets](https://www.databreaches.net/20-20-eye-care-network-and-hearing-care-network-notify-3253822-health-plan-members-of-breach-that-deleted-contents-of-aws-buckets/) |
| Sendtech | 2021, February | (Current or former employee) Compromised credentials | Created additional admin account | Accessed customer data in S3 | [PERSONAL DATA PROTECTION COMMISSION Case No. DP-2102-B7884]https://web.archive.org/web/20220923025502/https://www.pdpc.gov.sg/-/media/Files/PDPC/PDF-Files/Commissions-Decisions/Decision---Sendtech-Pte-Ltd---220721.ashx?la=en) |
| LogicGate | 2021, April | Compromised credentials | N/A | Backup files in S3 stolen | [Risk startup LogicGate confirms data breach](https://web.archive.org/web/20210519233848/https://techcrunch.com/2021/04/13/logicgate-risk-cloud-data-breach/) |
| Ubiquiti | 2021, April | Compromised credentials from IT employee Lastpass (alleged former employee insider threat) | N/A | root administrator access to all AWS accounts, extortion | [Ubiquiti All But Confirms Breach Response Iniquity](https://web.archive.org/web/20210731152054/https://krebsonsecurity.com/2021/04/ubiquiti-all-but-confirms-breach-response-iniquity/) |
| Uran Company | 2021, July | Compromised Drupal with API keys | N/A | Cryptomining | [Clear and Uncommon Story About Overcoming Issues With AWS](https://topdigital.agency/clear-and-uncommon-story-about-overcoming-issues-with-aws/) |
| redoorz.com | 2021, September | Access Key leaked via APK | N/A | Customer database stolen | [PERSONAL DATA PROTECTION COMMISSION Case No. DP-2009-B7057](https://web.archive.org/web/20211130202805/https://www.pdpc.gov.sg/-/media/Files/PDPC/PDF-Files/Commissions-Decisions/Decision---Commeasure-Pte-Ltd---15092021.pdf?la=en) |
| HPE Aruba | 2021, October | Unknown exposure of Access Key | N/A | Potential access to network telemetry and contact trace data | [Aruba Central Security Incident](https://www.arubanetworks.com/support-services/security-bulletins/central-incident-faq/) |
| Kaspersky | 2021, November | Compromised SES token from third party | N/A | Phishing attacks | [Kaspersky's stolen Amazon SES token used in Office 365 phishing](https://www.bleepingcomputer.com/news/security/kasperskys-stolen-amazon-ses-token-used-in-office-365-phishing/) |
| Onus | 2021, December | Log4Shell vulnerability in Cyclos server | AmazonS3FullAccess creds (and DB creds) in Cyclos config | 2 million ONUS users’ information including EKYC data, personal information, and password hash was leaked.  | [The attack on ONUS – A real-life case of the Log4Shell vulnerability](https://cystack.net/research/the-attack-on-onus-a-real-life-case-of-the-log4shell-vulnerability) |
| Flexbooker | 2021, December | Unknown | Unknown | 3.7M first and last names, email addresses, phone numbers, "encrypted" passwords | [Booking management platform FlexBooker leaks 3.7 million user records](https://therecord.media/booking-management-platform-flexbooker-leaks-3-7-million-user-records/) |
| Uber | 2022, September | Contractor account compromise leading to AWS credential discovery on a shared drive | Unknown | N/A | [Uber - Security update](https://www.uber.com/newsroom/security-update/) |

## Catalog of Vendor Reports on AWS Customer Security Incidents

| Report | Date | Root Cause | Escalation Vector(s) | Impact | Link to details|
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| TeamTNT Worm| 2020, April | Misconfigured Docker & k8s platforms | Steals AWS credentials from \~/.aws/* | Cryptojacking for Monero | [Team TNT – The First Crypto-Mining Worm to Steal AWS Credentials](https://web.archive.org/web/20210607223609/https://www.cadosecurity.com/post/team-tnt-the-first-crypto-mining-worm-to-steal-aws-credentials/), [TeamTNT with new campaign aka “Chimaera”](https://cybersecurity.att.com/blogs/labs-research/teamtnt-with-new-campaign-aka-chimaera) |
| Expel case study 1 | 2020, April  | 8 IAM access keys compromised | Backdoored security groups | Command line access to EC2 instances | [Finding evil in AWS: A key pair to remember](https://web.archive.org/web/20210226132628/https://expel.io/blog/finding-evil-in-aws/) |
| Expel case study 2 | 2020, July  | Root IAM user access keycompromised | SSH keys generated for EC2 instances  | Cryptojacking | [Behind the scenes in the Expel SOC: Alert-to-fix in AWS](https://web.archive.org/web/20210128055101/https://expel.io/blog/behind-the-scenes-expel-soc-alert-aws/) |
| Mandiant: Insider Threat Scenario | 2020, September | Fired employee uses credentials | Access CI/CD server, create a new user, steal credentials | Deleted production databases | [Cloud Breaches: Case Studies, Best Practices, and Pitfalls](https://web.archive.org/web/20201103091354/https://www.youtube.com/watch?v=rtEjI_5TPdw&feature=youtu.be/) |
| Expel case study 3 | 2022, April | Credentials in publicly available code repository | AttachUserPolicy used for privesc | Cryptomining (prevented) | [Incident report: From CLI to console, chasing an attacker in AWS](https://expel.com/blog/incident-report-from-cli-to-console-chasing-an-attacker-in-aws/) |
| Permiso case study 1 | 2022, June | Gitlab vulnerability (CVE-2021-22205) | Credentials on the system found, used to create a backupuser | Cryptomining | [Anatomy of an Attack: Exposed keys to Crypto Mining](https://web.archive.org/web/20220629061640/https://permiso.io/blog/s/anatomy-of-attack-exposed-keys-to-crypto-mining/) |

## Catalog of AWS Exploits via SSRF

[Server-side request forgery](https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/) is a class of attack that is not cloud or AWS specific. However, the existence of cloud metadata services, such as [IMDS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html) in AWS, have historically allowed for a substantial straightforward impact when SSRF is achieved on a cloud hosted application. For that reason, we include this list of SSRF attacks against AWS environments.

* [Bypassing SSRF Protection to Exfiltrate AWS Metadata from LarkSuite](https://sirleeroyjenkins.medium.com/bypassing-ssrf-protection-to-exfiltrate-aws-metadata-from-larksuite-bf99a3599462)
* [ESEA Server-Side Request Forgery and Querying AWS Meta Data](https://buer.haus/2016/04/18/esea-server-side-request-forgery-and-querying-aws-meta-data/)
* [A pair of Plotly bugs: Stored XSS and AWS Metadata SSRF](https://web.archive.org/web/20170527104436/https://ysx.me.uk/a-pair-of-plotly-bugs-stored-xss-and-aws-metadata-ssrf/)
* [Dropbox - Full Response SSRF via Google Drive](https://github.com/httpvoid/writeups/blob/main/Hacking-Google-Drive-Integrations.md#dropboxs-full-read-ssrf)
* [Mandiant - Old Services, New Tricks: Cloud Metadata Abuse by UNC2903](https://www.mandiant.com/resources/blog/cloud-metadata-abuse-unc2903)
* [SSRF leads to access AWS metadata.](https://infosecwriteups.com/ssrf-leads-to-access-aws-metadata-21952c220aeb)
* [Escalating SSRF to RCE](https://sanderwind.medium.com/escalating-ssrf-to-rce-7c0147371c40)
* [SSRF Leads To AWS Metadata Exposure](https://systemweakness.com/ssrf-leads-to-aws-metadata-exposure-8b4c3424755b)
* [How I discovered an SSRF leading to AWS Metadata Leakage](https://techkranti.com/ssrf-aws-metadata-leakage/)
* [Exploitation of an SSRF vulnerability against EC2 IMDSv2](https://www.yassineaboukir.com/blog/exploitation-of-an-SSRF-vulnerability-against-EC2-IMDSv2/)
* [Mozilla - AWS SSRF to Pull AWS Metadata and Keys](https://bugzilla.mozilla.org/show_bug.cgi?id=1550366)

For more about this attack, please see [Hacking the Cloud - Steal EC2 Metadata Credentials via SSRF](https://hackingthe.cloud/aws/exploitation/ec2-metadata-ssrf/)

## Catalog of AWS Threat Actors

| Name | Vectors | Reports |
| ------------- | ------------- | ------------- |
| UNC2903 | SSRF (targeting known CVEs) | [Mandiant - Old Services, New Tricks: Cloud Metadata Abuse by UNC2903](https://www.mandiant.com/resources/blog/cloud-metadata-abuse-unc2903) |
| 8220 Gang | Exploit outdated and misconfigured software | [JupiterOne - 8220 Gang Cloud Botnet Targets Misconfigured Cloud Workloads](https://www.sentinelone.com/blog/8220-gang-cloud-botnet-targets-misconfigured-cloud-workloads/) |

<a class="anchor" id="1"></a> [Postmortem Culture: Learning from Failure](https://sre.google/sre-book/postmortem-culture/)

<a class="anchor" id="2"></a> _Note_: There have been numerous identified incidents of Magecart exploiting S3 Global Write - in [one review targeting "well over 17,000 domains"](https://web.archive.org/web/20210620145033/https://www.riskiq.com/blog/labs/magecart-amazon-s3-buckets/)
