# Podman (Pod Manager)
## 1 Podman Architecture.
![image](https://user-images.githubusercontent.com/51382410/194245279-f551c680-6105-42f9-86b9-6b6899410f5d.png)

[Reference](https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#podman_pods__what_you_need_to_know)

## 2 Rootfull and Rootless conatiners using podman.
### A Root container running root process
- Not Secure solution.
```
[centos@tjtestvmpodman ~]$ sudo podman run -it --rm quay.io/quay/busybox sh 
/ # whoami 
root
/ # sleep 1000 &
/ # ps aux
PID   USER     TIME  COMMAND
    1 root      0:00 sh
    7 root      0:00 sleep 1000
   10 root      0:00 ps aux
```
Ctrl-p,Ctrl-q
```
[centos@tjtestvmpodman ~]$ ps aux | grep sleep
root       39147  0.0  0.0   1300     4 pts/0    S    02:27   0:00 sleep 1000
```
### B Rootless run root process
- It is not harmfull to the host pc
```
[centos@tjtestvmpodman ~]$ podman run -it --rm quay.io/quay/busybox sh 
/ # whoami 
root
/ # sleep 2000 &
/ # ps aux
```
Ctrl-p,Ctrl-q
```
[centos@tjtestvmpodman ~]$ ps aux | grep sleep
[centos@tjtestvmpodman ~]$ ps fax
```

### C Rootful run rootless process
- Care full if the ID exisits on the host system (UID mapping)
```
[centos@tjtestvmpodman ~]$ sudo podman run -it -u 55 --rm quay.io/quay/busybox sh 
~ $ whoami 
55
~ $ sleep 3000 &
~ $ ps aux | grep sleep
    8 55        0:00 sleep 3000
   10 55        0:00 grep sleep
```
Ctrl-p,Ctrl-q
```
[centos@tjtestvmpodman ~]$ ps aux | grep sleep
[centos@tjtestvmpodman ~]$ ps fax
```

### D Rootless run rootless process
- Openshift loves it :) 

```
[centos@tjtestvmpodman ~]$ podman run -it -u 55 --rm quay.io/quay/busybox sh
~ $ whoami 
55
~ $ sleep 4000 &
~ $ ps aux
PID   USER     TIME  COMMAND
    1 55        0:00 sh
    8 55        0:00 sleep 4000
    9 55        0:00 ps aux
```
Ctrl-p,Ctrl-q
```
~ $ [centos@tjtestvmpodman ps aux | grep sleep
root       39147  0.0  0.0      0     0 pts/0    Z    02:27   0:00 [sleep] <defunct>
root       39149  0.0  0.0      0     0 pts/0    Z    02:27   0:00 [sleep] <defunct>
100054     39392  0.0  0.0   1300     4 pts/0    S    02:53   0:00 sleep 4000
centos     39395  0.0  0.0 221940  1188 pts/0    S+   02:54   0:00 grep --color=auto sleep
```
### Example of podman volume
  ```
  podman run --name=logger -v /dev/log:/dev/log --rm ubuntu logger holla
  sudo journalctl
  ```
### Summary
- Rootless conatiners do not have IP address, can not run ports >1024 , and the can be reachable using portforwarding.
## 3 Creating pods using podman (genearte YAML for k8s + OpenShift).
```
sudo podman pod create --help
sudo podman pod create
sudo podman pod list
sudo podman ps -a --pod
sudo podman run -dt --pod youthful_jones docker.io/library/alpine:latest top
sudo podman pod ps
sudo podman ps -a --pod
```
## 4 Customizing binami images.
### Matomo template use case
### Spark template use case

