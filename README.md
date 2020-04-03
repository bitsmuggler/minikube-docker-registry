# Setup Docker registry on minikube

### 1. Modify your /etc/hosts entry for reaching your local registry

``127.0.0.1       localhost registry.me``


### 2. Create the docker-registry on minikube 

``kubectl create -f kube-registry.yaml``

Check the response of the installed docker registry:

```minikube ssh```

```curl localhost:5000```

### 3. Map the port 5000 to minikube registry pod

<code>
kubectl port-forward --namespace kube-system $(kubectl get po -n kube-sy
stem | grep kube-registry-v0 | \awk '{print $1;}') 5000:5000
</code>

### 4. Build, tag and push your docker image to the local registry

1. Build:  ```docker build -t techtopics/notesapp .```   
1. Tag: ```docker tag techtopics/notesapp:latest registry.me:5000/notesapp:0.0.1```
1. Push: ```docker push registry.me/notesapp:0.0.1```

## Resources

* [kube-registry.yaml on git](https://gist.github.com/coco98/b750b3debc6d517308596c248daf3bb1)
* [Sharing a local registry with minikube](https://hasura.io/blog/sharing-a-local-registry-for-minikube-37c7240d0615/)