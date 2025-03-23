Description: There's a web server access log file at /home/admin/access.log. The file consists of one line per HTTP request, with the requester's IP address at the beginning of each line.

Find what's the IP address that has the most requests in this file (there's no tie; the IP is unique). Write the solution into a file /home/admin/highestip.txt. For example, if your solution is "1.2.3.4", you can do echo "1.2.3.4" > /home/admin/highestip.txt


Solution: 

cat /home/admin/access.log | awk '{print $1}' | uniq -c | sort -r | head -n 1  

echo "1.2.3.4" > /home/admin/highestip.txt
