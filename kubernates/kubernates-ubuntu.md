

#### Install kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/OS_DISTRIBUTION/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

#### Install Helm Charts
curl https://raw.githubusercontent.com/kubernetes/helm/HEAD/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh

