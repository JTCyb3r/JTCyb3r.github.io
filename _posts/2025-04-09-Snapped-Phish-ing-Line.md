---
title: "Writeup - Snapped Phish-ing Line"
date: 2024-03-31 10:00:00 +0000
categories: [Writeups]
tags: [phishing]
pin: false
---

## Introduction  
This is a writeup of the Snapped Phish-ing Line, on TryHackMe. This isn't a typical CTF, but rather a challenge room, focused on phishing emails. As such, it won't follow the regular format of my other writeups on here. Regardless, lets begin...

We're given a scenario brief, several employees from various departments received an unusual email, with some already having submitted their credentials to the phishing email...

*Q1:Who is the individual who received an email attachment containing a PDF?* 

We're provided 5 of these phishing emails in a .eml format. Opening them with Thunderbird we easily find which email contained a PDF attachment and who it was addressed to.
![Nmap Scan Results](/assets/TryHackMe/Lo-Fi/Nmap_Scan.png)


*Q2:What email address was used by the adversary to send the phishing emails?*

This is clearly shown in the sender address of the emails

*Q3:What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)*

Viewing the attachment in a text editor (it's safe as we're not opening it in a web browser), shows the redirection URL

We can then defang this in CyberChef

*Q4: What is the URL to the .zip archive of the phishing kit? (defanged format)*

Looking at the redirection URL in the previous question, we can see the use of the domain kennaroads.buzz

The website doesn't give us much initially


But we know of the existence of the /data/ directory from the redirection URL in the previous question, and this gives us the .zip file we are looking for. We can then defang it, for the answer to the the question.

*Q5:What is the SHA256 hash of the phishing kit archive?*

After downloading the .zip phishing kit, we can run the command sha256sum to generate the SHA256 hash of the file

*Q6:When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)*

Entering the SHA256 hash of the file onto VirusTotal provides the first submission of the file

*Q7:When was the SSL certificate the phishing domain used to host the phishing kit archive first logged? (format: YYYY-MM-DD)*

Using crt.sh, entering the kennaroads.buzz domain shows us the first logging of the SSL certificate

*Q8:What was the email address of the user who submitted their password twice?*

Heading back to kennaroads.buzz/data/, opening the Update365 file provides another file named log.txt

Inside this .txt file, we can see the email address of the user who submitted their password twice


*Q9:What was the email address used by the adversary to collect compromised credentials?*


*Q10:The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?*
*Q11:What is the hidden flag?*
