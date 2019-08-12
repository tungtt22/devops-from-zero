# Linux log and troubleshoot 
### LINUX LOG

Linux log files are normally stored in the folder /var/logs

Linux log grouped into 4 categores:
-  Application Logs
-  Event Logs
-  Service Logs
-  System Logs
### More detail
- **/var/log/syslog** or **/var/log/messages**: system-related information
- **/var/log/auth.log** or **/var/log/secure**: store authentication logs, including both successful and failed login and authentication method
- **/var/log/boot.log**: a repository of all information related to booting and any message logged during startup
- **/var/log/maillog** or **/var/log/mail.log**: stores all logs related to mail servers
- **/var/log/kern**: store Kernel logs and warning data
- **/var/log/dmesg**: message relate to device drivers. The command dmesg can be used to view message in this file
- **/var/log/cron**: store all Crond-relate message ( cron jobs)
- **/var/log/yum.log**: store all related information about package and all component were correctly installed
- **/var/log/httpd/**: a directory containing error_log and access_log file of Apache http daemon.
    > “*error_log*” contains all errors encountered by httpd
    > “*access_log*” contains a record of all request over HTTP
- **/var/log/mysql.log** or **/var/log/mysql.log**: store all logs debug, failure and success message
Contains information about the starting, stopping and restarting of SQL deamon mysqld
- **/var/log/utmp**: current login state, by user
- **/var/log/wtm**p: login/logout history
- **/var/log/lastlog**: information about the last login for all users

### TROUBLESHOOT

```sh
    # Getting ram information
    cat /proc/meminfo
```
```sh
    # Get just the amount of ram
    cat /proc/meminfo | head -n 1
```
```sh
    # Getting cpu info
    cat /proc/cpuinfo
```
```sh
    # Check the temperature of your CPU
    cat /proc/acpi/thermal_zone/THRM/temperature
```
```sh
    # Check out how much hard drive space is left
    df -h
```
```sh
    # Kill a process
    ps -A | grep ProgramName
    kill 7207
```
For more logs just cd into the */var/log* directory and start using, **cat, less, tail, grep, find** or any other tool to view and search.
### Example

```sh
    nano <logfilename>
```
```sh
    tail <logfilename>
```

```sh
    tail –n <logfilename> ( -n how many line )
```

```sh
    tail -f -n 5 /var/log/syslog, which prints the most recent 5 lines
```
```sh
    # Find “authentication failure” in file  /var/log/auth.log and get value from column 8
    grep "authentication failure" /var/log/auth.log | cut -d '=' -f 8
```
```sh
    # Lấy cột thứ 7 của file /etc/passwd có chứa từ root
    grep root /etc/passwd|cut -d: -f7
```

# References 
1. https://www.hpe.com/us/en/insights/articles/the-first-5-things-to-do-when-your-linux-server-keels-over-1705.html
2. https://www.tecmint.com/linux-network-configuration-and-troubleshooting-commands/
3. https://www.dedoimedo.com/computers/linux-hardware-troubleshooting.html
4. https://upcloud.com/community/tutorials/troubleshoot-network-connectivity-linux-server/