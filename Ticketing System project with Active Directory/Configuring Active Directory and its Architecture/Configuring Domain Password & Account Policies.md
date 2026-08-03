# Overview
- In this section, I will configure domain-wide password and account lockout policies using Group Policy Management


# Configuring the Policies
- The following settings will be configured to the user account policies:
  - Enforce Password History:	**10 passwords**
  - Maximum Password Age:	**90 days**
  - Minimum Password Age:	**1 day**
  - Minimum Password Length:	**10 characters**
  - Password Complexity: **Enabled**
  - Reversible Encryption:	**Disabled**
  - Account Lockout Threshold:	**5 failed attempts**
  - Lockout Duration:	**15 minutes**
  - Reset Lockout Counter:	**15 minutes**
 
- To achieve this I have to change the settings within Group Policy Management for the domain
<img width="1021" height="773" alt="image" src="https://github.com/user-attachments/assets/5fa55ff3-bb0c-4194-a91d-7c6e513f6836" />

- I will begin modifying the Password Policies located within: 
  - Computer Configuration
    - Policies
      - Windows Settings
        - Security Settings
          - Account Policies
            - **Password Policy**

<img width="953" height="777" alt="image" src="https://github.com/user-attachments/assets/11813498-00bd-465f-b0a2-05fec6a6e228" />


- Now I will Configure the Password History policy.
<img width="786" height="543" alt="image" src="https://github.com/user-attachments/assets/a0225b57-96ac-4f31-af85-8160bda2b74c" />

- Then I will enforce the minimum and maximum password ages.
<img width="801" height="541" alt="image" src="https://github.com/user-attachments/assets/6b521691-468e-4e8b-9523-c8a18a379829" /> 
<img width="797" height="540" alt="image" src="https://github.com/user-attachments/assets/37ca286c-4e89-484d-b0b3-4b3245ddb3d7" />

- I also made the Minimum password length 10 characters.
<img width="800" height="542" alt="image" src="https://github.com/user-attachments/assets/4f339814-ec30-4a46-a156-e9558ce385e3" />

- I also kept the Enforcement of the password length as enabled
<img width="792" height="562" alt="image" src="https://github.com/user-attachments/assets/17dfc18e-d24b-47cb-ba99-235c7528bcf9" />

- I also kept the setting of **Store passwords using reversible encryption** as disabled.

# Configuring the account lockout policies

- I configured the accounts to have a lockout policy of 15 minutes
<img width="413" height="506" alt="image" src="https://github.com/user-attachments/assets/9eb1251e-2acf-4e60-9b97-f46f7ccf67d9" />

- The accounts will lockout after 5 failed logon attempts, and the lockout counter will reset after 15 minutes.
<img width="806" height="551" alt="image" src="https://github.com/user-attachments/assets/3ea71347-8b64-47b2-884e-3f7b49ce3e64" />


- After applying all of the account password policies, I updated group policy and verified the changes were made using PowerShell.
<img width="957" height="198" alt="image" src="https://github.com/user-attachments/assets/a23dd1d0-de56-4cfb-b973-132bfe2d6a5d" />


<img width="960" height="530" alt="image" src="https://github.com/user-attachments/assets/f9ae17f3-e70e-4b1d-9614-3ce652ab7803" />

- We can see the successful application of the new policies made.
<img width="960" height="282" alt="image" src="https://github.com/user-attachments/assets/25d0d3a7-5e6a-4fe3-8512-6719e5d3384c" />























