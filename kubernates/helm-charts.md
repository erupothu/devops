
> helm create mychart
> helm install mychart --dry-run --debug ./mychart --set service.internalPort=8080
> helm install example ./mychart --set service.type=NodePort
