
#### windows  minikube setup
download and install minikube for windows  
download and set path for kubectl place both kubectl.exe and minikube.exe in same location  
download and install virtual box for windows  
download and install putty for windows
download and install aws-cli for windows 

set PATH="path to kubectl path"  
> kubectl version  
> minikube start --driver=virtualbox  
> kubectl get pods  
> kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10  
> kubectl get pods  
> minkibe dashborad  
> open the url in browser for Orchestartion dashboard
> minikube stop

#### AWS kubernates installations  
download and install aws-cli for windows  
download and install putty and puttygen(for converting pem key to .ppk file) for windows to communicate with aws ec2  
login to AWS console and create IAM user with programtic access with access key and EC2 instance with pem key and linux OS  

> ssh -i pem_key.pem ubuntu@ip_address or use putty with ppk file  
> sudo apt install docker-ce  
> sudo service docker start  
> wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64  
> sudo cp minikube-linux-amd64 /usr/local/bin/minikube  
> sudo chmod 755 /usr/local/bin/minikube  
> minikube version  
> curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl  
> chmod +x ./kubectl  
> sudo mv ./kubectl /usr/local/bin/kubectl  
> kubectl version -o json  
> minikube start --driver=docker  
> kubectl cluster-info  
> minikube ssh  
> minikube dashboard  
> minikube dashboard --url
> kubectl proxy --address='0.0.0.0' --disable-filter=true (to access remotely)

#### yaml file

```pod.yaml
apiVersion: v1
kind: Pod / Service / Deployment / ReplicationSet
metadata:
  name: web
  labels:
    app:web
spec:
  containers:
    - name: frontend
      image: nginx
      env:
      - name: SPECIAL_LEEVEL_KEY
        valueFrom:
          configMapKeyRef:
            name: special_config
            key: SPECIAL_LEVEL
     - name: SECRET_USERNAME
       valueFrom:
         secretKeyRef:
           name: mysecret
           key: USERNAME
      ports:
        - containerPort: 80
    - name: proxy
      image: myproxy:v1
      ports:
        - containerPort: 8080
      volumeMounts:
      - mountPath: "/usr/share/nginx/html"
        name: task-pv-storage
  volumes:
  - name: task-pv-storage
    persistentVolumeClaim:
      claimName: task-pv-claim
```

```replicaset.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replica-test
  labels:
    app: web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: replia-web
        image: nginx
```

```service.yml
apiVersion: v1
kind: Service
metadata:
  name: redis-master
  labels:
    app: redis
    tier: backend
    role: master
spec:
  ports:
    - port: 6379
      nodePort: 30200
      protocol: TCP
      targetPort: 6379
  selector:
    app: redis
    tier: backend
    role: master
  type: NodePort
```

```deployemnt.yml
apiVersion: v1
kind: Deployment
metadata:
  name: frontend
  labels:
    app:web
spec:
  selector:
    matchLabels:
      app: guesbook
      tier: frontend
  replicas: 3
  template:
    metadata:
      labels:
        app: guestbook
        tier: frontend
    spec:
      containers:
        - name: frontend
          image: nginx
          ports:
          - containerPort: 80
          env:
          - name: GET_HOST_FROM
            value: dns
          resources:
            requests:
              cpu: 100m
              memory: 100mi
```

```persistantvolume.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: volume1
  labels:
    app: volume
    tier: storage
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
  - ReadWriteOnce
  hostPath:
    path: /mnt/data
```

```persistantvolumeclaim.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

```configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  player_initial_lives: "3"
  ui_properties_file_name: "myuser-interface.properties"
  game.properties: |
    enemy.types=firstline, zoomzoom
  user-interface.properties: |
    color.good=green
    color.bad=red
    allow.textmode=true
```

```secret.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  username: adkajerowri
  password: asdfwerwerfserttr
```

#### kubectl commands  
> kubectl run nginxrun --image=nginx  
> kubctl get pods   
> kubectl describe pods nginxrun  
> kubectl delete pod/nginxrun  
>
> kubectl apply -f pod.yaml --validate=false  
> kubectl describe pods new-pod  
> kubectl port-forward --address 0.0.0.0 new-pod 80:80  
> curl http://localhost  
> kubectl exec -it new-pod /bin/bash  
> kubctl cp new-pod:copytest/test.txt /root/harish/docs.txt  
>
> kubectl appy -f replicaset.yaml  
> kubectl get rs  
> kubectl delete pod/rs-id (autoscalling works)  
>
> kubectl apply -f deployment.yaml  
> kubectl appy -f service.yaml  
> kubectl get svc  
> kubectl get pods o wide  
> kubectl get pods --selector='app' --show-labels  
> kubectl get pods --selector='app=redis' --show-labels  
> kubectl get pods --selector='role in (master, slave)' --show-labels  
>
> kubectl exec dirtest-pod df  
> kubectl exec -it dirtest-pod -- /bin/bash  
>
> kubectl apply -f persistent-volume.yaml  
> kubectl get pv  
> kubectl apply -f persistnat-volume-claim.yaml  
> kubectl get pvc  
> kubectl delete pod task-pv-pod  
> kubectl delete pvc task-pv-claim  
> kubectl delete pv task-pv-volume  
>
> kubectl apply -f myconfigmap.yaml  
> kubectl get configmaps  
> kubectl describe configmaps my-configmap -o yaml  
>
> kubectl create secret generic mysecret --from-fle=./username.txt --from-file=./password.txt  
> kubectl create secret generic mysecret --from-literal='usermame' --from-literal='password'  
> kubectl get secrets  
> 

#### 

