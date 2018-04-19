# PromAnsible Install Scripts

这是用来自动化安装PromAnsible平台的Ansible脚本。

### Prepare
- install Ubuntu 16.04 Server 64bit with openssh-server
- login and run 
```
sudo apt-get install python
```
- make sure no apt process is running

### Install
- change monitor to your host actual IP addr
```
$ cat hosts
[educloud]
monitor ansible_ssh_host=192.168.96.151
```
- run comand, refer to example.txt
```
cd ~/promansible-Install
ansible-playbook playbook/monitor.yml -i hosts -u luhya -kK --extra-vars "myhost=monitor"
```
- install log as below
```
$ ansible-playbook playbook/monitor.yml -i hosts -u luhya -kK --extra-vars "myhost=monitor"
SSH password:
SUDO password[defaults to SSH password]:

PLAY [monitor] ******************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [monitor]

TASK [monitor : apt-get update] *************************************************************************************************************************************
changed: [monitor]

TASK [monitor : set MySQL root password before installing] **********************************************************************************************************
changed: [monitor]

TASK [monitor : confirm MySQL root password before installing] ******************************************************************************************************
changed: [monitor]

TASK [monitor : install mysql-server] *******************************************************************************************************************************
changed: [monitor]

TASK [monitor : create user luhya if not exist] *********************************************************************************************************************
changed: [monitor]

TASK [monitor : install monitor depends deb package] ****************************************************************************************************************
changed: [monitor] => (item=[u'libmysqld-dev', u'libmysqlclient-dev', u'memcached', u'libmemcached-tools', u'apache2', u'libapache2-mod-wsgi', u'python2.7', u'python-pip', u'python-dev', u'libssl-dev', u'libffi-dev', u'openssl', u'python-yaml', u'ifstat', u'sysstat', u'sudo', u'openssh-server', u'sshfs', u'iperf', u'iotop', u'supervisor', u'libzmq3-dev', u'ansible', u'git'])

TASK [monitor : install tornado with version 4.5.2] *****************************************************************************************************************
changed: [monitor]

TASK [monitor : install all needed python lib by pip] ***************************************************************************************************************
changed: [monitor] => (item=pip)
changed: [monitor] => (item=apscheduler)
changed: [monitor] => (item=pywinrm)
changed: [monitor] => (item=wtee)

TASK [monitor : copy monitor's deb package to target host] **********************************************************************************************************
changed: [monitor] => (item=promansible-monitor_1.1_all.deb)
changed: [monitor] => (item=promansible-daemon_1.1_all.deb)
changed: [monitor] => (item=promansible-wtee_1.1_all.deb)
changed: [monitor] => (item=prometheus-server_1.1_all.deb)
changed: [monitor] => (item=alertman-server_1.1_all.deb)
changed: [monitor] => (item=grafana-server_1.1_all.deb)
changed: [monitor] => (item=snmp-exporter_1.1_all.deb)
changed: [monitor] => (item=node-exporter_1.1_all.deb)

TASK [monitor : install monitor's deb package] **********************************************************************************************************************
changed: [monitor] => (item=promansible-monitor_1.1_all.deb)
changed: [monitor] => (item=promansible-daemon_1.1_all.deb)
changed: [monitor] => (item=promansible-wtee_1.1_all.deb)
changed: [monitor] => (item=prometheus-server_1.1_all.deb)
changed: [monitor] => (item=alertman-server_1.1_all.deb)
changed: [monitor] => (item=grafana-server_1.1_all.deb)
changed: [monitor] => (item=snmp-exporter_1.1_all.deb)
changed: [monitor] => (item=node-exporter_1.1_all.deb)

TASK [monitor : reboot the machie] **********************************************************************************************************************************
fatal: [monitor]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Shared connection to 192.168.96.151 closed.\r\n", "unreachable": true}
	to retry, use: --limit @/home/luhya/Documents/promansible-Install/playbook/monitor.retry

PLAY RECAP **********************************************************************************************************************************************************
monitor                    : ok=11   changed=10   unreachable=1    failed=0
```


