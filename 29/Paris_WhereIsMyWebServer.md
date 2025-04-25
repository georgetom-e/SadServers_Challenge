Description: A developer put an important password on his webserver localhost:5000 . However, he can't find a way to recover it. This scenario is easy to to once you realize the one "trick".

Find the password and save it in /home/admin/mysolution , for example: echo "somepassword" > ~/mysolution

Solution: 

User-agents are what one uses to communicate with a web-server. For security reasons, sometimes user-agents like 'curl' or 'wget' are blocked. 

Netcat (nc) allows us to establish a trutsed connection to our webserser and then we request the static data using the GET HTTP request.

    admin@ip-10-1-13-44:~$ nc localhost 5000
    GET /
    
    Welcome! Password is FDZPmh5AX3oiJt
    
    
    echo "FDZPmh5AX3oiJt" > ~/mysolution
