# Overview
- In this section I will configure security groups, implement basic password policies, and prepare the domain for future Help Desk operations.
  - For this section I will powershell.
 
# Configuring Active Directory Security Groups
- I will create the following **Deparment**security groups:
  - HR_Users
  - Finance_Users
  - IT_Users
  - Sales_Users
  - Marketing_Users
- These groups will be the resource groups:  
  - VPN_Users
  - Printer_Users
  - SharedDrive_RW
  - SharedDrive_RO

<img width="763" height="386" alt="image" src="https://github.com/user-attachments/assets/a38446b7-cde9-46e4-81a0-834c8a2162e4" />

- This script will create the Department groups as a global security group.
```PowerShell
$DepartmentGroups = @(
    "HR_Users",
    "Finance_Users",
    "IT_Users",
    "Sales_Users",
    "Marketing_Users"
)

foreach ($Group in $DepartmentGroups) {
    New-ADGroup `
        -Name $Group `
        -SamAccountName $Group `
        -GroupCategory Security `
        -GroupScope Global `
        -Path "OU=Groups,OU=Corporate,DC=helpdesk,DC=local"
}
```
<img width="957" height="392" alt="image" src="https://github.com/user-attachments/assets/207a510d-a9d4-4fc9-a5d9-a36c10b13687" />

- Now I can see the successful addition of the security groups.
  - The next step is to create the resource groups.
<img width="958" height="775" alt="image" src="https://github.com/user-attachments/assets/b367604a-3269-4f30-9dba-e84c4ac327da" />

- I created the resource groups, and verfied one of the groups.
<img width="960" height="127" alt="image" src="https://github.com/user-attachments/assets/193f00a6-b419-4fc7-909e-fb606e30af5f" />












