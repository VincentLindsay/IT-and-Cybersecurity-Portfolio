# Section summary
- In this section, I installed an Apache Web Server, MariaDB Database Server, and PHP and any extensions needed to run osTicket.
- I followed the osTicket installation Documentation: https://docs.osticket.com/en/latest/Getting%20Started/Installation.html

# Installing Apache
- To install Apache, I executed the following command:
```Bash
sudo apt install apache2 -y
```
- After installing Apache, I verified that the service is running.
<img width="960" height="417" alt="image" src="https://github.com/user-attachments/assets/c06af991-40bf-4331-88d2-066fdee46d12" />

- I verified via my web browser.
<img width="1917" height="1087" alt="image" src="https://github.com/user-attachments/assets/78844467-e91b-4d2e-97b7-6679a19f6ee6" />

- We can now see that the web page is working, and that is running on Port 80 - HTTP.
<img width="1886" height="56" alt="image" src="https://github.com/user-attachments/assets/c63b0734-f364-4daf-8821-fbfba8c5fd74" />

# Installing MariaDB
- To store ticket history, I will use MariaDB for this project, and I installed it via this command:
```Bash
sudo apt install mariadb-server mariadb-client -y
```

<img width="1918" height="587" alt="image" src="https://github.com/user-attachments/assets/e904d096-6979-49d8-a24f-a072698d9ddb" />

- I verified that the service is active.
- I also verified that the Database is working
<img width="1120" height="260" alt="image" src="https://github.com/user-attachments/assets/6a591523-6c54-4e09-b40c-06396ff7c1ba" />

# Installing PHP
- Installed PHP through this command:
```Bash
sudo apt install php libapache2-mod-php php-mysql -y
```

- Once installed, I checked the version of PHP.
<img width="1077" height="117" alt="image" src="https://github.com/user-attachments/assets/d2c7ae14-28f7-4459-8d54-4d22bc170f40" />

- I installed various PHP modules for osTicket to run:
```Bash
sudo apt install -y \
php-cli \
php-common \
php-imap \
php-intl \
php-gd \
php-curl \
php-xml \
php-mbstring \
php-zip \
php-bcmath \
php-soap \
php-apcu \
php-ldap 
```

- I also verified that the PHP modules were installed.
<img width="1918" height="1096" alt="image" src="https://github.com/user-attachments/assets/92248f5f-9926-4903-93ac-9955ede7b9b3" />



- I also created a test page, and verified that its working
<img width="1917" height="1091" alt="image" src="https://github.com/user-attachments/assets/af74d7ed-3734-4da7-81aa-1e25b057638c" />

- After creating the information page, I deleted it.
<img width="1107" height="107" alt="image" src="https://github.com/user-attachments/assets/241f53fb-7003-4229-be6d-005c149f33d7" />

















