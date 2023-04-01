# Simple Kubernetes App

### Start Vagrant
```vagrant up```

### Access the virtual box
```vagrant ssh```

### Set up Kubernetes on your minikube
```
vagrant@minikube:~$ kubectl apply -f /vagrant/services/
deployment.apps/flask-app created
pod/client-pod created
ingress.networking.k8s.io/app-ingress created
service/flask-app-service created
```

### Check available pods
```
vagrant@minikube:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
client-pod                   1/1     Running   0          8m29s
flask-app-84847f8b5d-dz9h8   1/1     Running   0          8m29s
flask-app-84847f8b5d-sw666   1/1     Running   0          8m29s
flask-app-84847f8b5d-zlstk   1/1     Running   0          8m29s
```

### Check available services
```
vagrant@minikube:~$ kubectl get svc
NAME                TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
flask-app-service   LoadBalancer   10.102.149.9   <pending>     80:32405/TCP   13s
kubernetes          ClusterIP      10.96.0.1      <none>        443/TCP        39s
```

### Port forward in the minikube box
```
vagrant@minikube:~$ kubectl port-forward flask-app-84847f8b5d-dz9h8 5000:5000
Forwarding from 127.0.0.1:5000 -> 5000
Forwarding from [::1]:5000 -> 5000
```

### SSH into minikube in another terminal
```
vagrant ssh
```
You may check if the the service is running properly by running the app locally in your vagrant box.
Follow the procedure from here [Git Repo](https://github.com/joyceiphone/app)

### Ingress exposes the service
In the minikube, run the following command to enable ingress
```
minikube addons enable ingress
kubectl apply -f /vagrant/services/ingress.yaml
```

### Add hosts
```
minikube ip
echo "192.168.49.2 joyce.com" | sudo tee -a /etc/hosts
```

### Check if the service is up

```python
In [1]: import requests

In [2]: result = requests.post("http://joyce.com/train")

In [3]: result.status_code
Out[3]: 200

In [4]: result = requests.get("http://joyce.com/get-result?sepal_length=1&sepal_width=2&petal_length=3&petal_width=4")

In [5]: result.status_code
Out[5]: 200

In [6]:result.text
Out[6]:'iris-setosa'
```

### If the service is down
```python
In [1]: import requests

In [2]: result = requests.post("http://joyce.com/train")

In [3]: result.status_code
Out[3]: 404

In [4]: result = requests.get("http://joyce.com/fallback?petal_length=1")

In [5]: result.status_code
Out[5]: 200

In [6]:result.text
Out[6]:'iris-setosa'
```