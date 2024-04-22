
# Introduction

Now, I will answer questions to finish labs from [K8S Labs](https://beta.kodekloud.com/user/courses/udemy-labs-online-kubernetes-lab-for-beginners-hands-on/module/bdce9f5e-32e6-4727-ad5c-b9f93f69e093/lesson/7371c82a-edab-42bb-986a-3fe401f4130a?utm_source=udemy&utm_medium=labs&utm_campaign=kubernetes ) on KodeKloud platform.

# Labs: Familiarize with Lab Environment
## câu1
Question:
```bash
How many nodes are part of the cluster?
```

Answer:
```bash
➜  kubectl get nodes
Client: 
NAME           STATUS   ROLES                  AGE   VERSION
controlplane   Ready    control-plane,master   19m   v1.29.0+k3s1
```

## câu2
Question:
```bash
What is the version of Kubernetes running on the nodes ?
```

Answer:
```bash
➜  kubectl get nodes
➜  kubectl version 
Client:
Client Version: v1.29.0+k3s1
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.29.0+k3s1
```

# caau3:
Question:
```bash
What is the flavor and version of Operating System on which the Kubernetes nodes are running?
```

Anser:
```bash
➜  uname -a
Client:
Linux controlplane 5.4.0-1106-gcp #115~18.04.1-Ubuntu SMP Mon May 22 20:46:39 UTC 2023 x86_64 Linux

➜  cat /etc/os-release
client:
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.16.8
PRETTY_NAME="Alpine Linux v3.16"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"


```

# Labs: PODs with YAML

## caau1:
Question:
```bash
How many pods exist on the system?

In the current(default) namespace.
```

Answer:
```bash
➜  kubectl get pods --namespace=default | grep -c ' '
client:
No resources found in default namespace.
0

```

## caau2:
Question:
```bash
Create a new pod with the nginx image.
```

Answer:
```bash
➜  sudo nano nginx-pod.yaml

        apiVersion: v1
        kind: Pod
        metadata:
        name: nginx-pod
        spec:
        containers:
        - name: nginx-container
            image: nginx

➜  kubectl apply -f nginx-pod.yaml
client:
pod/nginx-pod created

➜  kubectl get pods
client: NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          59s
```

## caau3:
Question:
```bash
How many pods are created now?

Note: We have created a few more pods. So please check again.
```

Answer:
```bash
kubectl get pods --namespace=default
client:
NAME            READY   STATUS    RESTARTS   AGE
nginx-pod       1/1     Running   0          3m40s
newpods-6gd7x   1/1     Running   0          2m4s
newpods-4czgh   1/1     Running   0          2m4s
newpods-xxckx   1/1     Running   0          2m4s
```

## caau4:

Question:
```bash
What is the image used to create the new pods?

You must look at one of the new pods in detail to figure this out.
```

Answer:
```bash
➜  kubectl describe pod newpods-6gd7x 
client:
Name:             newpods-6gd7x
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.5.114.3
Start Time:       Mon, 22 Apr 2024 03:49:19 +0000
Labels:           tier=busybox
Annotations:      <none>
Status:           Running
IP:               10.42.0.12
IPs:
  IP:           10.42.0.12
Controlled By:  ReplicaSet/newpods
Containers:
  busybox:
    Container ID:  containerd://e4b1b479eb637c37d7846166cb010bf9a86a2639b5f995f14f504b91cf4e67a7
    Image:         busybox
    Image ID:      docker.io/library/busybox@sha256:c3839dd800b9eb7603340509769c43e146a74c63dca3045a8e7dc8ee07e53966
    Port:          <none>
    Host Port:     <none>
    Command:
      sleep
      1000
    State:          Running
      Started:      Mon, 22 Apr 2024 03:49:23 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-78nzf (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-78nzf:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  7m8s  default-scheduler  Successfully assigned default/newpods-6gd7x to controlplane
  Normal  Pulling    7m6s  kubelet            Pulling image "busybox"
  Normal  Pulled     7m6s  kubelet            Successfully pulled image "busybox" in 260ms (260ms including waiting)
  Normal  Created    7m6s  kubelet            Created container busybox
  Normal  Started    7m5s  kubelet            Started container busybox

```

## caau5:
Question: 
```bash
Which nodes are these pods placed on?

You must look at all the pods in detail to figure this out.
```

Answer:
```bash
➜  kubectl get pods --all-namespaces -o wide
client:
NAMESPACE     NAME                                      READY   STATUS      RESTARTS   AGE   IP           NODE           NOMINATED NODE   READINESS GATES
kube-system   local-path-provisioner-84db5d44d9-2s26k   1/1     Running     0          39m   10.42.0.2    controlplane   <none>           <none>
kube-system   coredns-6799fbcd5-2vlwq                   1/1     Running     0          39m   10.42.0.3    controlplane   <none>           <none>
kube-system   helm-install-traefik-crd-j84wh            0/1     Completed   0          39m   10.42.0.4    controlplane   <none>           <none>
kube-system   svclb-traefik-6b1f7970-zr88r              2/2     Running     0          39m   10.42.0.7    controlplane   <none>           <none>
kube-system   helm-install-traefik-5grkk                0/1     Completed   1          39m   10.42.0.6    controlplane   <none>           <none>
kube-system   metrics-server-67c658944b-w6t5j           1/1     Running     0          39m   10.42.0.5    controlplane   <none>           <none>
kube-system   traefik-f4564c4f4-gr74m                   1/1     Running     0          39m   10.42.0.8    controlplane   <none>           <none>
default       nginx-pod                                 1/1     Running     0          12m   10.42.0.9    controlplane   <none>           <none>
default       newpods-6gd7x                             1/1     Running     0          11m   10.42.0.12   controlplane   <none>           <none>
default       newpods-4czgh                             1/1     Running     0          11m   10.42.0.10   controlplane   <none>           <none>
default       newpods-xxckx                             1/1     Running     0          11m   10.42.0.11   controlplane   <none>           <none>

```

## caau6:
Question:
```bash
How many containers are part of the pod webapp?

Note: We just created a new POD. Ignore the state of the POD for now.
```

Answer:
```bash
➜  kubectl describe pod webapp
client:
Name:             webapp
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.5.114.3
Start Time:       Mon, 22 Apr 2024 04:01:05 +0000
Labels:           <none>
Annotations:      <none>
Status:           Pending
IP:               10.42.0.13
IPs:
  IP:  10.42.0.13
Containers:
  nginx:
    Container ID:   containerd://7b8b47cc21e7b1f5ce92d553e12a450c41b566fa283e37602b79cb8d89852777
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:0463a96ac74b84a8a1b27f3d1f4ae5d1a70ea823219394e131f5bf3536674419
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Mon, 22 Apr 2024 04:01:06 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-df84f (ro)
  agentx:
    Container ID:   
    Image:          agentx
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-df84f (ro)
```

## caau7:
Question:
```bash
What images are used in the new webapp pod?

You must look at all the pods in detail to figure this out.
```

Answer:
```bash
➜  kubectl get pod webapp -o jsonpath="{.spec.containers[*].image}"
client:
nginx agentx
```

## caua8:

Question:
```bash
What is the state of the container agentx in the pod webapp?

Wait for it to finish the ContainerCreating state
```

Answer:
```bash
➜  kubectl get pods webapp -w
client:
NAME     READY   STATUS             RESTARTS   AGE
webapp   1/2     ImagePullBackOff   0          7m52s

➜  kubectl wait pod/webapp --for=condition=containerReady=agentx
client:
error: timed out waiting for the condition on pods/webapp
```

## caau9:

Question:
```bash
Why do you think the container agentx in pod webapp is in error?

Try to figure it out from the events section of the pod.
```

Answer:
```bash
➜  kubectl describe pod webapp
client:

```

## caau10:
Question:
```bash
Delete the webapp Pod.


Once deleted, wait for the pod to fully terminate.
```

Answer:
```bash
➜  kubectl delete pod webapp --wait=true
client:
pod "webapp" deleted

```

## caau11:
Question:
```bash
Create a new pod with the name redis and the image redis123.


Use a pod-definition YAML file. And yes the image name is wrong!
```
Answer:
```bash
➜  sudo nano redis-pod.yaml

        apiVersion: v1
        kind: Pod
        metadata:
        name: redis
        spec:
        containers:
        - name: redis
            image: redis123 # Use the official redis image
            ports:
            - containerPort: 6379

➜  kubectl apply -f redis-pod.yaml
client
pod/redis created
```

## caau12:
Question:
```bash
Now change the image on this pod to redis.


Once done, the pod should be in a running state.
```





Answer:
```bash
➜  kubectl set image pod redis redis=redis
client:
pod/redis image updated

➜  kubectl get pods
client:

NAME            READY   STATUS    RESTARTS        AGE
nginx-pod       1/1     Running   0               44m
newpods-4czgh   1/1     Running   2 (9m49s ago)   43m
newpods-6gd7x   1/1     Running   2 (9m49s ago)   43m
newpods-xxckx   1/1     Running   2 (9m49s ago)   43m
redis           1/1     Running   1 (6m55s ago)   8m39s
```

# Labs: Replica Sets
## caau1:
Question:
```bash
How many PODs exist on the system?

In the current(default) namespace.
```

Answer:
```bash
➜  kubectl get pods
Client:
No resources found in default namespace.
```

## caau2: 
Question:
```bash
How many ReplicaSets exist on the system?

In the current(default) namespace.
```

Answer:
```bash
 ➜  kubectl get ReplicaSets
Client:
No resources found in default namespace.
```

## caau3:
Question:
```bash
How about now? How many ReplicaSets do you see?

We just made a few changes!
```

Answer:
```bash
➜  kubectl get ReplicaSets
Client:
NAME              DESIRED   CURRENT   READY   AGE
new-replica-set   4         4         0       106s

```

## caau4:
Question:
```bash
How many PODs are DESIRED in the new-replica-set?
```

Answer:
```bash
➜  kubectl get replicaset new-replica-set -o yaml
Client:
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  creationTimestamp: "2024-04-22T06:49:15Z"
  generation: 1
  name: new-replica-set
  namespace: default
  resourceVersion: "891"
  uid: ca1af2f1-8261-4ae8-a652-06038dc45220
spec:
  replicas: 4
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      creationTimestamp: null
      labels:
        name: busybox-pod
    spec:
      containers:
      - command:
        - sh
        - -c
        - echo Hello Kubernetes! && sleep 3600
        image: busybox777
        imagePullPolicy: Always
        name: busybox-container
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  fullyLabeledReplicas: 4
  observedGeneration: 1
  replicas: 4
```

## caau5:
Question:
```bash
What is the image used to create the pods in the new-replica-set?
```

Answer:
```bash
➜  kubectl get replicaset new-replica-set -o yaml
Client:
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  creationTimestamp: "2024-04-22T06:49:15Z"
  generation: 1
  name: new-replica-set
  namespace: default
  resourceVersion: "891"
  uid: ca1af2f1-8261-4ae8-a652-06038dc45220
spec:
  replicas: 4
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      creationTimestamp: null
      labels:
        name: busybox-pod
    spec:
      containers:
      - command:
        - sh
        - -c
        - echo Hello Kubernetes! && sleep 3600
        image: busybox777
        imagePullPolicy: Always
        name: busybox-container
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  fullyLabeledReplicas: 4
  observedGeneration: 1
  replicas: 4
```

## caau6:
Question:
```bash
How many PODs are READY in the new-replica-set?
```

Answer:
```bash
➜  kubectl get pods
Client:
NAME                    READY   STATUS             RESTARTS   AGE
new-replica-set-s742v   0/1     ImagePullBackOff   0          9m57s
new-replica-set-r7m25   0/1     ImagePullBackOff   0          9m57s
new-replica-set-zxzk9   0/1     ImagePullBackOff   0          9m57s
new-replica-set-hzhz6   0/1     ImagePullBackOff   0          9m57s
```

## caau7:
Question:
```bash
Why do you think the PODs are not ready?
```

Answer:
```bash
➜  kubectl describe pods
client: 
Name:             new-replica-set-hzhz6
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.10.255.9
Start Time:       Mon, 22 Apr 2024 06:49:15 +0000
Labels:           name=busybox-pod
Annotations:      <none>
Status:           Pending
IP:               10.42.0.9
IPs:
  IP:           10.42.0.9
Controlled By:  ReplicaSet/new-replica-set
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox777
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8kkwp (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-8kkwp:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  12m                   default-scheduler  Successfully assigned default/new-replica-set-hzhz6 to controlplane
  Normal   Pulling    10m (x4 over 12m)     kubelet            Pulling image "busybox777"
  Warning  Failed     10m (x4 over 12m)     kubelet            Failed to pull image "busybox777": failed to pull and unpack image "docker.io/library/busybox777:latest": failed to resolve reference "docker.io/library/busybox777:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     10m (x4 over 12m)     kubelet            Error: ErrImagePull
  Warning  Failed     10m (x6 over 12m)     kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m26s (x42 over 12m)  kubelet            Back-off pulling image "busybox777"


Name:             new-replica-set-s742v
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.10.255.9
Start Time:       Mon, 22 Apr 2024 06:49:15 +0000
Labels:           name=busybox-pod
Annotations:      <none>
Status:           Pending
IP:               10.42.0.11
IPs:
  IP:           10.42.0.11
Controlled By:  ReplicaSet/new-replica-set
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox777
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-jh6dd (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-jh6dd:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  12m                   default-scheduler  Successfully assigned default/new-replica-set-s742v to controlplane
  Normal   Pulling    10m (x4 over 12m)     kubelet            Pulling image "busybox777"
  Warning  Failed     10m (x4 over 12m)     kubelet            Failed to pull image "busybox777": failed to pull and unpack image "docker.io/library/busybox777:latest": failed to resolve reference "docker.io/library/busybox777:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     10m (x4 over 12m)     kubelet            Error: ErrImagePull
  Warning  Failed     10m (x6 over 12m)     kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m28s (x42 over 12m)  kubelet            Back-off pulling image "busybox777"


Name:             new-replica-set-r7m25
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.10.255.9
Start Time:       Mon, 22 Apr 2024 06:49:15 +0000
Labels:           name=busybox-pod
Annotations:      <none>
Status:           Pending
IP:               10.42.0.12
IPs:
  IP:           10.42.0.12
Controlled By:  ReplicaSet/new-replica-set
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox777
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-tf49k (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-tf49k:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  12m                   default-scheduler  Successfully assigned default/new-replica-set-r7m25 to controlplane
  Normal   Pulling    10m (x4 over 12m)     kubelet            Pulling image "busybox777"
  Warning  Failed     10m (x4 over 12m)     kubelet            Failed to pull image "busybox777": failed to pull and unpack image "docker.io/library/busybox777:latest": failed to resolve reference "docker.io/library/busybox777:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     10m (x4 over 12m)     kubelet            Error: ErrImagePull
  Warning  Failed     10m (x6 over 12m)     kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m23s (x42 over 12m)  kubelet            Back-off pulling image "busybox777"


Name:             new-replica-set-zxzk9
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.10.255.9
Start Time:       Mon, 22 Apr 2024 06:49:15 +0000
Labels:           name=busybox-pod
Annotations:      <none>
Status:           Pending
IP:               10.42.0.10
IPs:
  IP:           10.42.0.10
Controlled By:  ReplicaSet/new-replica-set
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox777
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-frn8m (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-frn8m:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  12m                   default-scheduler  Successfully assigned default/new-replica-set-zxzk9 to controlplane
  Normal   Pulling    11m (x4 over 12m)     kubelet            Pulling image "busybox777"
  Warning  Failed     11m (x4 over 12m)     kubelet            Failed to pull image "busybox777": failed to pull and unpack image "docker.io/library/busybox777:latest": failed to resolve reference "docker.io/library/busybox777:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     11m (x4 over 12m)     kubelet            Error: ErrImagePull
  Warning  Failed     10m (x6 over 12m)     kubelet            Error: ImagePullBackOff
  Normal   BackOff    2m27s (x42 over 12m)  kubelet            Back-off pulling image "busybox777"

➜  
```

## caau8:

Question:
```bash
Delete any one of the 4 PODs.
```

Answer:
```bash
➜  kubectl get pods
NAME                    READY   STATUS             RESTARTS   AGE
new-replica-set-hzhz6   0/1     ImagePullBackOff   0          15m
new-replica-set-s742v   0/1     ImagePullBackOff   0          15m
new-replica-set-r7m25   0/1     ImagePullBackOff   0          15m
new-replica-set-zxzk9   0/1     ImagePullBackOff   0          15m

➜  kubectl delete pod
 new-replica-set-hzhz6 
pod "new-replica-set-hzhz6" deleted

➜  kubectl delete pod new-replica-set-s742v 
pod "new-replica-set-s742v" deleted

➜  kubectl delete pod new-replica-set-r7m25 
pod "new-replica-set-r7m25" deleted

➜  kubectl delete pod new-replica-set-zxzk9 
pod "new-replica-set-zxzk9" deleted

```

## caau9:
Question:
```bash
How many PODs exist now?
```

Answer:
```bash
➜  kubectl get pods
client:
NAME                    READY   STATUS             RESTARTS   AGE
new-replica-set-ls92v   0/1     ImagePullBackOff   0          94s
new-replica-set-zzhsz   0/1     ImagePullBackOff   0          87s
new-replica-set-9dgcp   0/1     ErrImagePull       0          103s
new-replica-set-l65xn   0/1     ErrImagePull       0          115s

```

## caau10: 
Question:
```bash
Create a ReplicaSet using the replicaset-definition-1.yaml file located at /root/.


There is an issue with the file, so try to fix it.
```

Answer:
```bash
 ➜  ls -l /root/replicaset-definition-1.yaml
 client: 
-rw-r--r--    1 root     root           275 Apr 22 07:23 /root/replicaset-definition-1.yaml

➜  sudo nano replicaset-definition-1.yaml 

client: sửa("apiVersion: v1" -> "apiVersion: app/v1")
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx

 ➜  kubectl apply -f replicaset-definition-1.yaml
 CLient:
replicaset.apps/replicaset-1 created

```
## caau12:
Question:
```bash
Fix the issue in the replicaset-definition-2.yaml file and create a ReplicaSet using it.


This file is located at /root/.
```

Answer:
```bash
 ➜  sudo nano replicaset-definition-2.yaml 
client: sửa {
    selector:
    matchLabels:
      tier: frontend
    thành
    selector:
    matchLabels:
      tier: nginx}

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-2
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: nginx
  template:
    metadata:
      labels:
        tier: nginx
    spec:
      containers:
        - name: nginx
          image: nginx

➜  kubectl apply -f replicaset-definition-2.yaml
client: 

replicaset.apps/replicaset-2 created
```

## caau13:
Question:
```bash
Delete the two newly created ReplicaSets - replicaset-1 and replicaset-2
```

Answer:
```bash
 ➜  kubectl delete rs replicaset-1
 client:
replicaset.apps "replicaset-1" deleted

controlplane ~ ➜  kubectl delete rs replicaset-2
client:
replicaset.apps "replicaset-2" deleted
```

# Labs: Deployments

## caau1:
Question:
```bash
How many PODs exist on the system?

In the current(default) namespace.
```
Answer:
```bash
➜  kubectl get pods
client:
No resources found in default namespace.
```

## caau2:
Question:
```bash
How many Deployments exist on the system?

In the current(default) namespace.
```

Answer:
```bash
➜  kubectl get Deployments --namespace=default
client: 
No resources found in default namespace.
```

## caau3:
Question:
```bash
How many Deployments exist on the system now?

We just created a Deployment! Check again!
```

Answer:
```bash
 ➜  kubectl get Deployments
 client:
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
frontend-deployment   0/4     4            0           4m20s

```

## caau4:
Question:
```bash
How many ReplicaSets exist on the system now?
```

Answer:
```bash
➜  kubectl get ReplicaSets
client:
NAME                             DESIRED   CURRENT   READY   AGE
frontend-deployment-7b9984b987   4         4         0       5m13s
```

## caau5:
Question:
```bash
How many PODs exist on the system now?
```

Answer:
```bash
➜  kubectl get Pods
client:
NAME                                   READY   STATUS             RESTARTS   AGE
frontend-deployment-7b9984b987-qr8rr   0/1     ImagePullBackOff   0          6m48s
frontend-deployment-7b9984b987-jhjg2   0/1     ImagePullBackOff   0          6m48s
frontend-deployment-7b9984b987-t575n   0/1     ImagePullBackOff   0          6m48s
frontend-deployment-7b9984b987-dfpgl   0/1     ImagePullBackOff   0          6m48s
```

## caau:
Question:
```bash
Out of all the existing PODs, how many are ready?
```

Answer:
```bash
kubectl get pods --field-selector=status.phase=Running --no-headers | grep -c "1/1"
client:
No resources found in default namespace.
0

```

## caau7:
Quenstion:
```bash
What is the image used to create the pods in the new deployment?
``` 

Answer:
```bash
➜  kubectl describe deployment
client:
Name:                   frontend-deployment
Namespace:              default
CreationTimestamp:      Mon, 22 Apr 2024 08:24:42 +0000
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               name=busybox-pod
Replicas:               4 desired | 4 updated | 4 total | 0 available | 4 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  name=busybox-pod
  Containers:
   busybox-container:
    Image:      busybox888
    Port:       <none>
    Host Port:  <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      False   MinimumReplicasUnavailable
  Progressing    False   ProgressDeadlineExceeded
OldReplicaSets:  <none>
NewReplicaSet:   frontend-deployment-7b9984b987 (4/4 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  12m   deployment-controller  Scaled up replica set frontend-deployment-7b9984b987 to 4
```

## caau8:
Question:
```bash
Why do you think the deployment is not ready?
```
Answer:
```bash
➜  kubectl describe pods
Name:             frontend-deployment-7b9984b987-qr8rr
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.6.31.3
Start Time:       Mon, 22 Apr 2024 08:24:42 +0000
Labels:           name=busybox-pod
                  pod-template-hash=7b9984b987
Annotations:      <none>
Status:           Pending
IP:               10.42.0.10
IPs:
  IP:           10.42.0.10
Controlled By:  ReplicaSet/frontend-deployment-7b9984b987
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox888
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-cc4mj (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-cc4mj:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                 From               Message
  ----     ------     ----                ----               -------
  Normal   Scheduled  15m                 default-scheduler  Successfully assigned default/frontend-deployment-7b9984b987-qr8rr to controlplane
  Normal   Pulling    14m (x4 over 15m)   kubelet            Pulling image "busybox888"
  Warning  Failed     14m (x4 over 15m)   kubelet            Failed to pull image "busybox888": failed to pull and unpack image "docker.io/library/busybox888:latest": failed to resolve reference "docker.io/library/busybox888:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     14m (x4 over 15m)   kubelet            Error: ErrImagePull
  Warning  Failed     13m (x6 over 15m)   kubelet            Error: ImagePullBackOff
  Normal   BackOff    28s (x65 over 15m)  kubelet            Back-off pulling image "busybox888"


Name:             frontend-deployment-7b9984b987-jhjg2
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.6.31.3
Start Time:       Mon, 22 Apr 2024 08:24:42 +0000
Labels:           name=busybox-pod
                  pod-template-hash=7b9984b987
Annotations:      <none>
Status:           Pending
IP:               10.42.0.9
IPs:
  IP:           10.42.0.9
Controlled By:  ReplicaSet/frontend-deployment-7b9984b987
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox888
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-5c9v4 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-5c9v4:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                 From               Message
  ----     ------     ----                ----               -------
  Normal   Scheduled  15m                 default-scheduler  Successfully assigned default/frontend-deployment-7b9984b987-jhjg2 to controlplane
  Normal   Pulling    14m (x4 over 15m)   kubelet            Pulling image "busybox888"
  Warning  Failed     14m (x4 over 15m)   kubelet            Failed to pull image "busybox888": failed to pull and unpack image "docker.io/library/busybox888:latest": failed to resolve reference "docker.io/library/busybox888:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     14m (x4 over 15m)   kubelet            Error: ErrImagePull
  Warning  Failed     13m (x6 over 15m)   kubelet            Error: ImagePullBackOff
  Normal   BackOff    23s (x66 over 15m)  kubelet            Back-off pulling image "busybox888"


Name:             frontend-deployment-7b9984b987-dfpgl
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.6.31.3
Start Time:       Mon, 22 Apr 2024 08:24:42 +0000
Labels:           name=busybox-pod
                  pod-template-hash=7b9984b987
Annotations:      <none>
Status:           Pending
IP:               10.42.0.12
IPs:
  IP:           10.42.0.12
Controlled By:  ReplicaSet/frontend-deployment-7b9984b987
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox888
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-vr96x (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-vr96x:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                 From               Message
  ----     ------     ----                ----               -------
  Normal   Scheduled  15m                 default-scheduler  Successfully assigned default/frontend-deployment-7b9984b987-dfpgl to controlplane
  Normal   Pulling    13m (x4 over 15m)   kubelet            Pulling image "busybox888"
  Warning  Failed     13m (x4 over 15m)   kubelet            Failed to pull image "busybox888": failed to pull and unpack image "docker.io/library/busybox888:latest": failed to resolve reference "docker.io/library/busybox888:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     13m (x4 over 15m)   kubelet            Error: ErrImagePull
  Warning  Failed     13m (x6 over 15m)   kubelet            Error: ImagePullBackOff
  Normal   BackOff    20s (x66 over 15m)  kubelet            Back-off pulling image "busybox888"


Name:             frontend-deployment-7b9984b987-t575n
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/192.6.31.3
Start Time:       Mon, 22 Apr 2024 08:24:42 +0000
Labels:           name=busybox-pod
                  pod-template-hash=7b9984b987
Annotations:      <none>
Status:           Pending
IP:               10.42.0.11
IPs:
  IP:           10.42.0.11
Controlled By:  ReplicaSet/frontend-deployment-7b9984b987
Containers:
  busybox-container:
    Container ID:  
    Image:         busybox888
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-5j5kx (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-5j5kx:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                 From               Message
  ----     ------     ----                ----               -------
  Normal   Scheduled  15m                 default-scheduler  Successfully assigned default/frontend-deployment-7b9984b987-t575n to controlplane
  Normal   Pulling    14m (x4 over 15m)   kubelet            Pulling image "busybox888"
  Warning  Failed     14m (x4 over 15m)   kubelet            Failed to pull image "busybox888": failed to pull and unpack image "docker.io/library/busybox888:latest": failed to resolve reference "docker.io/library/busybox888:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: authorization failed
  Warning  Failed     14m (x4 over 15m)   kubelet            Error: ErrImagePull
  Warning  Failed     13m (x6 over 15m)   kubelet            Error: ImagePullBackOff
  Normal   BackOff    28s (x65 over 15m)  kubelet            Back-off pulling image "busybox888"

```

## caau9:
Question:
```bash
Create a new Deployment with the below attributes using your own deployment definition file.


Name: httpd-frontend;
Replicas: 3;
Image: httpd:2.4-alpine
```

Answer:
```bash
➜  sudo nano deployment-definition-httpd.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
        - name: httpd-container
          image: httpd:2.4-alpine

➜  kubectl apply -f deployment-definition-httpd.yaml
client:
deployment.apps/httpd-frontend created

➜  kubectl get deployment httpd-frontend
client
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
httpd-frontend   3/3     3            3           34s
```