### Configure Syslog-ng to send data via 5514 port to Splunk

Login as root user using below command

```bash
sudo su
```
 

Enable syslog 

```bash
systemctl enable syslog-ng
```


Go to the directory mentioned below

```bash
cd /etc/syslog-ng
```

List the files to check if syslog-ng.conf is available

```bash
ls
```

Edit the syslog-ng.conf file

```bash
vi syslog-ng.conf
```

Add the below-listed lines to forward the data
Use your Splunk instance IP address & Port number

```bash
source tcp_log {
file("/var/log/secure");
};

destination splunk_tcp {
network("YOUR_SPLUNK_IP_ADDRESS" transport("tcp") port(5514));
};

log {
source(tcp_log);
destination(splunk_tcp);
};
```

Enable 5514 port in syslog

```bash
semanage port -a -t http_port_t -p tcp 5514
```

Restart syslog-ng service

```bash
systemctl restart syslog-ng
```

Troubleshooting:

Check if 5514 port is enabled properly

```bash
semanage port -l | grep 5514
```

```bash
egrep -i 'syslog-ng.*' /var/log/messages
```
