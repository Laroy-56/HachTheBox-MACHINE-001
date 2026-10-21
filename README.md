# HachTheBox-MACHINE-001

In this exercise we will look at a Hack The Box vulnerable machine that shows how an IDOR (Insecure Direct Object Reference) can be used to break into a machine and ultimately escalate privileges on the same machine.

# INFORMATION GATHERING

Tool used - nmap (A powerful network recon tool)

<img width="702" height="262" alt="image" src="https://github.com/user-attachments/assets/a484c6e2-8319-4267-a64e-b0e221f73f94" />

As seen ports 22 - ssh , 21 - ftp and 80 - http were all open 

The interesting port was port number 80 running a webserver using Gunicorn 

Another port to look at was port 21 ftp 

# Enumeration

* Testing port 21 ftp for anonymous access

<img width="702" height="282" alt="image" src="https://github.com/user-attachments/assets/9971b386-62ca-44e7-bc30-597cee2a8618" />

As seen when using default credentials such as for the username we use anonymous and for the password also use anonymous the login fails as anonymous access is not allowed.

I then moved on to the HTTP web server running on port 80 

<img width="745" height="297" alt="image" src="https://github.com/user-attachments/assets/a8f512b1-6874-40b0-8b6c-24cb6a8cc7aa" />

Analyzing the web page we can see the main Dashboard 
