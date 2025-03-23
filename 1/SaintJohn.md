Description: A developer created a testing program that is continuously writing to a log file /var/log/bad.log and filling up disk. You can check for example with tail -f /var/log/bad.log.
This program is no longer needed. Find it and terminate it.

Solution: Locate the problematic program, terminate program's process by process ID.  

find -type f -iname bad*  --> badlog.py 

ps -ef | grep badlog.py | awk '{print $2}'| head -n 1 | xargs kill -9 



