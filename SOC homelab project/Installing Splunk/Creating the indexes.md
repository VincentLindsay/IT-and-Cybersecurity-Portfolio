# Overview
- This section will showcase the creation of different indexes which pertain to log sources like the Windows Endpoint, or the Domain Controller.

# Creating the indexes and installing apps on Splunk
- To see a more detailed account of how I achieved this portion of the lab, check of my Splunk [lab.](https://github.com/VincentLindsay/Security-Analysis-Portfolio/tree/main/Splunk%20lab)
- Prior to creating any indexes, I installed applications on Splunk that will make querying logs much easier.

<img width="1193" height="726" alt="image" src="https://github.com/user-attachments/assets/60031c1a-3578-44ce-ab58-789475b2f7f4" />

<img width="1247" height="597" alt="image" src="https://github.com/user-attachments/assets/68eeedf1-0a73-4ef9-a726-c0212e0bcccf" />

- I added the Splunk Addon for Sysmon, and for Windows.

<img width="1205" height="622" alt="image" src="https://github.com/user-attachments/assets/ca80aad0-21c2-43ee-9d2a-44ec74aadbc7" />

- Since I have an Active Directory Domain, I also installed an add-on for Active Directory.
- Now that I've installed the applications, I can now move onto creating the indexes.
- The first index I created is called **winevent**.
<img width="1871" height="46" alt="image" src="https://github.com/user-attachments/assets/52e6691d-a0ff-4dcb-9787-87d6ecd35f14" />

- This index focuses on the Windows endpoint logs, such as application and sysmon.
- The index will also be used to monitor Active Directory events.
- I also created two indexes for Zeek, and Suricata.

<img width="1890" height="145" alt="image" src="https://github.com/user-attachments/assets/20bbadab-c399-4a01-9bf8-90c47d37eea6" />

- Now with the creation of the indexes, I can now begin to install Splunk Universal Forwarder on every endpoint.





