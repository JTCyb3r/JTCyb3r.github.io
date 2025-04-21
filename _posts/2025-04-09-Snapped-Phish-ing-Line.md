---
title: "Writeup - Snapped Phish-ing Line"
date: 2024-03-31 10:00:00 +0000
categories: [Writeups]
tags: [phishing]
image: /assets/TryHackMe/Snapped-Phish-ing-Line/Thumbnail.png
pin: false
---

## Introduction  
This is a writeup of the Snapped Phish-ing Line, on TryHackMe. This isn't a typical CTF, but rather a challenge room, focused on phishing emails. As such, it won't follow the regular format of my other writeups on here. Regardless, lets begin...

We're given a scenario brief, several employees from various departments received an unusual email, with some already having submitted their credentials to the phishing email...

*Q1:Who is the individual who received an email attachment containing a PDF?* 

We're provided 5 of these phishing emails in a .eml format. Opening them with Thunderbird we easily find which email contained a PDF attachment and who it was addressed to.

![Q1](/assets/TryHackMe/Snapped-Phish-ing-Line/Q1.png)


*Q2:What email address was used by the adversary to send the phishing emails?*

This is clearly shown in the sender address of the emails
![Q2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q2.png)

*Q3:What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)*

Viewing the attachment in a text editor (it's safe as we're not opening it in a web browser), shows the redirection URL
![Q3](/assets/TryHackMe/Snapped-Phish-ing-Line/Q3.png)
We can then defang this in CyberChef
![Q3_2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q3_2.png)

*Q4: What is the URL to the .zip archive of the phishing kit? (defanged format)*

Looking at the redirection URL in the previous question, we can see the use of the domain kennaroads.buzz

The website doesn't give us much initially
![Q4](/assets/TryHackMe/Snapped-Phish-ing-Line/Q4.png)

But we know of the existence of the /data/ directory from the redirection URL in the previous question, and this gives us the .zip file we are looking for. We can then defang it, for the answer to the the question.
![Q4_2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q4_2.png)

*Q5:What is the SHA256 hash of the phishing kit archive?*

After downloading the .zip phishing kit, we can run the command sha256sum to generate the SHA256 hash of the file

![Q5](/assets/TryHackMe/Snapped-Phish-ing-Line/Q5.png)

*Q6:When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)*

Entering the SHA256 hash of the file onto VirusTotal provides the first submission of the file
![Q6](/assets/TryHackMe/Snapped-Phish-ing-Line/Q6.png)

*Q7:When was the SSL certificate the phishing domain used to host the phishing kit archive first logged? (format: YYYY-MM-DD)*

Using crt.sh, entering the kennaroads.buzz domain shows us the first logging of the SSL certificate
![Q7](/assets/TryHackMe/Snapped-Phish-ing-Line/Q7.png)

*Q8:What was the email address of the user who submitted their password twice?*

Heading back to kennaroads.buzz/data/, opening the Update365 file provides another file named log.txt
![Q8](/assets/TryHackMe/Snapped-Phish-ing-Line/Q8.png)

Inside this .txt file, we can see the email address of the user who submitted their password twice
![Q8_2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q8_2.png)

*Q9:What was the email address used by the adversary to collect compromised credentials?*

To answer this, we must explore .zip file present on the /data/ directory of the website earlier. Within this zip, is a file named submit.php (We can take a wild guess what this script does...)
![Q9](/assets/TryHackMe/Snapped-Phish-ing-Line/Q9.png)

Opening this script in a text editor, and searching for "@" symbols, gives us an email address. This email address is assigned to the variable "send"
![Q9_2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q9_2.png)

*Q10:The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?*

Whilst we could manually search through each file for the email. Given that we know its structure from the question, we can use grep.

Unzipping the file, and then using the command 

```bash
grep -r "@gmail.com"
```

Gives us the following answer.
![Q10](/assets/TryHackMe/Snapped-Phish-ing-Line/Q10.png)

*Q11:What is the hidden flag?*
The hint states we are looking for a .txt file, and that with some adjustments,it should be downloadable from the phishing url, urging us to look through every directory
![Q11](/assets/TryHackMe/Snapped-Phish-ing-Line/Q11.png)

Exploring the domain, we see a folder that when opened, gives us a "Not Found" error
![Q11_2](/assets/TryHackMe/Snapped-Phish-ing-Line/Q11_2.png)

We know we are looking for a .txt file, and its a flag. So its reasonable to assume its most likely named flag.txt. Using this assumption, inputting this into the url gives us a result
![Q11_3](/assets/TryHackMe/Snapped-Phish-ing-Line/Q11_3.png)

This looks like base64, so lets head to CyberChef once more and decode it
![Q11_4](/assets/TryHackMe/Snapped-Phish-ing-Line/Q11_4.png)

It's the expected format of THM{}, but its in reverse. So lets reverse it once more
![Q11_5](/assets/TryHackMe/Snapped-Phish-ing-Line/Q11_5.png)
And that's it, the room is completed!
