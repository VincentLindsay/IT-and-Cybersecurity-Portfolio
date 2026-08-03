# Overview
- This section will feature the creation of alerts that pertain to the simulated attack.


# Creating the alerts
- The first alert I created checks for Kerberos Username Enumeration.

```Bash
index=winevent EventCode IN (4768,4771)
| stats count dc(TargetUserName) as users by _time, Client_Address, Account_Name
```
<img width="952" height="897" alt="image" src="https://github.com/user-attachments/assets/9b2261b9-6567-4eaf-83c4-6877f3fb1b7c" />

- The second alert I made detects for Kerberos AS tickets without preauthentication.

```Bash
index=winevent EventCode=4768 Account_Name !=DC01$
| stats count by _time, Account_Name
```
<img width="947" height="731" alt="image" src="https://github.com/user-attachments/assets/a0b8f36b-5553-43a1-b016-bb2d25ad741d" />

- This alert detects an abnormal number of Kerberos service ticket requests
```Bash
index=winevent EventCode=4769
| stats count BY _time Client_Address Account_Name
```
<img width="1002" height="912" alt="image" src="https://github.com/user-attachments/assets/e3c707ca-8b98-4854-bf1a-4159d3f840a7" />


- This alert identifies any failed login, and maps it out based on the IP address.
```Bash
index=winevent EventCode=4625 
| stats  count BY _time Source_Network_Address Account_Name
```
<img width="957" height="902" alt="image" src="https://github.com/user-attachments/assets/5a85df5c-4d36-4439-99d9-97ed9c9dc45c" />

- This alert Identifies any successful logins from an untrusted network.
```Bash
index=winevent EventCode=4624 Account_Name!=DC01$ 
| where NOT cidrmatch("172.16.50.0/24",Source_Network_Address)   
| search Account_Name!=SYSTEM 
| table  _time host Account_Name Source_Network_Address Logon_Type
```

<img width="947" height="812" alt="image" src="https://github.com/user-attachments/assets/c667fe81-0aec-4590-9eff-4a3587cb4f33" />

- This next alert pertains to special priviledges assigned to a logon, but excludes machine accounts, and system accounts.
```Bash
index=winevent EventCode=4672 
| stats count by _time, Account_Name
| search NOT Account_Name IN ("SYSTEM","LOCAL SERVICE","NETWORK SERVICE", "DC01$", "DWM-1" "DWM-2" )
```

<img width="952" height="906" alt="image" src="https://github.com/user-attachments/assets/319d70be-f374-4642-ae01-8b095062d3c2" />


- The next alert I created pertains to registry modications. 
```Bash
index=winevent EventCode=4657
```
<img width="956" height="817" alt="image" src="https://github.com/user-attachments/assets/ca431e87-83db-49be-9a4c-70d3e14d9817" />

- This alert identifies an external connection to one of the machines.
```Bash
index=winevent EventCode=5156
| where NOT cidrmatch("172.16.50.0/24",DestAddress)
```
<img width="998" height="820" alt="image" src="https://github.com/user-attachments/assets/e4ecce1d-fb13-4ef5-9a82-e45efc650562" />

- The last alert I created pertains to priveledged account created.

```Bash
index=winevent (EventCode=4720 OR EventCode=4728) 
| search TargetUserName="adm-*" OR MemberName="*adm-*"
```
<img width="1002" height="910" alt="image" src="https://github.com/user-attachments/assets/f278d896-4d22-4345-ac66-d0cce2838948" />


