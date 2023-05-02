Prerequisite

Make two instance naming Kubernetes-master and Kubernetes-worker with instance type both set to t2.medium as shown in the below image

![image](https://user-images.githubusercontent.com/120701020/235591229-2eec3662-55fb-45b4-8aee-2f716af5f385.png)

![image](https://user-images.githubusercontent.com/120701020/235591245-d7228171-1865-44c1-8505-34cb8d68c6b0.png)

Make a Kubernetes cluster in this if you don't know how to do it please check this blog https://gurucharan.hashnode.dev/kubernetes-architecture-and-cluster.
To confirm that your are connected run these commands in the master server

kebectl get nodes 

You should see like this in the image shown below

![image](https://user-images.githubusercontent.com/120701020/235591545-5bac9356-bfa7-42a8-9d57-dc578d6ba4c1.png)

