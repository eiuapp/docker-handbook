error 之 `unable to configure the Docker daemon with file /etc/docker/daemon.json: the following directives are specified both as a flag and in the configuration file: hosts: (from flag: [fd://], from file: [tcp://0.0.0.0:2376 unix:///var/run/docker.sock])`

当参考
https://code.launchpad.net/~paskal-07/+archive/ubuntu/softethervpn
To install SoftEtherVPN type in terminal:
```
sudo apt-add-repository ppa:paskal-07/softethervpn && sudo apt-get update && sudo apt-get upgrade && sudo apt-get install softether-vpnserver
```

得到下面的日志

```
Setting up python3-distupgrade (1:18.04.34) ...
Setting up dmeventd (2:1.02.145-4.1ubuntu3.18.04.1) ...
dm-event.service is a disabled or a static unit not running, not starting it.
Setting up lvm2 (2.02.176-4.1ubuntu3.18.04.1) ...
update-initramfs: deferring update (trigger activated)
Setting up ubuntu-release-upgrader-core (1:18.04.34) ...
Setting up update-manager-core (1:18.04.11.10) ...
Setting up update-notifier-common (3.192.1.7) ...
Processing triggers for install-info (6.5.0.dfsg.1-2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for doc-base (0.10.8) ...
Processing 3 changed doc-base files...
Processing triggers for systemd (237-3ubuntu10.31) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for dbus (1.12.2-1ubuntu1.1) ...
Processing triggers for rsyslog (8.32.0-1ubuntu4) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for initramfs-tools (0.130ubuntu3.9) ...
update-initramfs: Generating /boot/initrd.img-4.15.0-65-generic
Setting up ubuntu-server (1.417.3) ...
Errors were encountered while processing:
 docker-ce
E: Sub-process /usr/bin/dpkg returned an error code (1)
root@utuntu:/home/ubuntu# docker ps
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
root@utuntu:/home/ubuntu# sudo systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: failed (Result: exit-code) since Tue 2019-10-15 15:02:08 CST; 50s ago
     Docs: https://docs.docker.com
 Main PID: 14102 (code=exited, status=1/FAILURE)

Oct 15 15:02:08 utuntu systemd[1]: docker.service: Service hold-off time over, scheduling restart.
Oct 15 15:02:08 utuntu systemd[1]: docker.service: Scheduled restart job, restart counter is at 8.
Oct 15 15:02:08 utuntu systemd[1]: Stopped Docker Application Container Engine.
Oct 15 15:02:08 utuntu systemd[1]: docker.service: Start request repeated too quickly.
Oct 15 15:02:08 utuntu systemd[1]: docker.service: Failed with result 'exit-code'.
Oct 15 15:02:08 utuntu systemd[1]: Failed to start Docker Application Container Engine.
root@utuntu:/home/ubuntu# reboot
```
开机后：

```
ubuntu@utuntu:~$ docker ps
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
ubuntu@utuntu:~$ sudo su 
root@utuntu:/home/ubuntu# journalctl -xe
Oct 15 15:03:40 utuntu gitlab-runner[1110]: time="2019-10-15T15:03:40+08:00" level=warning msg="Checking for jobs... failed" runner=k7U2n9Sb status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api/v4/job
Oct 15 15:03:41 utuntu systemd[1]: jiukun_self_runner.service: Service hold-off time over, scheduling restart.
Oct 15 15:03:41 utuntu systemd[1]: jiukun_self_runner.service: Scheduled restart job, restart counter is at 28765.
-- Subject: Automatic restarting of a unit has been scheduled
-- Defined-By: systemd
-- Support: http://www.ubuntu.com/support
-- 
-- Automatic restarting of the unit jiukun_self_runner.service has been scheduled, as the result for
-- the configured Restart= setting for the unit.
Oct 15 15:03:41 utuntu systemd[1]: Stopped GitLab Runner.
-- Subject: Unit jiukun_self_runner.service has finished shutting down
-- Defined-By: systemd
-- Support: http://www.ubuntu.com/support
-- 
-- Unit jiukun_self_runner.service has finished shutting down.
Oct 15 15:03:41 utuntu systemd[1]: Started GitLab Runner.
-- Subject: Unit jiukun_self_runner.service has finished start-up
-- Defined-By: systemd
-- Support: http://www.ubuntu.com/support
-- 
-- Unit jiukun_self_runner.service has finished starting up.
-- 
-- The start-up result is RESULT.
Oct 15 15:03:41 utuntu jiukun_self_runner[26292]: time="2019-10-15T15:03:41+08:00" level=info msg="Starting multi-runner from /home/ubuntu/.gitlab-runner/config.toml ..." builds=0
Oct 15 15:03:41 utuntu jiukun_self_runner[26292]: time="2019-10-15T15:03:41+08:00" level=info msg="Running in system-mode."
Oct 15 15:03:41 utuntu gitlab-runner[26292]: time="2019-10-15T15:03:41+08:00" level=info msg="Starting multi-runner from /home/ubuntu/.gitlab-runner/config.toml ..." builds=0
Oct 15 15:03:41 utuntu gitlab-runner[26292]: time="2019-10-15T15:03:41+08:00" level=info msg="Running in system-mode."
Oct 15 15:03:41 utuntu gitlab-runner[26292]: time="2019-10-15T15:03:41+08:00" level=info
Oct 15 15:03:41 utuntu gitlab-runner[26292]: time="2019-10-15T15:03:41+08:00" level=fatal msg="chdir /home/ubuntu/gitlabRunner: no such file or directory"
Oct 15 15:03:41 utuntu jiukun_self_runner[26292]: time="2019-10-15T15:03:41+08:00" level=info
Oct 15 15:03:41 utuntu jiukun_self_runner[26292]: time="2019-10-15T15:03:41+08:00" level=fatal msg="chdir /home/ubuntu/gitlabRunner: no such file or directory"
Oct 15 15:03:41 utuntu systemd[1]: jiukun_self_runner.service: Main process exited, code=exited, status=1/FAILURE
Oct 15 15:03:41 utuntu systemd[1]: jiukun_self_runner.service: Failed with result 'exit-code'.
Oct 15 15:03:42 utuntu jiukun_self_runner_2[1110]: time="2019-10-15T15:03:42+08:00" level=warning msg="Checking for jobs... failed" runner=obhhKvSY status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api
Oct 15 15:03:42 utuntu gitlab-runner[1110]: time="2019-10-15T15:03:42+08:00" level=warning msg="Checking for jobs... failed" runner=obhhKvSY status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api/v4/job
Oct 15 15:03:43 utuntu jiukun_self_runner_2[1110]: time="2019-10-15T15:03:43+08:00" level=warning msg="Checking for jobs... failed" runner=k7U2n9Sb status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api
Oct 15 15:03:43 utuntu gitlab-runner[1110]: time="2019-10-15T15:03:43+08:00" level=warning msg="Checking for jobs... failed" runner=k7U2n9Sb status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api/v4/job
Oct 15 15:03:45 utuntu jiukun_self_runner_2[1110]: time="2019-10-15T15:03:45+08:00" level=warning msg="Checking for jobs... failed" runner=obhhKvSY status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api
Oct 15 15:03:45 utuntu gitlab-runner[1110]: time="2019-10-15T15:03:45+08:00" level=warning msg="Checking for jobs... failed" runner=obhhKvSY status="couldn't execute POST against http://192.168.168.137/api/v4/jobs/request: Post http://192.168.168.137/api/v4/job

root@utuntu:/home/ubuntu# systemctl status docker.service 
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: failed (Result: exit-code) since Tue 2019-10-15 15:35:23 CST; 4s ago
     Docs: https://docs.docker.com
  Process: 4582 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=1/FAILURE)
 Main PID: 4582 (code=exited, status=1/FAILURE)

Oct 15 15:35:23 utuntu systemd[1]: docker.service: Service hold-off time over, scheduling restart.
Oct 15 15:35:23 utuntu systemd[1]: docker.service: Scheduled restart job, restart counter is at 3.
Oct 15 15:35:23 utuntu systemd[1]: Stopped Docker Application Container Engine.
Oct 15 15:35:23 utuntu systemd[1]: docker.service: Start request repeated too quickly.
Oct 15 15:35:23 utuntu systemd[1]: docker.service: Failed with result 'exit-code'.
Oct 15 15:35:23 utuntu systemd[1]: Failed to start Docker Application Container Engine.
root@utuntu:/home/ubuntu# ls /var/run/docker.sock 
/var/run/docker.sock
root@utuntu:/home/ubuntu# /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock 
unable to configure the Docker daemon with file /etc/docker/daemon.json: the following directives are specified both as a flag and in the configuration file: hosts: (from flag: [fd://], from file: [tcp://0.0.0.0:2376 unix:///var/run/docker.sock])
root@utuntu:/home/ubuntu# 
```

- https://github.com/moby/moby/issues/22339
- https://github.com/moby/moby/issues/22339#issuecomment-225437878

This is a problem if you are using the default systemd unit file, which is hardcoded to start dockerd with -H fd://.

quick workaround (Debian 8)): create /etc/systemd/system/docker.service.d/docker.conf

```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd
```

then 

```
systemctl daemon-reload
systemctl start docker
```

ok
