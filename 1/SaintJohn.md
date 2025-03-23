Description: A developer created a testing program that is continuously writing to a log file /var/log/bad.log and filling up disk. You can check for example with tail -f /var/log/bad.log.
This program is no longer needed. Find it and terminate it.

Solution: Locate the problematic program, terminate program by process ID.  


ps -ef | grep -i problem.py | awk {'print $2'} | xargs kill -9 



