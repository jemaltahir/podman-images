# Container networking

## 1. Running two Podman Containers
### **Step 1: Creating a Custom nginx Image with Network Utilities**
1. Create a `Dockerfile` for your custom nginx image:
```Dockerfile
FROM nginx:latest

RUN apt-get update && apt-get install -y \
    net-tools \
    iproute2 \
    dnsutils \
    iputils-ping \
    curl \
    && rm -rf /var/lib/apt/lists/*
```

2. Build the custom image:
```bash
podman build -t customnginx-nettools .
```

### **Step 2: Run the Two Containers**

1. Run the first container:
```bash
podman run -d --name nginx1 customnginx-nettools
```

2. Run the second container:
```bash
podman run -d --name nginx2 customnginx-nettools
```

### **Step 3: Check Container IPs and Try to Reach One from Another**

1. Get the IP address of `nginx1`:
```bash
podman inspect nginx1 | grep IPAddress
```
Note down the IP (let's say it's `IP1`).
why is it empty?

2. Get the IP address of `nginx2`:
```bash
podman inspect nginx2 | grep IPAddress
```
Note down the IP (let's say it's `IP2`).
Why is it empty?

Rerun using sudo the above steps then continue...

3. Check reachability from `nginx1` to `nginx2` using IP:

Enter the shell of `nginx1`:
```bash
podman exec -it nginx1 /bin/bash
```

Inside the shell, ping `nginx2` using `IP2`:
```bash
ping IP2
```

### **Step 4: Test reachability of the nginx service running from host**

```bash
http://IP1 or http://IP2
```
why it is not reachable?
