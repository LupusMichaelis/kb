
# Install Minikube



kubectl

kubectl create -f image-name-pod.yml
kubectl run hw --image image-name

kubectl get pods
minikube dashboard

```yaml
# image-name-pod.yml
apiVerstion: v1
kind: Pod
metadata:
   - name: image-name
     image: libatrio/hello-world
     ports:
       - name: nodejs-port
         containerPort: 3000
```
