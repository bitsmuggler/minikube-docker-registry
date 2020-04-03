# Setup Docker Registry on minikube

## 1. Create the docker-registry on minikube 

``kubectl create -f kube-registry.yaml``

Check the response of the installed docker registry:

```minikube ssh```

```curl localhost:5000```

## 2. Map the port 5000 to minikube registry pod

<code>
kubectl port-forward --namespace kube-system $(kubectl get po -n kube-sy
stem | grep kube-registry-v0 | \awk '{print $1;}') 5000:5000
</code>


## Resources

* [kube-registry.yaml on git](https://gist.github.com/coco98/b750b3debc6d517308596c248daf3bb1)
* [Sharing a local registry with minikube](https://hasura.io/blog/sharing-a-local-registry-for-minikube-37c7240d0615/)