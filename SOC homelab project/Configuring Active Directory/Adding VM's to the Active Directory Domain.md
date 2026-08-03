# Overview 
- This section entails the addition of the VM's to the domain to centralize the management of the machines

# Adding the Windows endpoint to the domain
- To add the Windows endpoint to the domain, I first changed the name of the machine in order to maintain an organized domain.
- I re-named it to **WIN-PC01**.
<img width="1191" height="495" alt="image" src="https://github.com/user-attachments/assets/fcea271a-213c-4034-8b74-c89b514e1785" />

- Next, I began to add the endpoint to the domain.
<img width="1828" height="961" alt="image" src="https://github.com/user-attachments/assets/e6dfd132-a9a7-45a3-921e-904e69d0b245" />

<img width="1918" height="960" alt="image" src="https://github.com/user-attachments/assets/c96856a8-edc9-4196-b871-adcd46c1e6ff" />

- Using the account **vlindsay**, which was assigned as the domain administrator, I was able to add the Windows endpoint to the domain of **phoenix.local**.

<img width="1861" height="666" alt="image" src="https://github.com/user-attachments/assets/5c6ec62a-7476-475a-9ffc-4774258affad" />

- After sometime, the machien was configured within the domain, and I logged into the Windows endpoint.
<img width="1913" height="956" alt="image" src="https://github.com/user-attachments/assets/a897551e-0129-4586-a2bb-e074cfa8faf7" />

- We can see that the addition was successful, since it was detected on the DC.
<img width="752" height="312" alt="image" src="https://github.com/user-attachments/assets/abd2c420-81af-45eb-8427-2a304e0ae09f" />

# Adding the Splunk server to the domain
- To add the servers to the domain, I will have to do some configurations.
- I ran the following commands:

```
sudo apt update
sudo apt install realmd sssd sssd-tools adcli samba-common-bin oddjob oddjob-mkhomedir packagekit
```
- These commands update packages, and allow the servers to discover and joing the domain, use kerberos, and be logged into by AD users.
- Prior to joining the domain, I needed to point DNS to the DC.
```Bash
sudo systemctl disable systemd-resolved.service
sudo systemctl stop systemd-resolved.service
sudo systemctl status systemd-resolved.service
```

<img width="926" height="67" alt="image" src="https://github.com/user-attachments/assets/9878fb24-ed58-4c43-a6f7-87a326ca27f3" />

- I changed the DNS to point towards the domain controller.
<img width="951" height="612" alt="image" src="https://github.com/user-attachments/assets/c8ef55d4-efeb-42c4-95b5-acea819eb956" />

- The changes allowed the server to discover the domain.
<img width="886" height="316" alt="image" src="https://github.com/user-attachments/assets/ba5d9b91-dcfa-4cfc-9676-6c7786aac9dc" />

- Once the domain was discovered, I logged in as the default Administrator account.
<img width="955" height="412" alt="image" src="https://github.com/user-attachments/assets/e9816787-4c46-41e9-9981-998da9f58560" />

- Once configured, I logged in as the **vlindsay** account.
<img width="1323" height="147" alt="image" src="https://github.com/user-attachments/assets/b081e4db-458b-4e9c-b7be-901eda274d40" />

- On the DC, I can see the Splunk server.
<img width="752" height="535" alt="image" src="https://github.com/user-attachments/assets/9a5a25a8-5338-4f3a-bcec-3548cef25329" />

- I will create the organization units later.

# Adding the suricata server to the domain
- Adding the suricata server to the domain follows the same process as the Splunk server.
<img width="956" height="691" alt="image" src="https://github.com/user-attachments/assets/218fdfab-d231-4f08-85c7-97753a385ea7" />

- I updated the packages, and made changes to the **resolv.conf** file.

<img width="765" height="317" alt="image" src="https://github.com/user-attachments/assets/07fec218-860e-45a3-933c-55f4882ddd37" />

- The domain was discovered.

<img width="858" height="77" alt="image" src="https://github.com/user-attachments/assets/f3a1b810-81c8-4ca3-9d0f-5e83d6644472" />

- I joined the domain using the configured **vlindsay** domain administrator account.
<img width="938" height="177" alt="image" src="https://github.com/user-attachments/assets/eb82b555-00c3-4200-9a23-7aa509d139cc" />

- Now we can see the suricata server on the domain controller.
<img width="748" height="307" alt="image" src="https://github.com/user-attachments/assets/4ea2d2d7-3855-4a7b-bd0b-fd2c21459401" />






