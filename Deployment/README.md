***DEPLOYMENT***

**Steps to change replica** -

vi kubia-deployment-and-service-v1.yaml --> set replicas: 1

kubectl apply -f kubia-deployment-and-service-v1.yaml

kubectl get po
NAME                     READY   STATUS    RESTARTS   AGE
kubia-9d62ba022c48-nckhz   1/1     Running   0          10s


kubectl get deploy
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
kubia   1/1     1            1           40s


kubectl describe deploy kubia
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
 nodejs:
    Image:        luksa/kubia:v1
	
	
kubectl patch deployment kubia -p '{"spec": {"minReadySeconds": 10}}'
MinReadySeconds:        10


kubectl set image deployment kubia nodejs=luksa/kubia:v999
deployment.apps/kubia image updated


kubectl describe deploy kubia

Containers:
   nodejs:
    Image:        luksa/kubia:v999
	
	
	
kubectl get po
NAME                     READY   STATUS              RESTARTS   AGE
kubia-9d62ba022c48-nckhz   1/1     Running             0          7m50s
kubia-28fcc32b681a-dvgsc   0/1     ContainerCreating   0          2s
kubia-52896192e081-fwrbw   0/1     Terminating         0          2m29s

kubectl get po
NAME                     READY   STATUS             RESTARTS   AGE
kubia-9d62ba022c48-nckhz   1/1     Running            0          8m20s
kubia-28fcc32b681a-dvgsc   0/1     ImagePullBackOff   0          32s
