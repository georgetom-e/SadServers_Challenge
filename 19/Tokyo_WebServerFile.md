Description: There's a web server serving a file /var/www/html/index.html with content "hello sadserver" but when we try to check it locally with an HTTP client like curl 127.0.0.1:80, nothing is returned. This scenario is not about the particular web server configuration and you only need to have general knowledge about how web servers work.



Solution: 

curl 127.0.0.1:80 times-out

1. Check the service running on port 80: netstat -tulnp | grep -w 80 --> apache2  

2. Since we're told the index.html file could be an issue, we check the assosciated permission: ls -l /var/www/html/index.html 

And we find out that only the root user has rw permission. 

We need to enable permissions for the apache2 service user. Findout the apache2 user: ps -aux | grep -w apache2 --> www-data

3. Enable owner permissions for the www-data user over the index.html file: chown www-data:www-data /var/www/html/index.html 

4. curl 127.0.0.1:80 now returns the index.html page
