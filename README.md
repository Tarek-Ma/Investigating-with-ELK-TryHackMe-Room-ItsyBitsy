# Investigating-with-ELK ( TryHackMe room ItsyBitsy )
SOC lvl 1 investigation with ELK ( THM ItsyBitsy room ) - Detecting and analyzing C2 communication

## Introduction

During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern THM:{ ________ }. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana.

Our task in this room will be to examine the network connection logs of this user, find the link and the content of the file, and answer the questions.

## Walkthrough

### **Task 1**:
**How many events were returned for the month of March 2022?**


![](https://i.postimg.cc/52vPjkWQ/Screenshot-2025-09-04-05-42-40.png)

We configure the date range in Kibana to March 2022 and we can see the number of events returned.


---


### **Task 2**:
**What is the IP associated with the suspected user in the logs?**

![](https://i.postimg.cc/44hv3m92/elk2.png)
In the left-hand pannel, we can see the field `source_ip` which shows 2 values. By adding the second one as a filter, we find 2 results, i then searched the `destination_ip`(104.23.99.190)  with VirusTotal and confirmed that the second IP tried to connect to a malicious IP.


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


