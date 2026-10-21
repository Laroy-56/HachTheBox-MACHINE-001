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

Analyzing the web page we can see the main Dashboard , a page for the security snapshot , a page for ip configuration and a Network status page 

Looking at the security snapshot page :

<img width="737" height="636" alt="image" src="https://github.com/user-attachments/assets/6a926cd1-5957-4302-a532-9c8e6becc1a9" />

We can see that there is a download option that allows us to download a security snapshot. 

The ip config page  just  shows the ip configuration :

<img width="745" height="462" alt="image" src="https://github.com/user-attachments/assets/d6287a98-2102-4154-b5f0-999f76b25640" />

Finally the network status page netstat shows all network activity that has happened on the web page 

# EXPLOITATION

* Finding the Insecure Direct Object Reference
  
when navigating to the security snapshot page at the very top One interesting thing to notice is the URL scheme when creating a new capture, that is of the form 

/data/<id> 

When changing the <id> from 1 to 0 . A new page is shown with a different security snapshots downloading the pcap file (packet capture) :

<img width="747" height="587" alt="image" src="https://github.com/user-attachments/assets/c64f40af-1233-489a-96e3-5735b7b7ec02" />

When we analyze the pcap using Wireshark to look at the network traffic this is what we find   
