# Overview 
This section involves the implementation of a Splunk Universal Forwarder on the Windows 10 machine.

# Implementing the forwarder
* In the Windows machine, I pinged the splunk server to ensure that logs could be ingested into the splunk index.
<img width="687" height="307" alt="image" src="https://github.com/user-attachments/assets/01ed5100-ed5e-4826-a228-bb0f99cbc214" />

* To install the Splunk universal forwarder, you will need to navigate to Splunk's webpage on a web browser in the vm.
* link: https://www.splunk.com/
* Create an account if you do not have one.
* Once logged in, click Trials and Downloads
<img width="1862" height="291" alt="image" src="https://github.com/user-attachments/assets/028f33bf-7359-4216-af75-6296a0767013" />

* Click on Universal Forwarder download
<img width="1330" height="531" alt="image" src="https://github.com/user-attachments/assets/1ad6bcda-4e5c-4805-ab4f-bad9cfc92813" />

* Download the version for Windows 10
<img width="1367" height="207" alt="image" src="https://github.com/user-attachments/assets/ec4fab91-92a5-49fa-89c5-594bad9012c3" />

* Once downloaded, begin the installation
* Select the on premises option
<img width="491" height="387" alt="image" src="https://github.com/user-attachments/assets/b3690b26-05cd-4191-ab9b-a39b25fb9a43" />

* Since we are using this machine as a forwarder, we will need to add the Splunk server as the receiving indexer
<img width="495" height="387" alt="image" src="https://github.com/user-attachments/assets/af9b2731-2595-4ad0-a453-31e50500276c" />

* Next, we will add the Windows machine to our Splunk instance by adding the default port as a receiving port
* Add the receiving port to the settings
<img width="1918" height="487" alt="image" src="https://github.com/user-attachments/assets/68ce1665-3f20-446d-ab62-6b85f4c20a42" />

* Next we will need to add configurations to allow Windows security event logs to be forwarded to Splunk


* This can be achieved by adding the **inputs.conf** file from
 ```Bash
  C:\Program Files\SplunkUniversalForwarder\etc\system\default
```
* to
 ```Bash
C:\Program Files\SplunkUniversalForwarder\etc\system\local
```

* Next, we can modify the inputs.conf file using Splunk's settings for the configuration file
* Link: https://help.splunk.com/en/data-management/splunk-enterprise-admin-manual/9.1/configuration-file-reference/9.1.9-configuration-file-reference/inputs.conf
* These settings will forward only the Windows Security Event logs to the index
<img width="692" height="683" alt="image" src="https://github.com/user-attachments/assets/3de02733-f986-441c-bcc0-0605d3cb750b" />

* Next, I changed the settings of the Service in order to login as the local account for the Windows machine
<img width="398" height="460" alt="image" src="https://github.com/user-attachments/assets/7317c675-fd35-4da4-841b-9e37fd875d2d" />

* I verified the logs being forwarded in Splunk
<img width="1917" height="897" alt="image" src="https://github.com/user-attachments/assets/3a60239c-d199-4267-bd2a-08e07579a19a" />

* We can see that the Windows Security logs were successfully forwarded to the Splunk indexer.
* I also added the Application logs to the instance as well

<img width="1578" height="732" alt="image" src="https://github.com/user-attachments/assets/0ea062c6-d14e-4f15-b05b-49de0c092069" />




