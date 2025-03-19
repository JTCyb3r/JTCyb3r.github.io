---
layout: article
title: My CTF Methodology
mathjax: true
---
Hello! Given that the majority of posts on this website will be writeups of CTF's, I will first be detailing the methodology by which these writeups will be created.

Each of these writeups will be created under the following framework stages, with tools used detailed for each stage:

1. Reconnaissance  - Passive and active reconnaissnce to gather and enumerate information. Passive reconnaissance  would encompass the collection of publicly avaialble information like webpages, active reconnaissance  will involve direct interaction with the target systems, utilising tools like Nmap for network scanning.
2. Vulnerability Analysis - This phase involves analysing the information gathered in the previous stage to identify vulnerabilities or weak points in the system. Potential exploits or misconfigurations can be identified in this stage.
Look for potential exploits or misconfigurations.
3. Exploitation - This is the practical application of the gathered intelligence of earlier stages. I will attempt to gain intial access to the target machine through a variety of tools/exploits such as Metasploit or LFI.
4. Post-Exploitation - Once initial access is achieved, lateral movement or privilege escalation may be needed to achieve the ultimate goal.
5. Mitigation - While not typically a step of a CTF, I will list some mitigation methods so as add educational content and blue team knowledge
