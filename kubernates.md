
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
> 
