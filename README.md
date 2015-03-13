# Commands

### Linux
>
>1st octet between 1 and 3 digits, 2nd, 3rd, and 4th. Space, and then 500 response
>

    grep -Eo "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}.* 500" /var/log/httpd.log >> apache.txt

>
>Read in a specific mutt profile for from domain
>

    mutt -F muttconf_apache500 -s "$SUBJECT" email@address.com < apache.txt
    mutt file: set from="Apache Tracker <email@address.com>"


Working with date in Linux

    dayofmonth=$(date +%d)
    monthname=$(date +%b)
    now=$(date +"%m-%d-%Y")


Then using date to find all unique IPs to hit webserver

    grep /var/log/httpd.log | grep "$dayofmonth/$monthname" | cut -c 1-12 | sort | uniq >> iplist.log
    grep /var/log/httpd.log | grep "$dayofmonth/$monthname" >> logdata.log


Read input at bash script

    touch /var/log/restore.log
    echo -n "What date would you like to restore from (example format 08_13_2012) :"
    read -e RESTOREDATE


Access Mysql

Description of Switches.
N: No Column Name
s: No formatting, easier to read

    mysql -h $host_name -u $user_name -p$pass_word -N -D $data_base -s -e "SELECT * from $table_name;"
    mysqldump -u $user_name --password=$pass_word $table_name > /opt/$now.sql


SSH to call another script

    ssh root@ip.add.re.ss /opt/scripts/bash.sh

Reverse Screens

    ssh -p2200 1voipsupport@ip.add.re.ss -R2222:localhost:22 -R8000:localhost:80 -R9000:localhost:443 -R4445:localhost:4445

### Excel

Never forget Excel Concatenate...

    =CONCATENATE("INSERT INTO UPSTREAM (number) VALUES (",A86,");",)
    =CONCATENATE("INSERT INTO $table_name ($1, $2, $3, $4, $5) VALUES ('",$CELL,"','$value','$value','$value','$value');",)



