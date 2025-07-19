#!bin/bash
OUTPUT="failed.txt"
echo "failed logins" > OUTPUT
echo "----------------------------">> OUTPUT
grep "Failed Password" /var/log/auth.log | awk '{print $(NF - 3)}' | sort | uni>
echo "report generated: $OUTPUT"


#!bin/bash
o="m.txt"
auth="/var/log/auth.log"
sys="/var/log/syslog"
echo "malware check- $(date)" >$o
echo -e "\n failed logins" >> $o
grep "Failed password" $auth | awk '{print$(NF - 3)}' | sort | uniq -c| sort -n>
echo "root logins" >> $o
grep "accepted password.*root" $auth >> $o
echo "new user" >> $o
grep "useradd" $SYS >> $o
echo "open ports"
netstat -tulnp | grep -v "127.0.0.1" >>$o

echo "report saved $o "

#!bin/bash
og="/var/log/syslog"
output="error.txt"
echo  "system error" > $OUTPUT
echo "-----------------------" >> $OUTPUT
grep -Ei "error|fail|critical" $log >> $OUTPUT
echo "report saved in $OUTPUT”


#!bin/bash
thres=5
log="/var/log/auth.log"
blocked="blocked.txt"

grep "Failed password" $log | awk '{print $(NF_3)} |sort|uniq -c
while read count IP; do
if [ $count -ge $thres ]; then
echo "blocking $IP ($count attempts)"
ufw status | grep -qw $IP || {sudo ufw deny from $IP; >> $blocked;
fi
done
echo "done blocking ips"

