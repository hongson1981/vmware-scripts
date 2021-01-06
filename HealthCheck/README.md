# Health Check script

This script can be used to check Health of automaticly created solutions in pipelines e.g. OVA Creation. This can be also used as a standalone solution.

### Features 
* ping check
* TCP port check
* http/https code status check (eg. 200)
* http/https return string check
* ICAP check if returned file is modified

### Install
```bash
sudo su -
cd /opt
mkdir healthcheck
healthcheck/
sh <(curl -s https://raw.githubusercontent.com/MariuszFerdyn/vmware-scripts/main/HealthCheck/install.sh || wget -q -O - https://raw.githubusercontent.com/MariuszFerdyn/vmware-scripts/main/HealthCheck/install.sh)
```
### Usage

Edit config.yml with checks and run using (ICAP is not working):
```bash
python3 pyCheck.py
```
If you want to display how many checks fails or use it in pipelines use:
```bash
echo $?
```
### This will add Health Check script to the cron and it will run every minute and put data to syslog:
```bash
echo '* * * * * root /opt/healthcheck/pyCheck.py | logger -t healthcheck' > /etc/cron.d/pyMonitor
```
### Filter healcheck output from syslog
```
grep 'healthcheck' /var/log/syslog
```
