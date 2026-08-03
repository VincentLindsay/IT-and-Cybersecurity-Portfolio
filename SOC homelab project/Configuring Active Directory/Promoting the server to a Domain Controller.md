# Summary
- This section involves the promotion of the Windows Server 2019 into a Domain Controller (DC).

# Promoting the server to a Domain Controller
- Prior to the installation of Active Directory Domain Services (AD-DS), I assigned the server a static IP and DNS IP adresses.
- To do this, I navigated to the network adapter's settings on the machine.

<img width="810" height="615" alt="image" src="https://github.com/user-attachments/assets/44a5ec4d-9107-48a5-b006-a87314ac9b4b" />

- I also changed the NIC of the vm to have the custom made VNET I made previously

<img width="893" height="916" alt="image" src="https://github.com/user-attachments/assets/1032d0f0-b7c9-4778-bfed-726f299bd55e" />

- Using the **ping** command, I can now verify that the server's connectivity is isolated.

<img width="983" height="512" alt="image" src="https://github.com/user-attachments/assets/49597081-6d57-4b5c-8d46-8d02839a95f8" />



- To be able to promote the server, AD-DS has to be installed.
- This was done by the addition of roles and features.

<img width="791" height="557" alt="image" src="https://github.com/user-attachments/assets/b9995c89-bee5-4215-9c07-1fe25f631bae" />

<img width="790" height="562" alt="image" src="https://github.com/user-attachments/assets/0aed8e05-0f50-48d2-b069-acc74ce2cf39" />

- We can now see that the installation of AD-DS was successful.

<img width="787" height="563" alt="image" src="https://github.com/user-attachments/assets/841e94ae-2f2d-4a37-9e83-73726f849c3d" />

- Next, I added a new forest to serve as the domain in the lab.
<img width="766" height="562" alt="image" src="https://github.com/user-attachments/assets/64325759-64ab-463e-979a-43ebf2284692" />

- After sometime, the server was promoted to a DC
- I created a separate domain account to serve as a domain administrator to simplify the addition of endpoints into the domain.

<img width="1023" height="780" alt="image" src="https://github.com/user-attachments/assets/32e5d191-2c89-474d-ba99-2f5ec6fdedb2" />

- I will add Organizational Units in a later point






