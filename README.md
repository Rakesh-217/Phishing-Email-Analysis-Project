Real-world Phishing Email & Header Investigation case study
As part of my hands-on-practice as an aspiring SOC Analyst,I picked up a suspicious inbound email 
sample to investigate its authenticity Instaed of just looking at the surface level,I wanted to dig deep info the email headers and infrastructure to see where it actually came from.
Here is how I broke down step-by-step:

step 1:The Trigger & Initial Triage
when I first inspected the email,I noticed it was claiming to be from a well-known service but some thing felt off.To investigate safely without clicking any links or risking execution I pulled up the raw email headers(show original in Gmail)
Right away I Checked the email authentication tags:
SPF: Passed meaning the server sending the mail was authorized.
DKIM & DMARC: One of them failed.This immediately raised a flag,telling me that either the digital signature didn't match or it was routed through a third-party mail relay that didn't align properly
<img width="1183" height="365" alt="Screenshot_14-11-2026_162249_mail google com(1)" src="https://github.com/user-attachments/assets/b6da3d62-cc66-4b63-8269-0438dcd76d56" />

Step 2:Threat Intelligance & IP Reputation check
Since the SPF header gave me the exact IP address of the sending mail server I wanted to check its reputation globally.I copied that IP and ran it through VIRUSTOTAL to check if it has been flaged by any security vendors for spam or phishing campaigns
RESULT: 0/92 security vendors flagged this IP.
TAKEAWAY: The IP Came out completely clean and green.<img width="1756" height="736" alt="Screenshot_14-11-2026_16226_www virustotal com" src="https://github.com/user-attachments/assets/51ea6849-8b13-4fa4-ac27-14d0858f1fd1" />

Step 3: Final Conclusion / My Verdict
After correlating the data:
Even though the email triggered  a DKIM/DMARC alignment failure the underlying sending IP was fully verified by SPA and checked out 100 percent clean on VirusTotal(0/92)
VERDICT: False positive(Benign) this was not a malicious phishing attack it was likely just a legitimate automated or third-party marketing email that lacked proper DMARC configuration on the sender's end


practiced and documented by RAKESH KUMAR REBBA | Entry-level SOC ANALYST Lab



