# Setting-Up-Minikube-Kubernetes-Cluster-

## In This Project I Created following things:


1. [Installation of Minikube & Kubectl on Window](#install-minikube)
2. [Create Single-Node Cluster and use Adhoc cmds](#single-node-cluster)
3. [Create Multi-Node Cluster](#multi-node-cluster)
4. [Kubernetes Resources YAML file](#k8s-resources)
5. [Kubernetes Secret](#k8s-secret)
6. [Check and Explain K8s resources](#explain-cmd)
7. [Minikube Dashboard](#dashboard)


**There are many ways to create K8s cluster:**
1. EKS
2. AKS
3. GKE
4. Kubeadm
5. Minikube

Minikube required for Multi-Node Cluster:
Note: The Cluster is creating is automatic by Minikube we just put our requirement but this is not give fully customize option like Kubeadm.

## <a id="install-minikube"></a>Installation of Minikube & Kubectl on Window:
1. *Minikube install on window:*
    - Search on Browser "kubernetes minikube install" and then Click on ->  'latest release' 
    [Minikube-Download-link](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+downloa)
    ![Download-minikube](https://github.com/user-attachments/assets/676f0852-8c27-4780-aba7-5069338b9c69)
    - After Download Extract exe file then, add **"Path in System Environment variable"**.
    - Note: Install Oracle VirtualBox on Window [download-virtualBox-Link](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html)
  2.  *Now Install Client side/ User side command that is **"kubectl"** for managing K8s Cluster:*
    - Search on Browser:-> "kubectl install" -> then click on "Install and Set Up kubectl on Windows"
    [kubectl-Download-cmd-Link](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-on-windows-via-direct-download-or-curl)

- Note: If CLI show error then put both minikube & kubectl file in same folder of window. 

***

# <a id="single-node-cluster"></a>Single-Node Cluster command:
Here i create Single-node cluster that is means on single node Master & Worker Node work done.

To Create Single-Node Culster using minikube command is:

    minikube start
<img width="1449" height="248" alt="Screenshot 2026-01-05 222832" src="https://github.com/user-attachments/assets/4b80a0ba-c528-4bd1-b317-758b2ae8fe4d" />

Check status of Minikube:


   minikube status
<img width="1344" height="251" alt="Screenshot 2026-01-05 222317" src="https://github.com/user-attachments/assets/812c6fc8-8b70-4972-b339-c1443e8330b1" />

![Uploading Screenshot 2026-01-05 222959.png…]()



### CLi Adhoc command:
**Create Deployment and svc using CLI adhoc commands:**
-Install Kubectl 
     curl.exe -LO https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl.exe

- Now create deployment using image:

      kubectl create deployment myweb --image=pratikshinde55/apache-webserver:v1

  ![Deployment](https://github.com/user-attachments/assets/7ed66fae-9733-4ef7-abe2-c80e0879ddaa)

- Use describe:

      kubectl describe deployment myweb

- Print list of Deployment & Pod:

      kubectl get pods
   kubectl get deployment

   ![get-cmd](https://github.com/user-attachments/assets/88dc8c0c-917d-4c97-8126-d43c31459b29)

- Get Full lenght information:

      kubectl get pods myweb-b77b85fb9-bghs9  -o wide
      kubectl get deployment myweb -o wide

   **Load Balancer: [expose] for CLI way**
- Create service or expose our deployment app to outside world:

      kubectl expose deployment myweb --type=NodePort --port=80

- Print list of LB:

      kubectl get svc 
      kubectl get service

- **Note:** `--type=NodePort` is define give Public_IP & `--port=80` => This is port number of Container or If any app running inside pod/Container then give that port no for example Python-flask app port 5000.
      
      kubectl describe svc myweb

  - Here, We see all three pods are attached to the Load Balancer, If we Scale-out or Scale-in that will automatic upadte to Load Balancer Service
  ![See all details](https://github.com/user-attachments/assets/59709750-cdd0-4f5d-990e-3b8d615ba2cb)

### Manual Scaling using Adhoc command: [scale]
- Command for manual scale:

      kubectl scale deployment myweb --replicas=3   
    
  ![scale-cmd](https://github.com/user-attachments/assets/3ecc1a0f-c6e5-41db-89f6-d8d4491bec91)

- delete command for delete all k8s resources:

      kubectl delete all -all

  ### Delete minikube single-node cluster:

     minikube delete
     
- **Note:** After deleted cluster then Go to windows file manager then go to C:\ then -> Users -> ownuser -> `.minikube` then delete this minikube file

***

# <a id="multi-node-cluster"></a>Multi-Node-Cluster:
Now here create multi-node cluster using minikube.

Now here create multi-node cluster using minikube.

**Interact with Kubernetes:**
1. CLI (Adhoc commands)
2. Code (YAML - Yet Another Markup Language , Declarative Language)
3. API

**Start Minikube Multi-node Cluster Command:**

     minikube start -n 2 -p pscluster2

![Startind-status](https://github.com/user-attachments/assets/ce59b492-f1a5-4f7e-b366-57d187afa23e)

![list-of nodes](https://github.com/user-attachments/assets/05fec64d-712a-4bd0-9da9-ef20de357504)


# <a id="k8s-resources"></a>Resource Types in K8s:

**Basic Format of K8s yaml manifest file:** (Use .yml extention for code file)

    apiVersion:
    kind:
    metadata:
       name:
       labels:
    spec:
       containers:
         - name: 
           image: 
## 1. Pod resource type (Only Launch Pod without any Deployment or else):

- Create file:
  
       notepad pod.yml

  ![pod-file](https://github.com/user-attachments/assets/31bc7b76-cb74-45b8-acfd-80ce94e5f257)

- Describe command:

       kubectl describe pods myonlypod
  
  ![Event](https://github.com/user-attachments/assets/705b1c75-5aa9-4dd7-8c51-dfabba52018b)

  
## 2. Replication Controller resource type: [rc]
