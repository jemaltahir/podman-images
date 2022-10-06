# Podman (Pod Manager)
## 1 Podman Architecture.
![image](https://user-images.githubusercontent.com/51382410/194245279-f551c680-6105-42f9-86b9-6b6899410f5d.png)

[Reference](https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#podman_pods__what_you_need_to_know)

## 2 Rootfull and Rootless conatiners using podman.
  ```
      podman run --name=logger -v /dev/log:/dev/log --rm ubuntu logger holla
      sudo journalctl
  ```
## 3 Creating pods using podman (genearte YAML for k8s + OpenShift).

## 4 Customizing binami images.

