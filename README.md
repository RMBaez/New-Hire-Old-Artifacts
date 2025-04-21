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
- <b>8. Based on the previous answer, what were the four IDs set by the attacker? Enter the answer in order of execution. (format: 1st,2nd,3rd,4th)
</b>
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
3. <br/>

<p align="center">
    I didn't know how to find ran scheduled tasks on Splunk so I began to type scheduled task on the search bar and 'schtasks' appeared, I pressed enter and got results. The full search query was 'index=win-eventlogs schtasks'. I then clicked on the field UserName and saw several values. I looked at each user and only one of them where from the HR department.
<img width="1440" alt="Screenshot 2025-04-19 at 9 00 09 AM" src="https://github.com/user-attachments/assets/53b63351-b8b6-4555-806c-16c2b784fc5d" />





<br />
<br />
Answer:  <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>
4. </b>

<p align="center">
    I decided to filter for only the HR employees. Because there were so many commands, I decided to add the filter ' | stats count by CommandLine ' to make it easier to analyze. I looked at all the results that were executables and the only one that stood out to me was the first result that appeared.
  <img width="1440" alt="Screenshot 2025-04-19 at 9 58 15 AM" src="https://github.com/user-attachments/assets/1e747312-4d72-476e-8999-2d188e19d0b3" />
  There was a hint to this question and it read 'Explore lolbas-project.github.io/ to find binaries used to download payloads'. After doing researh on what a LOLBIN is, I googled 'lolbin certutil.exe' and read that attackers would use certutil.exe for exploitation. So now that I know I have the right command, I clicked and added the command into the search query. I looked for the field username and found the answer.
<img width="1440" alt="Screenshot 2025-04-19 at 10 20 38 AM" src="https://github.com/user-attachments/assets/7a39dbf6-59c6-4995-8443-1fdedd57246f" />





<br />
<br />
Answer:  <br/>



<h2>Program walk-through</h2>

<b>Answer the question below <br/>

5. 

<p align="center">
    The answer was discussed in the previous question.




<br />
<br />
Answer:  <br/>






<h2>Program walk-through</h2>

<b>Answer the question below <br/>

6.

<p align="center">
    Answer is part of same event as question 4.




<br />
<br />
Answer:  <br/>





<h2>Program walk-through</h2>

<b>Answer the question below <br/>
7. 

<p align="center">
     Answer is part of same event as question 4.




<br />
<br />
Answer:  <br/>




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
