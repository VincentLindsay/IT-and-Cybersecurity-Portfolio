# Overview
- In this section I secured the MariaDB installation and create a dedicated database and database user for osTicket.

# Configuring MariaDB
- To begin, I started with the secure configuration of MariaDB to prevent unauthenticated logins.
- I used to following command:
```Bash
sudo mysql_secure_installation
```

- I successfully changed the authentication settings for MariaDB
<img width="1918" height="1101" alt="image" src="https://github.com/user-attachments/assets/1911bd7c-e3ac-4cb4-a61f-d1dabf5e2fb8" />

- I also verified the version of MariaDB
<img width="956" height="458" alt="image" src="https://github.com/user-attachments/assets/3d46c2b9-a317-4f1b-921b-102dfd36d83b" />

- I began to create the database for osTicket
<img width="718" height="157" alt="image" src="https://github.com/user-attachments/assets/a28753ca-da91-4329-b458-0aeb2ee8291c" />

- Next, I checked that the database was actually created.
<img width="772" height="275" alt="image" src="https://github.com/user-attachments/assets/243a2a58-b497-42bb-a93f-220b03d8cbde" />

- I began to create the database account.
<img width="722" height="312" alt="image" src="https://github.com/user-attachments/assets/4bee2e18-6fb5-4f0a-aa11-4a6170878e1f" />

- I will grant the account full access to the database.
<img width="957" height="562" alt="image" src="https://github.com/user-attachments/assets/6f3b9f31-3af2-4816-b8d0-8fd26ba91c73" />

- I checked the databases the account has access to.
<img width="957" height="456" alt="image" src="https://github.com/user-attachments/assets/4ef9b8da-8642-4c45-8d52-8543c02690aa" />


















