***Service***
Node port - 
First Will check whether port is in use or not by doing 
  netstat -ano | grep tcp:8000
Will display if any ports are being in use
Or else it'll through next line.


Steps-

kubectl get po -o wide
NAME          READY   STATUS    RESTARTS   AGE   IP                NODE                                              NOMINATED NODE   READINESS GATES
kubia-bl6cw   1/1     Running   0          16s   192.168.166.250   ip-172-31-25-53.ap-southeast-1.compute.internal   <none>           <none>

curl  192.168.166.250:8000
curl: (7) Failed to connect to 192.168.166.250 port 8000 after 0 ms: Connection refused

As we can check the particular pod is refusing the port we can use the default port which is 8080
curl  192.168.166.250:8080
You've hit kubia-bl6cw
2>then will verify by accessing
http://51.121.29.165:30101

