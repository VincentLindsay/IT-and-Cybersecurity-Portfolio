# Overview
- In this section, I deployed the osTicket application to Apache, configured the required permissions, and prepared the web installer.


# Installing osTicket
- I verified the Apache document root
<img width="710" height="116" alt="image" src="https://github.com/user-attachments/assets/6ea6c5f0-f3b1-44cb-833e-96bb4af15a25" />

- I downloaded the **.zip** file from the official github page.
- Direct link: https://github.com/osTicket/osTicket
- I installed osTicket, and created the respective directories
<img width="952" height="373" alt="image" src="https://github.com/user-attachments/assets/174d04c8-d981-463b-ab87-4c523bbed25f" />

- I will now copy the osTicket files to the Apache web root.
<img width="952" height="206" alt="image" src="https://github.com/user-attachments/assets/13688339-d243-4589-8847-068bbc629d46" />

- I changed the file ownership of the osTicket files to Apache.
<img width="953" height="326" alt="image" src="https://github.com/user-attachments/assets/52ddb881-231b-4b5e-a9aa-f2656ca12a70" />

- I also changed the recommended file and directory permissions for the web page.
<img width="1096" height="166" alt="image" src="https://github.com/user-attachments/assets/a182d9e0-00d5-4611-8822-5e394b9ec213" />

- I also created the osTicket configuration file.
<img width="1136" height="162" alt="image" src="https://github.com/user-attachments/assets/7929af2a-ae50-4dce-975d-65546c9f8ca2" />

- I also enabled the necessary Apache modules.
<img width="1838" height="1005" alt="image" src="https://github.com/user-attachments/assets/e0f8579c-d82d-4970-b0e1-d63b16c01a98" />

- We can now see that the osTicket web page works
<img width="1918" height="1087" alt="image" src="https://github.com/user-attachments/assets/7743b32e-9045-48f5-840f-20f4da06b73d" />



















