<h1>New-Hire-Old-Artifacts</h1>


<h2>Description</h2>

Scenario: You are a SOC Analyst for an MSSP (managed Security Service Provider) company called TryNotHackMe.

A newly acquired customer (Widget LLC) was recently onboarded with the managed Splunk service. The sensor is live, and all the endpoint events are now visible on TryNotHackMe's end. Widget LLC has some concerns with the endpoints in the Finance Dept, especially an endpoint for a recently hired Financial Analyst. The concern is that there was a period (December 2021) when the endpoint security product was turned off, but an official investigation was never conducted. 

Your manager has tasked you to sift through the events of Widget LLC's Splunk instance to see if there is anything that the customer needs to be alerted on. 



<h2>Questions</h2>

- <b>1. A Web Browser Password Viewer executed on the infected machine. What is the name of the binary? Enter the full path.</b>
- <b>2. What is listed as the company name?</b>
- <b>3. Another suspicious binary running from the same folder was executed on the workstation. What was the name of the binary? What is listed as its original filename? (format: file.xyz,file.xyz)</b>
- <b>4. The binary from the previous question made two outbound connections to a malicious IP address. What was the IP address? Enter the answer in a defang format.</b>
- <b>5. The same binary made some change to a registry key. What was the key path?</b>
- <b>6. Some processes were killed and the associated binaries were deleted. What were the names of the two binaries? (format: file.xyz,file.xyz)</b>
- <b>7. The attacker ran several commands within a PowerShell session to change the behaviour of Windows Defender. What was the last command executed in the series of similar commands?</b>
- <b>8. Based on the previous answer, what were the four IDs set by the attacker? Enter the answer in order of execution. (format: 1st,2nd,3rd,4th)</b>
- <b>9. What were the DLLs that were loaded from the binary from the previous question? Enter the answers in alphabetical order. (format: file1.dll,file2.dll,file3.dll)</b>



<h2>Languages and Utilities Used</h2>

- <b>Splunk</b> 


<h2>Environments Used </h2>

- <b>TryHackMe VM</b>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>

1. A Web Browser Password Viewer executed on the infected machine. What is the name of the binary? Enter the full path.

<p align="center">
  First, I adjusted the time to All TIme and in Verbose mode. Then on the search bar I wrote down ' index=main password viewer '.
<img width="1440" alt="Screenshot 2025-04-21 at 9 06 15 AM" src="https://github.com/user-attachments/assets/838a279e-be52-4ecf-8a65-b86ab590429d" />
  I went to the CommandLine field which only had one result. I clicked it and saw two commands but only one was an executable.
<img width="1440" alt="Screenshot 2025-04-21 at 9 07 53 AM" src="https://github.com/user-attachments/assets/6c552bae-9d11-4a7c-bff9-a2a06887465f" />




<br />
<br />
Answer: C:\Users\FINANC~1\AppData\Local\Temp\11111.exe  <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
2. What is listed as the company name?

<p align="center">
   I added the command line from question 1 into the search bar. I looked at the field Company and there was the answer.
<img width="1440" alt="Screenshot 2025-04-21 at 9 12 34 AM" src="https://github.com/user-attachments/assets/30e436b2-efd9-4bc0-87f8-df7ca36790e8" />






<br />
<br />
Answer: NirSoft<br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
3. Another suspicious binary running from the same folder was executed on the workstation. What was the name of the binary? What is listed as its original filename? (format: file.xyz,file.xyz)

<p align="center">
    I removed the previous search filters except for 'index=main'. I added 'EventCode=1' since it is for process creation. I went to the field CurrentDirectory and selceted 'C:\Users\Finance01\AppData\Local\Temp\'.
<img width="1440" alt="Screenshot 2025-04-21 at 9 52 47 AM" src="https://github.com/user-attachments/assets/86c55c55-cbdb-4610-8036-f93309667154" />
    I went down to the field 'Images" which contained the answer to the first question. I selected and clicked on the result 'C:\Users\Finance01\AppData\Local\Temp\IonicLarge.exe'.
<img width="1440" alt="Screenshot 2025-04-21 at 10 00 11 AM" src="https://github.com/user-attachments/assets/56f81ac3-a934-4cd0-bb6c-9c66c5953ce8" />
    I went dow to the field 'OriginalFileName which one had one result. That was the answer to the second question.
<img width="1440" alt="Screenshot 2025-04-21 at 10 02 51 AM" src="https://github.com/user-attachments/assets/3e3a6333-2351-4587-96da-85ae43962afe" />




<br />
<br />
Answer: IonicLarge.exe,PalitExplorer.exe <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
4. The binary from the previous question made two outbound connections to a malicious IP address. What was the IP address? Enter the answer in a defang format.

<p align="center">
    I filtered the binary 'IonicLarge.exe' into the search bar. I went to the field 'DestinationIp' and look for any connection(s) made twice to the same ip. Only one did. Defang the ip and that is the answer.
<img width="1440" alt="Screenshot 2025-04-21 at 10 09 58 AM" src="https://github.com/user-attachments/assets/c983acea-f9a5-430d-a2c1-225c11cdf949" />




<br />
<br />
Answer: 2[.]56[.]59[.]42 <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

5. The same binary made some change to a registry key. What was the key path?

<p align="center">
    I filtered the binary 'IonicLarge.exe' into the search bar. I then went to the field 'EventType' and added 'CreateKey' filter into the search bar. The first event contained the answer
    <img width="1440" alt="Screenshot 2025-04-21 at 10 31 12 AM" src="https://github.com/user-attachments/assets/7fe1dc3a-d543-4284-af55-5a0633a28507" />





<br />
<br />
Answer:  HKLM\SOFTWARE\Policies\Microsoft\Windows Defender<br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>

6. Some processes were killed and the associated binaries were deleted. What were the names of the two binaries? (format: file.xyz,file.xyz)

<p align="center">
    There was a hint to this question and it said Process were killed with 'taskkill /im'. I added it into the search bar. Received 5 events. I went to the field 'CommandLine' where the answer could be found.
<img width="1440" alt="Screenshot 2025-04-21 at 10 52 16 AM" src="https://github.com/user-attachments/assets/003c3e7d-b529-4f79-8671-d26cde9b80a0" />




<br />
<br />
Answer: WvmIOrcfsuILdX6SNwIRmGOJ.exe, phcIAmLJMAIMSa9j9MpgJo1m.exe <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
7. The attacker ran several commands within a PowerShell session to change the behaviour of Windows Defender. What was the last command executed in the series of similar commands?

<p align="center">
     I added powershell into the search since I was looking for a powershell command. I need to organize the data some more so I added the command “| Table _time CommandLine” to make a list and "| dedup CommandLine" to remove duplicates.
  <img width="1440" alt="Screenshot 2025-04-21 at 11 13 10 AM" src="https://github.com/user-attachments/assets/4a2cc1fa-e7a0-4abe-bc51-ff81befe9c7a" />





<br />
<br />
Answer: powershell WMIC /NAMESPACE:\\root\Microsoft\Windows\Defender PATH MSFT_MpPreference call Add ThreatIDDefaultAction_Ids=2147737394 ThreatIDDefaultAction_Actions=6 Force=True <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
8. 



<p align="center">
    Answer is part of same event as question 4.





<br />
<br />
Answer: <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
9. 

<p align="center">
   I copied and pasted the url ' https[:]//controlc[.]com/e4d11035 '(in its fanged format) into the website VirusTotal. I went to the detail section and kept scrolling until the saw the pattern mentioned in the question
<img width="1440" alt="Screenshot 2025-04-19 at 10 36 13 AM" src="https://github.com/user-attachments/assets/27da7b70-1c00-417c-96c4-6a9f0a3162d4" />






<br />
<br />
Answer: <br/>




<h2>Program walk-through</h2>

<b>Answer the question below <br/>
10. 

<p align="center">
   The answer is found in the same event as in question 4.






<br />
<br />
Answer: <br/>
