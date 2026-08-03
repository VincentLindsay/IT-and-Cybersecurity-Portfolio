# Overview
- This section will revolve around the creation of Organizational Units to simulate a real company. 
  - The format will be as follows:
    - helpdesk.local (forest)
      - Corporate
        - Users
        - Computers
        - Servers
        - Departments
          - Human Resources
          - Finance
          - Information Technology
          - Sales
          - Marketing
        - Groups
        - Service Accounts
        - Disabled Users 

# Creating the Organizational Units
* To begin I checked all of the built-in Organizational units.
<img width="1022" height="770" alt="image" src="https://github.com/user-attachments/assets/73f0c367-47ac-4fce-bbd0-e33310f282c3" />

- I created the OU called **Corporate**
<img width="435" height="383" alt="image" src="https://github.com/user-attachments/assets/37200bf4-166e-478e-9683-63d895220339" />

- For the remaining OU's, I will use PowerShell to speed up the process. 
<img width="962" height="396" alt="image" src="https://github.com/user-attachments/assets/8aac9f96-58de-4958-ab80-bd95763f3a39" />

- I imported the ActiveDirectory module to the DC's shell.
- I also created a Powershell Script that creates the primary OU's.
<img width="765" height="382" alt="image" src="https://github.com/user-attachments/assets/11e665db-409d-4ddb-944e-6f76049a7632" />

```PowerShell
$PrimaryOUs = @(
    "Users",
    "Computers",
    "Servers",
    "Departments",
    "Groups",
    "Service Accounts",
    "Disabled Users"
)

foreach ($OU in $PrimaryOUs) {
    New-ADOrganizationalUnit `
        -Name $OU `
        -Path "OU=Corporate,DC=helpdesk,DC=local" `
        -ProtectedFromAccidentalDeletion $true
}
```

* After creating the script, I executed the script.
<img width="773" height="703" alt="image" src="https://github.com/user-attachments/assets/80fe738b-ee4c-4652-9c6d-c522de811977" />

* We can now see the created OUs within the **Corporate** OU via Active Directory Users and Computers.
<img width="753" height="530" alt="image" src="https://github.com/user-attachments/assets/0a1043f1-560a-40f8-89e0-dca3abbc694f" />

* The next step is to create further OUs within the **Departments** Organizational Unit.
  * I will follow the same process, except the variable names will be tailored to the **Departments** OU.
 
<img width="767" height="382" alt="image" src="https://github.com/user-attachments/assets/576b8e97-db1f-465f-9a36-b24023c7a811" />

```Powershell
$Departments = @(
    "Human Resources",
    "Finance",
    "Information Technology",
    "Sales",
    "Marketing"
)

foreach ($Department in $Departments) {
    New-ADOrganizationalUnit `
        -Name $Department `
        -Path "OU=Departments,OU=Corporate,DC=helpdesk,DC=local" `
        -ProtectedFromAccidentalDeletion $true
}
```
  
* We can now see the created Organizational Units located with the **Departments** OU.


















