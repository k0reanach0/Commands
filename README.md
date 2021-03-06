# Linux

##### Finds 1st octet between 1 and 3 digits, 2nd, 3rd, and 4th. Space, and then 500 response
```bash
grep -Eo "^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}.* 500" /var/log/httpd.log >> apache.txt
```

##### Read in a specific mutt profile for from domain
```bash
mutt -F muttconf_apache500 -s "$SUBJECT" email@address.com < apache.txt
mutt file: set from="Apache Tracker <email@address.com>"
```

##### Finding files older than... and deleting
```bash
for i in `find /var/log/asterisk/ -mtime +14 -print`; do echo -e "Deleting $i within asterisk log"; rm -rf $i; done;
```

##### Using Delimiter and Fields
```bash
cut -d'-' -f1 alldata.log
```

##### Working with date in Linux
```bash
dayofmonth=$(date +%d)
monthname=$(date +%b)
now=$(date +"%m-%d-%Y")
```

###### Then using date to find all unique IPs to hit webserver
```bash
grep /var/log/httpd.log | grep "$dayofmonth/$monthname" | cut -c 1-12 | sort | uniq >> iplist.log
grep /var/log/httpd.log | grep "$dayofmonth/$monthname" >> logdata.log
```

##### Read input at bash script
```bash
touch /var/log/restore.log
echo -n "What date would you like to restore from (example format 08_13_2012) :"
read -e RESTOREDATE
```

##### ZIP All December Images
`find` - searches a directory structure for files matching an expression

`xargs` - exectues an arbitrary command using the output of a previous command as arguments

`egrep` - searches for text matching a given regular expression

`identify` - retrieves image metadata (part of ImageMagick)

`cut` - extracts segments of text

`tar` - creates file archives

Individually, these are fairly simple programs. They are often useful individually, but they don't do terribly complex things.

But say you want to search through your file system and gather all of your winter holiday season pictures from any year into a single archive? Well, maybe you can find some big monolothic program that will do it for you; you might have to pay for it, it surely does way more than you need, and yet still probably won't do exactly what you want. Or instead, you can compose several simple programs to accomplish your goal:

```bash
find . -iname '*.jp*g' -print0 \
 | xargs -0 -L 1 -I @ identify -format '%[EXIF:DateTime] %d/%f\n' @ \
 | egrep '^[[:digit:]]{4}:12' \
 | cut -d' ' -f3- \
 | tar -cf december.tar -T -
```

This uses `find` to list all files ending in jpg/jpeg, then `xargs` to pass each file to identify, which lists the date each image was taken and its name. Then `egrep` filters the list down to images taken in December of any year, and `cut` trims the output to just list the December file names. Finally, `tar` takes that list of files and puts them in an archive. Again, none of these individual tasks was particularly complex; when these simple programs were composed together, though, we were able to do something rather complex.

##### Access Mysql
```bash
mysql -h $host_name -u $user_name -p$pass_word -N -D $data_base -s -e "SELECT * from $table_name;"
mysqldump -u $user_name --password=$pass_word $table_name > /opt/$now.sql
```

###### Description of Switches
- N: No Column Name
- s: No formatting, easier to read

##### SSH to call another script
```bash
ssh root@ip.add.re.ss /opt/scripts/bash.sh
```

##### Reverse Screens
```bash
ssh -p2200 1voipsupport@ip.add.re.ss -R2222:localhost:22 -R8000:localhost:80 -R9000:localhost:443 -R4445:localhost:4445
```
## Excel

##### Never forget Excel Concatenate...

    =CONCATENATE("INSERT INTO UPSTREAM (number) VALUES (",A86,");",)
    =CONCATENATE("INSERT INTO $table_name ($1, $2, $3, $4, $5) VALUES ('",$CELL,"','$value','$value','$value','$value');",)

##### Using xargs with grep for reduced log (n+1) thing
On bigger datasets I learned to love `xargs`, limiting the execs of grep to a minimum. The saving may seem small, but when you need to search millions of files, it adds up.

`find /somedir -name '*.foo' -print0 | xargs -r0 grep -H "regexp_here"`
The `-print0` and `-0` guards against whitespaces in filenames without the need for crazy escaping shenanigans.

`-r` for xargs suppresses an error message if find does not find any matching files.

##### Dont search NFS mounts
```bash
find / -name 'whatever' -xdev
```

##### htop and now atop
If you think `htop` is top on steroids; you should check out `atop` - if for no other reason than it's a daemon rather than a util and it constantly logs in a replayable format.

It's top on steroids and you can review the system state from any given time in 10 min snapshots. The `atopsar` util lets you review cpu, memory, disk, etc stats across a whole day in one command.

I've evangelised about it many a time; so here's a previous comment I made about it:
(https://www.reddit.com/r/commandline/comments/9qdknj/htop_heres_how_to_customize_it/e88jahs/)[atop]
