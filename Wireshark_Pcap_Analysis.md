<h1 align="center">
    <img src="https://readme-typing-svg.herokuapp.com/?font=Righteous&size=35&center=true&vCenter=true&width=500&height=70&duration=4000&lines=Hi+There!+👋;+I'm+Guillermo!;" />
</h1>
 </div>
 <div align="center"> 
  <a href="https://linkedin.com/in/knowledgeseeker" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank" />
  </a>
  <a href="https://tryhackme.com/p/ECyberTekTrooper" target="_blank">
     <img src="https://img.shields.io/badge/TryHackMe-212121?style=for-the-badge&logo=tryhackme" target="_blank" /> <!-- sqlite, safari, google-chrome are other good icon options -->
  </a>
</div>

## 🚀 Challenge Introduction

This challenge involves analyzing a packet capture (pcap) of malicious activity, focusing on understanding and interpreting network traffic associated with potential malware infections. It tests us by answering the following questions on the analysis.

## 👋 Questions to answer

- When did the malicious traffic start in UTC?
- What is the victim’s IP address?
- What is the victim’s MAC address? 
- What is the victim’s Windows host name?
- What is the victim’s Windows user account name?
- How much RAM does the victim’s host have?
- What type of CPU is used by the victim’s host?
- What is the public IP address of the victim’s host?
- What type of account login data was stolen by the malware?

## 🕵️ Network traffic analysis

Upon initial inspection of our pcap file, we observe that the first line begins with a broadcast asking "who has 192.168.1.27," followed by the router's response providing the associated MAC address. We must verify that this IP address and MAC address correspond to the potential victim data we are investigating.

![img1.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img1.png?raw=true)

➡️ A few packets down, we immediately observe a GET request for a PNG file.

![img2.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img2.png?raw=true)

➡️ Upon examining the file, it's evident that the data is encoded.

![img3.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img3.png?raw=true)

➡️ When we research a bit further into the flowchart of this malware from the image provided below, we can see the infection process of a variant of Agent Tesla malware, detailing HTTP traffic for encoded payload delivery.

![img4.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img4.png?raw=true)

➡️ From this information, we can derive that the source IP address 192.168.1.27 requested this PNG file, confirming it as our infected host. We can document the information provided, noting that the victim's IP address is 192.168.1.27, and the MAC address can be copied from this request.

![img5.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img5.png?raw=true)

### This discovery answers the following questions: 

- **What is the victim’s IP address?** <red>192.168.1.27</red>


![img6.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img6.png?raw=true)

- **What is the victim’s MAC address?** bc:ea:fa:22:74:fb

➡️ Next, our task is to determine when the malicious traffic started. To find this information, we can inspect the payload request and examine the headers to locate the time and date.

![img7.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img7.png?raw=true)

- **When did the malicious traffic start in UTC?** 05 Jan 2023 22:51:00

➡️ Our next question asks us about the victim's Windows host name and user account name, so our first step is to filter for Windows traffic, such as NBNS and SMB, on the network. This will allow us to identify commonly generated Windows communications, including host names and user account names.

![img8.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img8.png?raw=true)


➡️ If we examine the packet under the Microsoft Windows Browser Protocol, the "Master Browser Server Name" field indicates the name of the computer currently acting as the Master Browser on the network is "DESKTOP-WIN11PC".

![img9.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img9.png?raw=true)

- **What is the victim’s Windows host name?** DESKTOP-WIN11PC

➡️ Our next question is asking us to find the victim's Windows user name. To do this, we look at SMTP traffic, and by following the TCP stream, we can see exfiltrated data from the email includes the infected PC's username, "Windows11user," which we can use as the user account name.

![img10.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img10.png?raw=true)


- **What is the victim’s Windows user account name?** windows11user

➡️ Our next question asks us about the type of CPU used by the victim's host and how much RAM the victim has. This information can be found in the same exfiltrated data from the email in the TCP stream.

![img11.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img11.png?raw=true)

- **What type of CPU is used by the victim’s host?** Intel® Core™ i5-13600K CPU @ 5.10GHz
  
![img12.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img12.png?raw=true)

- **How much RAM does the victim’s host have?** 32GB

➡️ Then it asks us what the public IP address of the victim's host is. This can also be found in the email.

![img13.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img13.png?raw=true)


- **What is the public IP address of the victim’s host?** 173.66.46.112

➡️ Our final question pertains to the type of account login data that the malware has acquired.

![img14.png](https://github.com/ETEKTrooper/wireshark_analysis/blob/main/img14.png?raw=true)


- **What type of account login data was stolen by the malware?** The malware stole usernames and passwords from multiple accounts, including email, social media, and shopping websites.

## 🏁 Conclusion

This real-world example demonstrates the importance of analyzing packet captures (pcap) to understand and interpret network traffic associated with potential malware infections.


