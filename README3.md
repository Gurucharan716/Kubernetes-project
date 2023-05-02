Step 1: Create a namespace called reddit-clone-ns by running these commands
kubectl create namespace reddit-clone-ns

In the below image you can see we have created "reddit-clone-ns" namespace

![image](https://user-images.githubusercontent.com/120701020/235591821-427fe010-bfa3-477f-8cf3-3c068f882a5d.png)

Step 2: Make a directory called deployment_k8s in master server and change directory to it

![image](https://user-images.githubusercontent.com/120701020/235591852-155b320d-230e-49df-b4c2-f1291c19fd32.png)

Step 3: Create a deployment.yml file in that directory 

![image](https://user-images.githubusercontent.com/120701020/235591917-6f5eedd7-1105-4ba4-ba5d-90772850b4d9.png)

Step 4: In deployment.yml run these commands

apiVersion: apps/v1
kind: Deployment
metadata:
  name: reddit-clone-deployment
  namespace: reddit-clone-ns
  labels:
    app: reddit-clone
spec:
  replicas: 2
  selector:
    matchLabels:
      app: reddit-clone
  template:
    metadata:
      labels:
        app: reddit-clone
    spec:
      containers:
      - name: reddit-clone
        image: gurucharan22/reddit-clone-app:latest
        ports:
        - containerPort: 3000
        

![image](https://user-images.githubusercontent.com/120701020/235592023-695d190b-38cb-454d-b389-180511da2cae.png)

here containerPort is 3000 because our reddit clone image we have expose port number 3000 and "gurucharan22/reddit-clone-app:latest" is our docker hub image id from that we are pulling that image

Step 5: Run these commands on master node

kubectl apply -f deployment.yml

![image](https://user-images.githubusercontent.com/120701020/235592118-b9b0018f-6445-42fc-82f0-9072ecc8bc7e.png)

Step 6: Run these commands on master node to confirm that what are the pods running in reddit-clone-ns namespace. 

kubectl get pods -n=reddit-clone-ns 

![image](https://user-images.githubusercontent.com/120701020/235592186-94be2269-47d3-41e3-b8f2-a69c7e07ce1b.png)
 
 Step 7: Create a service.yml file in that directory 
 
 ![image](https://user-images.githubusercontent.com/120701020/235592224-4ae4d16f-3052-48c8-aba9-c821b5e37660.png)
 
 Step 8: In service.yml run these commands 
 
 apiVersion: v1
kind: Service
metadata:
  name: reddit-clone-service
  namespace: reddit-clone-ns
spec:
  type: NodePort
  selector:
    app: reddit-clone
  ports:
      # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
    - port: 80
      targetPort: 3000
      # Optional field
      # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
      nodePort: 30007 
      
![image](https://user-images.githubusercontent.com/120701020/235592294-b946f3a4-4110-406e-b7d9-6669ce656d2f.png)

Step 9: Run these commands on master node

kubectl apply -f service.yml 

![image](https://user-images.githubusercontent.com/120701020/235592359-10aa027a-6504-4fa8-bcad-db5f4880734c.png)
 
 Step 10: Run these commands on master node to confirm that what are the services running in reddit-clone-ns namespace. 
 
 kubectl get service -n reddit-clone-ns 
 
 ![image](https://user-images.githubusercontent.com/120701020/235592400-c8c4ac06-ea3c-429b-a490-22982072e86a.png)
 
 Step 11: Run these commands in worker node 
 
 sudo docker ps 
 
 here you can see two replicas are running 
 
 ![image](https://user-images.githubusercontent.com/120701020/235592484-7475c6bb-a690-4561-9e30-df4dd168000a.png)
 
 Step 12: In the worker node open port 30007 in the security group and copy its Public IP address and paste it to google chrome 
 
 ![image](https://user-images.githubusercontent.com/120701020/235592527-368a4ff6-f1cd-4875-b9f5-f757c4c5d798.png)
 
 Now you see we have successfully deployed our application reedit clone through Kubernetes 
 
 ![image](https://user-images.githubusercontent.com/120701020/235592574-63f3a4d8-708e-4579-8904-4615d4700a6c.png)
 
 Thank you for reading this blog and if any queries or if any corrections to be done in this blog please let me know.

contact us in Linkedin(https://www.linkedin.com/in/gurucharan-shettigar-00794326b/) ,Twitter(https://twitter.com/Gurucharan7015) or email-id gurucharanu716@gmail.com


       

