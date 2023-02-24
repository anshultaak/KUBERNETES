# HEALTHCHECK

### LIVENESS PROBES
liveness inform us, Your kubernets container need to restart

### Readiness probe
you pod is ready to accept traffic

### startup probe
when conatiner statup 

````

livenessProbe:
      httpGet:
        path: /healthz                              # its endpoint of application check ( search internet by tis path you get health status0
        port: 8080                                   # port on which running 
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 13                                       # first time when livenss will test 
      periodSeconds: 10                                           # regular interval check your application heath
      
   READINESS PROBES
   its check port health
   
   readinessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 3
      periodSeconds: 3
      
    STARTUP PROBES
    its  check your application succesfuly or not .if it start succesfully  then yo shuld readniess and liveness probe
    
startupProbe:
  httpGet:
    path: /healthz
    port: 8080
  failureThreshold: 30                                      # 30 * 10 = 300, its maximum time is 5 min to start application 
  periodSeconds: 10
 
 
 yaml file
 
 apiVersion: v1
kind: Pod
metadata:
  name: goproxy
  labels:
    app: goproxy
spec:
  containers:
  - name: goproxy
    image: k8s.gcr.io/goproxy:0.1
    ports:
    - containerPort: 8080
    readinessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
    startupProbe:
      httpGet:
        path: /healthz
        port: 8080
      failureThreshold: 30                                      # 30 * 10 = 300, its maximum time is 5 min to start application 
      periodSeconds: 10
    
 ```
