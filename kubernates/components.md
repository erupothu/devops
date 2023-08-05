 
ETCD database  

> kubectl describe pod/etcd-node2 --namespace=kybe-system    
> kubectl exec -it pod/etcd-node2 --namespace=kybe-system -- /bin/sh  
> kubectl get all --all-namespaces  
> cd /etc/kubernetes/manifests  
> cat etcd.yaml  


API Server:  
1. cd /etc/kubernetes/manifests  
2. cat kube-apiserver.yaml   
3. /api/v1/namespaces/<namespace-name>/<resource-type-name>/<resource-name>  
> kubectl proxy   
> curl localhost:8001/api  
> curl localhost:8001/api/v1/nodes  
> cur localhost:8001/api/v1/[namespace]/pods  
> curl localhost:8001/api/v1/namespaces/kube-system/pods/kube-controller-manager-node2/  

Kube Controller  
https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kube-apiserver  
https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kube-controller-manager  
https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kube-scheduler  
https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl  

1. kube-controller-manager.yaml  
2. cat kube-controller-manager.yaml  
3. kubectl describe pod/kube-controller-manager-node2 --namespace=kube-system   

Schedular  
cd /etc/kubernetes/manifests  
cat kube-scheduler.yaml   
kubectl get all --all-namespaces  
kubectl exec -it pod/kube-scheduler-node2 --namespace=kube-system -- /bin/sh  
kubectl describe pod/kube-scheduler-node2 --namespace=kube-system  
1. resource request  
2. limits
3. selectors
4. Affinity
5. tains
6. Tollerance
7. Daemonset
8. Events
9. Manual scheduling
10. Custom Scheduling
11. Multiple scheduling

Kubelet  
1. installed every node  
2. send to kube apiserver   
3. sends resources utilized, available, requests, other reports to kube api server  
> cat /etc/kubernetes/kubelet.conf  
> journalctl -l -u kubelet  

Kubeproxy  
1. comunication between pods and external world and services  
2. dns server  
3. provide networking and maintains the pods ip  

> kubectl exec -it pod/kube-proxy-fcz7s  --namespace=kube-system -- /bin/sh  
> kubectl describe daemonset.apps/kube-proxy --namespace=kube-system  
> kubectl describe pod/kube-proxy-fcz7s --namespace=kube-system  
> kubectl logs -f pod/kube-proxy-7xklb --namespace=kube-system  

Core DNS:
1. service discovery  

> kubectl get all --all-namespaces  
pod/coredns-66bff467f8-g58kr  
pod/coredns-66bff467f8-lzw6v  
> kubectl describe pod/coredns-66bff467f8-g58kr --namespace=kube-system  
> kubectl describe pod/coredns-66bff467f8-lzw6v --namespace=kube-system  
> kubectl logs -f pod/coredns-66bff467f8-g58kr --namespace=kube-system  
> kubectl logs -f pod/coredns-66bff467f8-lzw6v --namespace=kube-system  
> kubectl get svc --namespace=kube-system  
> kubectl get ep kube-dns --namespace=kube-system  
> kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml  
> kubectl exec -ti dnsutils -- nslookup kubernetes.default  
> kubectl exec -ti dnsutils -- cat /etc/resolv.conf  
#end point for kube-system  
> kubectl get ep kube-dns --namespace=kube-system  
> kubectl get ep kube-dns --namespace=kube-system -o json  
> kubectl get logs -ns kube-system pod/calico-node-mppr8  
