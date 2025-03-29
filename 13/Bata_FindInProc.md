Description: A spy has left a password in a file in /proc/sys . The contents of the file start with "secret:" (without the quotes).

Find the file and save the word after "secret:" to the file /home/admin/secret.txt with a newline at the end (e.g. if the file contents were "secret:password" do: echo "password" > /home/admin/secret.txt).


Solution: 

    cd /proc/sys 
    grep -irl "secret:"  --> cat <foundFile> 
    echo "excalibur" > /home/admin/secret.txt
