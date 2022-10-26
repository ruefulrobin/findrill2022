# Financial Cyber Drill 2022 - Writeup
This repository is basically for the writeup of Financial Cyber Drill 2022, organized by <a href="https://www.cirt.gov.bd">BGD e-GOV CIRT</a>

<h2>Injection 0: 25</h2>

Our organization name is FIN and we are very conspicuous financial organization in Bangladesh. Our information technology domain name is FIN.LOCAL and Active Directory Domain Services (AD DS) or domain controller run on Windows Server 2019.

Very recently one of our employee received an email with an attachment. But after opening the attachment he found there was no content in the file. Later IT security team observed some suspicious activity in our organization network.

During analysis/investigation IT security team found a threatening text file in one of our domain controller administrator's account Desktop.

Threatening text file location in DC : 
<b>C:\Users\itadmin1\Desktop\Compromized.txt</b>

For further analysis/investigation we are providing the Active Directory (Domain Controller) server and one workstation (Windows 10) which is used as common workstation for IT support team.

For This injection, you read the scenario and submit <b>FIN2022{UNDERSTOOD}</b> that you understand the scenario.

<h3>Solution :</h3>


```
Flag : FIN2022{UNDERSTOOD}
```


<h2>Injection 1: 50</h2>
Identify the CVE of the vulnerability which was initially exploited by the attacker.
The format for this flag is <b>FIN2022{CVE-XXXX-XXXXX}</b>

<h3>Solution :</h3>
By reading the scenario we understand that this is the Follina Vulnerability. Follina is a Microsoft Office zero-day vulnerability that has recently been discovered. It's a high-severity vulnerability that hackers can leverage for remote code execution (RCE) attacks. If you search the CVE of Follina Vulnerability you will get the result.


```
Flag : FIN2022{CVE-2022-30190}
```


<h2>Injection 2: 50</h2>
Refer to injection 01, which program was abused by the vulnerability?

The format for this flag is <b>FIN2022{filename with extension}</b>

<h3>Solution :</h3>

Follina abuse the Microsoft Windows Support Diagnostic Tool (MSDT.exe) in order to exploit and execute remote code. So the answer is : 


```
Flag : FIN2022{msdt.exe}
```


<h2>Injection 3: 100</h2>
After initial access to the victim machine, attacker performed enumeration to the system and found a service where user privilege was not properly configured. This makes the service vulnerable to exploit. What is the name of that service?

The format for this flag is <b>FIN2022{flag}</b>

<h3>Solution :</h3>

Run sysinternal tool <b>autorun.exe</b> and check the services

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/databackupsvc.PNG)


```
Flag: FIN2022{DataBackupSvc}
```



<h2>Injection 4: 200</h2>
Which file is used by the attacker to gain persistent access to support-pc. Mention the file name with file extension and the full (absolute) directory path.

The format for this flag is <b>FIN2022{E:\Fin\Drill\2022\ctf.txt}</b>

<h3>Solution :</h3>

Run sysinternal tool <b>autorun.exe</b> and check the services. See the path location of the services databackupsvc and go to the file path. If you go one step back you will see the file backup.exe which is the actual file. To confirm that the file is malicious, collect the hash value of the file and check this to the virus total.

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/location.png)

<b>Virus Total Result:</b>

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/virustotal_result.PNG)


```
Flag : FIN2022{C:\Program Files (x86)\Windows Resource Kits\Tools\Data Backup App\Backup.exe}
```
