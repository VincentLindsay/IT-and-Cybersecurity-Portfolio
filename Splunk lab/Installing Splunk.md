# Overview
This section involves the installation and configuration of the splunk instance on the Ubuntu server

# Installing Splunk
* To install Splunk, you will need to navigate to Splunk's webpage
* link: https://www.splunk.com/
* Create an account if you do not have one.
* Once logged in, click Trials and Downloads
<img width="1862" height="291" alt="image" src="https://github.com/user-attachments/assets/d99914a5-927f-4eef-b448-905ed59f39f9" />

* Click on Splunk Enterprise trial
<img width="1397" height="657" alt="image" src="https://github.com/user-attachments/assets/18290099-29fd-471f-a252-eb154e0bb6c1" />

* Select the installation package for Linux, and specifically the **.deb** package since we are using Ubuntu, which is a distribution of Debian Linux
<img width="1647" height="832" alt="image" src="https://github.com/user-attachments/assets/a6ead251-6001-4285-b51a-e3fc72c69463" />

* Since we are SSH'd into the server, we can simply copy the wget link
* After retrieving the package, we can see that it is present in the server
<img width="1462" height="372" alt="image" src="https://github.com/user-attachments/assets/1cf64bc2-0bcd-43d5-9801-371ee5850e36" />

* Next, I began to install the package to the server
<img width="1217" height="227" alt="image" src="https://github.com/user-attachments/assets/c885214b-d880-4e6d-8795-e044255f58fb" />

* Next, I navigated to the **/opt/splunk/bin** directory to further configure the instance
* In the directory, I logged into the splunk account, and began to run the installer
<img width="893" height="107" alt="image" src="https://github.com/user-attachments/assets/fda6428d-1c7d-4b64-8255-b84cff45bc20" />

* Agree to the license, and create an administrator account that will be used to login to the console
* Once you agree, the installation of Splunk will begin
* Additionally, I also configured the instance to always launch upon start-up of the machine
<img width="1913" height="122" alt="image" src="https://github.com/user-attachments/assets/994e8842-c588-469c-b08d-70a198edeeb6" />

* I also created a snapshot of when splunk was installed
* I was able to login to the splunk console from my host machine using the server's IP address on the port 8000
<img width="1918" height="1140" alt="image" src="https://github.com/user-attachments/assets/a796dcd7-8cea-4931-b55a-562eba809038" />






