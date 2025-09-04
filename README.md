# Investigating-with-ELK ( TryHackMe room ItsyBitsy )
SOC lvl 1 investigation with ELK ( THM ItsyBitsy room ) - Detecting and analyzing C2 communication

## Introduction

During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern THM:{ ________ }. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana.

Our task in this room will be to examine the network connection logs of this user, find the link and the content of the file, and answer the questions.

## Walkthrough

### **Task 1**:
**How many events were returned for the month of March 2022?**

We configure the date range in Kibana to March 2022 and we can see the number of events returned.

![](https://i.postimg.cc/52vPjkWQ/Screenshot-2025-09-04-05-42-40.png)



---


### **Task 2**:
**What is the IP associated with the suspected user in the logs?**

In the left-hand pannel, we can see the field `source_ip` which shows 2 values. By adding the second one as a filter, we find 2 results, i then searched the `destination_ip`(104.23.99.190)  with VirusTotal and confirmed that the second IP tried to connect to a malicious IP.

![](https://i.postimg.cc/44hv3m92/elk2.png)


---



### **Task 3**:
**The user’s machine used a legit windows binary to download a file from the C2 server. What is the name of the binary?**

In the `user_agent` field, we can see **'bitsadmin'** . After a quick search on Google we can confirm that `bitsadmin` is a legit windows binary that can be used to download files.

<a href="https://i.postimg.cc/1RwQrrFG/Capture-d-cran-2025-09-04-192156.png" target="_blank">
  <img src="https://i.postimg.cc/1RwQrrFG/Capture-d-cran-2025-09-04-192156.png" width="550"/>
</a>
<a href="https://i.postimg.cc/1XcbhM0b/elk3.png" target="_blank">
  <img src="https://i.postimg.cc/1XcbhM0b/elk3.png" width="200"/>
</a>


---


### **Task 4**:
**The infected machine connected with a famous filesharing site in this period, which also acts as a C2 server used by the malware authors to communicate. What is the name of the filesharing site?**

By examining the `host` field, we can identify the filesharing site name.

<a href="https://i.postimg.cc/g2XbSCtT/elk4.png" target="_blank">
  <img src="https://i.postimg.cc/g2XbSCtT/elk4.png" width="550"/>
</a>


---


### **Task 5**:
**What is the full URL of the C2 to which the infected host is connected?**

We combine the filesharing site from the previous question with the `uri` value associated with the malicious IP to obtain the full C2 URL.

![](https://i.postimg.cc/Fsxxtz8f/elk5.png)

### **Task 6**:
**A file was accessed on the filesharing site. What is the name of the file accessed?**

By visiting the full URL in a browser, we can see the file name that was accesed.

![](https://i.postimg.cc/brLc28Cm/elk7.png)

### **Task 7**:
The file contains a secret code with the format THM{_____}.

We can also see the content on the file 
