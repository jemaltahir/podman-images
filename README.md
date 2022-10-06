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
- It is not harmfull to the host pc
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


### 
  ```
  
      podman run --name=logger -v /dev/log:/dev/log --rm ubuntu logger holla
      sudo journalctl
  ```

## 3 Creating pods using podman (genearte YAML for k8s + OpenShift).

## 4 Customizing binami images.

