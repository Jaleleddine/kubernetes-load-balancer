# kubernetes-load-balancer

  ## 1) create a namespace to isolate applications
    # $ kubectl apply -f namespace.yml 
    # -> namespace/production created

  ## 2) get all namespaces 
    # $ kubectl get namespaces
       # NAME              STATUS   AGE
       # default           Active   69d
       # ingress-nginx     Active   69d
       # kube-node-lease   Active   69d
       # kube-public       Active   69d
       # kube-system       Active   69d
       # production        Active   16s
       
  ## 3) create a first pod
    # $ kubectl apply -f pod-red.yml -n production
    # -> pod/simple-webapp-color-red created
    
  ## 4) get pods in the production namespace
   # $ kubectl get pods -n production 
       # NAME                      READY   STATUS    RESTARTS   AGE
       # simple-webapp-color-red   1/1     Running   0          2m22s
       
  ## 5) $ kubectl apply -f service-nodeport-web.yml -n production
     # -> service/service-nodeport-web created
     
  ## 6) $ kubectl -n production get svc
      # NAME                   TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
      # service-nodeport-web   NodePort   10.106.188.7   <none>        8080:30008/TCP   31s
 
  ## 7) describe the service with two pods
    # $ kubectl -n production describe svc service-nodeport-web
      # Name:                     service-nodeport-web
      # Namespace:                production
      # Labels:                   <none>
      # Annotations:              <none>
      # Selector:                 app=web
      # Type:                     NodePort
      # IP Families:              <none>
      # IP:                       10.106.188.7
      # IPs:                      10.106.188.7
      # Port:                     <unset>  8080/TCP
      # TargetPort:               8080/TCP
      # NodePort:                 <unset>  30008/TCP
      # Endpoints:                172.18.0.17:8080
      # Session Affinity:         None
      # External Traffic Policy:  Cluster
      # Events:                   <none>
  ## 8) create a second pod 
      # $ kubectl apply -f pod-blue.yml -n production
      # $ kubectl -n production describe svc service-nodeport-web
          # Name:                     service-nodeport-web
          # Namespace:                production
          # Labels:                   <none>
          # Annotations:              <none>
          # Selector:                 app=web
          # Type:                     NodePort
          # IP Families:              <none>
          # IP:                       10.106.188.7
          # IPs:                      10.106.188.7
          # Port:                     <unset>  8080/TCP
          # TargetPort:               8080/TCP
          # NodePort:                 <unset>  30008/TCP
          # Endpoints:                172.18.0.17:8080,172.18.0.18:8080
          # Session Affinity:         None
          # External Traffic Policy:  Cluster
          # Events:                   <none>
