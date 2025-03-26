Description: A web application relies on the PostgreSQL 13 database present on this server. However, the connection to the database is not working. Your task is to identify and resolve the issue causing this connection failure. The application connects to a database named app1 with the user app1user and the password app1user.


Solution: 
/etc/postgresql/13/main: sudo vi pg_hba.conf  (modify the config file for postgres) 
comment out the section of the conf file that rejects all connections 
for changes to take effect, restart postgresql service: sudo systemctl restart postgresql
