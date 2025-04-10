Description: There's an Nginx web server installed and managed by systemd. Running curl -I 127.0.0.1:80 returns curl: (7) Failed to connect to localhost port 80: Connection refused , fix it so when you curl you get the default Nginx page.

Test: curl -Is 127.0.0.1:80|head -1 returns HTTP/1.1 200 OK

Solution: 

1. Check nginx status: sudo systemctl status nginx.service 

         Apr 10 06:08:01 ip-172-31-73-152 systemd[1]: Starting The NGINX HTTP and reverse proxy server...
         Apr 10 06:08:02 ip-172-31-73-152 nginx[567]: nginx: [emerg] unexpected ";" in /etc/nginx/sites-enabled/default:1
         Apr 10 06:08:02 ip-172-31-73-152 nginx[567]: nginx: configuration file /etc/nginx/nginx.conf test failed
         Apr 10 06:08:02 ip-172-31-73-152 systemd[1]: nginx.service: Control process exited, code=exited, status=1/FAILURE
         Apr 10 06:08:02 ip-172-31-73-152 systemd[1]: nginx.service: Failed with result 'exit-code'.
         Apr 10 06:08:02 ip-172-31-73-152 systemd[1]: Failed to start The NGINX HTTP and reverse proxy server.

2. Remove the ';' in line 1 of the /etc/nginx/sites-enabled/defaultconfig file. 



3. Restart the nginx service: sudo systemctl restart nginx.service --> service runs successfully 


4. curl -Is 127.0.0.1:80|head -1 still shows an error HTTP/1.1 500 Internal Server Error

   Inspect the nginx service file at /etc/systemd/system/nginx.service and notice the "LimitNOFILE" term set to 10.
   Comment this out. Reload daemons and restart nginx service. 


   sudo systemctl deamon-reload
   sudo systemctl restart nginx.service 
