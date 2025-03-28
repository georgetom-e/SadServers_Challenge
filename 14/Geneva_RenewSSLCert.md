Description: There's an Nginx web server running on this machine, configured to serve a simple "Hello, World!" page over HTTPS. However, the SSL certificate is expired.

Create a new SSL certificate for the Nginx web server with the same Issuer and Subject (same domain and company information).

Test: Certificate should not be expired: echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -dates

the subject of the certificate should be the same as the original one: echo | openssl s_client -connect localhost:443 2>/dev/null | openssl x509 -noout -subject


Solution: 

1. Backup existing certificate and key

sudo mv /etc/nginx/ssl/nginx.crt /etc/nginx/ssl/nginx.crt.bkp 
sudo mv /etc/nginx/ssl/nginx.key /etc/nginx/ssl/nginx.key.bkp


2. Create a new certificate

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt

3. Restart nginx for changes to take effect 

sudo systemctl nginx restart 
