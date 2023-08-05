
#### Install Minikube
sudo apt-get install curl  
sudo apt-get install apt-transport-https  
sudo apt install virtualbox virtualbox-ext-pack  
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64  
sudo install minikube-linux-amd64 /usr/local/bin/minikube  
sudo chmod 755 /usr/local/bin/minikube  
minikube start  
minikube stop  
minikube delete  
minikube addons list  
minikube dashboard  
minikube dashboard --url  

#### Install kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/OS_DISTRIBUTION/amd64/kubectl  
chmod +x ./kubectl  
sudo mv ./kubectl /usr/local/bin/kubectl  
kubectl version -o json  

#### Install Helm Charts
curl https://raw.githubusercontent.com/kubernetes/helm/HEAD/scripts/get-helm-3 > get_helm.sh  
chmod 700 get_helm.sh  
./get_helm.sh  

OR

curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null  
sudo apt-get install apt-transport-https --yes  
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list  
sudo apt-get update  
sudo apt-get install helm  



