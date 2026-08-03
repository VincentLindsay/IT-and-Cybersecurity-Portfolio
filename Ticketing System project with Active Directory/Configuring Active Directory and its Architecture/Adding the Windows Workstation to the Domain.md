# Overview
- In this section, I will join the Windows 11 workstation (CLIENT01) to the helpdesk.local domain.
Once joined, the workstation will authenticate against the Domain Controller instead of relying solely on local accounts.


# Adding the workstation to the domain
- Prior to joining the workstation to the domain, I verified the network connectivity of the machine.
<img width="806" height="666" alt="image" src="https://github.com/user-attachments/assets/790ec7a9-6088-46c0-900e-df052919ed5e" />

- We can see that the machine resolves the domain, and I can proceed with joining the machine to the domain.
<img width="802" height="632" alt="image" src="https://github.com/user-attachments/assets/ad0d7ccf-df93-4d1a-aaa1-18914840881b" />

- After logging in as the Administrator account, the workstation joined the domain.
<img width="801" height="636" alt="image" src="https://github.com/user-attachments/assets/9bcaa22a-75e7-4c88-8499-6d7a7a1ee724" />

- Next, I verified that the Workstation appears in Active Directory Users and Computers.
<img width="751" height="536" alt="image" src="https://github.com/user-attachments/assets/252ccf5b-ebcc-4a6b-890f-5a72a76e5e8c" />

- Using PowerShell, I moved the Windows Client to the **Corporate/Computers** OU.
<img width="757" height="530" alt="image" src="https://github.com/user-attachments/assets/2208377e-f071-46b4-82c8-2987333c01f6" />

```PowerShell
Get-ADComputer CLIENT01 | Move-ADObject ` -TargetPath "OU=Computers,OU=Corporate,DC=helpdesk,DC=local"
```

- I verified that the Workstation joined the domain.
<img width="1022" height="525" alt="image" src="https://github.com/user-attachments/assets/2ad89b2e-b4ef-41ca-8e54-9b2e4df86b74" />




























