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

### Follow the procedures from the link below
[APP Repo](https://github.com/joyceiphone/app)