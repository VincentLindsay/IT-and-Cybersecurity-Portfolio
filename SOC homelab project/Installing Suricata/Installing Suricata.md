# Overview
This section will showcase the installation of suricata.

# Installing Suricata
- To install Suricata, I followed the Quickstart guide.
- Direct link: https://docs.suricata.io/en/latest/quickstart.html
- I first installed the libraries
<img width="928" height="301" alt="image" src="https://github.com/user-attachments/assets/26958e5a-bc58-4eb2-9776-cbfd60aa84ce" />

- Then, I added the Oisf repostory to install Suricata.
<img width="933" height="400" alt="image" src="https://github.com/user-attachments/assets/e5ba7093-7860-433e-bbdc-516eb913e90a" />

- After adding the packages, I installed Suricata on to the server.
- Once installed, I began to modify the configuration settings of the **.yaml** file.
<img width="953" height="368" alt="image" src="https://github.com/user-attachments/assets/f041eb76-940c-4945-b8c3-862661726551" />

- I added the **172.16.50.0/24** network as the HOME_NET that Suricata will monitor and generate alerts for.
- The **!$HOME_NET** setting will have Suricata treat any IP address outside of the range to be an external IP address.

<img width="873" height="244" alt="image" src="https://github.com/user-attachments/assets/560739bf-60df-4b73-84ec-bdd441663bc7" />

- I also enabled the community-id feature to make log correlation much easier when investigating a simulated attack later on.
- Now that the configurations were made to suit the lab's needs, I addded more rules to Suricata.
- I used the following commands to update Suricata's ruleset.

```Bash
sudo suricata-update
sudo suricata-update list-sources
sudo suricata-update enable-source tgreen/hunting
sudo suricata-update enable-source stamus/lateral
sudo suricata-update enable-source et/open
sudo suricata-update
sudo suricata -T -c /etc/suricata/suricata.yaml -v
sudo systemctl start suricata.service
```
- These commands will update the rule list, and sources, and include some custome ones like tgreen hunting rules that focuse on anomalies.

<img width="1085" height="277" alt="image" src="https://github.com/user-attachments/assets/2d75c0f1-acda-4108-9b9b-47d300fbde35" />

- After adding the data sources, I validated Suricata.

<img width="1887" height="347" alt="image" src="https://github.com/user-attachments/assets/ae3e8b96-eb15-4a76-8be3-4a9ca51b65b1" />

- Now Suricata is configured for this lab.
