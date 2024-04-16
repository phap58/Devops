# Minikube
- Minikube là công cụ giúp bạn dễ dàng chạy kubernetes ngay trên máy tính của bạn.
- Các tính năng mà minikube cung cấp đó là:
  - DNS
  - NodePorts
  - ConfigMaps and Secrets
  - Dashboards
  - Container Runtime: Docker, and rkt
  - Enabling CNI (Container Network Interface)
  - Ingress

# 1. Cài đặt

- Install Virtualbox
```
sudo apt install virtualbox-qt
```

- Install Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.18.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

- Install kubectl
```
curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/v1.6.0/bin/linux/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/

```

# 2. Deploy
- Start local Kubernetes cluster:
```sh
root@adk:/home/adk# minikube start
Starting local Kubernetes cluster...
Starting VM...
SSH-ing files into VM...
Setting up certs...
Starting cluster components...
Connecting to cluster...
Setting up kubeconfig...
Kubectl is now configured to use the cluster.
```
Sau khi chạy lệnh này, môi trường minikube đã được setup xong và các bạn có thể khai báo các pods, services để chạy. 

- Kiểm tra các node có trong cluster
```sh
root@adk:/home/adk# kubectl get nodes
NAME       STATUS    AGE       VERSION
minikube   Ready     7d        v1.6.0
root@adk:/home/adk# 
```

- Để kiểm tra các pods đang chạy, bạn dùng lệnh
```sh
root@adk:/home/adk# kubectl get pods --all-namespaces
NAMESPACE     NAME                          READY     STATUS    RESTARTS   AGE
kube-system   kube-addon-manager-minikube   1/1       Running   6          7d
kube-system   kube-dns-v20-xd09t            3/3       Running   15         7d
kube-system   kubernetes-dashboard-1d83q    1/1       Running   5          7d
root@adk:/home/adk# 
```

Mặc định thì kubernetes tạo và khởi chạy các pods này.

- Xem các services đang chạy
```sh
root@adk:/home/adk# kubectl get svc --all-namespaces
NAMESPACE     NAME                   CLUSTER-IP   EXTERNAL-IP   PORT(S)         AGE
default       kubernetes             10.0.0.1     <none>        443/TCP         7m
kube-system   kube-dns               10.0.0.10    <none>        53/UDP,53/TCP   7d
kube-system   kubernetes-dashboard   10.0.0.77    <nodes>       80:30000/TCP    7d
root@adk:/home/adk# 
```
- Minikube cung cấp dashboard cho phép ta xem, tạo, chỉnh sửa các pods, services. Để khởi chạy dashboard, các bạn dùng lệnh:
```sh
minikube dashboard
```
Sau đó, truy cập vào địa chỉ http://ip:30000 để truy cập vào dashboard. Trong đó, địa chỉ ip là giá trị
```sh
minikube ip
```

![](http://storage9.static.itmages.com/i/17/0418/s_1492500264_5772794_7af103cdf2.png)

- Stop minikube
```sh
$ minikube stop
Stopping local Kubernetes cluster...
Machine stopped.
```