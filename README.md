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

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/location.PNG)

<b>Virus Total Result:</b>

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/virustotal_result.PNG)


```
Flag : FIN2022{C:\Program Files (x86)\Windows Resource Kits\Tools\Data Backup App\Backup.exe}
```



<h2>Injection 5: 150</h2>
Refer to the injection 3 & 4, which account privilege was gained by the attacker after exploiting the misconfigured program?

The format for this flag is <b>FIN2022{AccountDomain\AccountName}</b>

<h3>Solution :</h3>

Check the event log with filtering....... 

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/special_priv.PNG)


```
Flag : FIN2022{NT Authority\System}
```



<h2>Injection 6: 50</h2>
Find out the IP address attacker which was used to controlling support-pc?

The format for this flag is <b>FIN2022{IP ADDRESS}</b>

<h3>Solution :</h3>

Check the event log with filtering....... 

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/attacker_ip.PNG)


```
Flag : FIN2022{192.168.187.135}
```



<h2>Injection 7: 100</h2>
What was the ip of the support-pc when it was compromised?

The format for this flag is <b>FIN2022{IP Address}</b>

<h3>Solution :</h3>

Check the event log with filtering....... 

Take a look at the log, and check your current ip address. it is same as the below image address. So the IP address with be the last one before the IP change.
![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/after_change_ip.PNG)

Now check the IP address of this PC. Compare the time between this two log and you will get the actual result.

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/before_change.PNG)



```
Flag : FIN2022{192.168.187.149}
```


<h2>Injection 8: 100</h2>
An application was executed by the attacker to collect domain object information from DC. What is the application name?

The format for this flag is <b>FIN2022{filename with extension}</b>

<h3>Solution :</h3>

There are few tools and techniques to collect the information from Domain Controller. BloodHound is an Active Directory (AD) reconnaissance tool that can reveal hidden relationships and identify attack paths within an AD environment. 

SharpHound is the official data collector for BloodHound. It is written in C# and uses native Windows API functions and LDAP namespace functions to collect data from domain controllers and domain-joined Windows systems by executing ><b>sharphound.exe</b> or <b>sharphound.ps1</b> script. Both of them provide json data of the DC, after importing the json data in the bloodhound attacker get the DC information.

Now take a look at the event log, and search if there anything in the name of sharphound.

Here we found that there is a log with sharphound.exe

![image](https://github.com/ruefulrobin/findrill2022/blob/main/img/sharphound.PNG)

```
Flag : FIN2022{sharphound.exe}
```


<h2>Injection 9: 150</h2>
During the post exploitation phase, which attack method was used by the attacker to get user details from DC?

The format for this flag is <b>FIN2022{FLAG}</b>

<h3>Solution :</h3>


<b>What is DCSync Attacks?</b>

DCSync is an attack that allows an adversary to simulate the behavior of a domain controller (DC) and retrieve password data via domain replication.

These attacks leverage what is a necessary function in Active Directory, which complicates attempts to prevent them. Large-scale networks require many DCs to function, and each of those DCs need to have up-to-date information. That requires a function allowing one DC to update another DC on any changes, like updated credential information.

Attackers subvert that necessary function by pretending to be a DC and using the DSGetNCChanges function to request password hashes. A common attack uses this method to get the KRBTGT hash, which brings them one step closer to getting a Kerberos "golden ticket."

DCSync requires a compromised user account with domain replication privileges. Once that is established, one can find a domain controller, tell it to replicate, and get password hashes from its subsequent response.

As I told that, The <b>Bloohound</b> tool gather information of a DC after compromised an user account with the special privileges how dcsync do.



```
Flag : FIN2022{dcsync}
```
