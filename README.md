

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
<img width="984" height="283" alt="Screenshot 2026-01-05 222959" src="https://github.com/user-attachments/assets/bdca2ea1-7856-4bee-960a-99779de60e39" />


### CLi Adhoc command:
**Create Deployment and svc using CLI adhoc commands:**
-Install Kubectl 
     curl.exe -LO https://dl.k8s.io/release/v1.35.0/bin/windows/amd64/kubectl.exe
     
<img width="1410" height="127" alt="Screenshot 2026-01-05 223051" src="https://github.com/user-attachments/assets/5668c05f-5511-4b56-977b-d072d3d50a46" />


         Kubectl run mywe --image=httpd

<img width="855" height="149" alt="Screenshot 2026-01-05 223158" src="https://github.com/user-attachments/assets/fcf7f47e-9d18-41fc-b71d-98cadff8954b" />


- Now create deployment using image:
 
        kubectl create deployment mywe1 --image=nginx:latest
<img width="944" height="181" alt="Screenshot 2026-01-05 223255" src="https://github.com/user-attachments/assets/a5debe7d-46d4-4ad5-b2ce-285072c056ea" />

<img width="707" height="212" alt="Screenshot 2026-01-05 223128" src="https://github.com/user-attachments/assets/7e5b5893-f52f-44a9-ad04-cc804d3fad38" />


- Use describe:

         kubectl describe deployment myweb

- Print list of Deployment & Pod:

      kubectl get pods
      kubectl get deployment
  

<img width="1053" height="495" alt="Screenshot 2026-01-05 223310" src="https://github.com/user-attachments/assets/3ad68483-bf2a-4859-b91d-a503645c152f" />


- Get Full lenght information:

      kubectl get pods mywe1-b77b85fb9-bghs9  -o wide
      kubectl get deployment mywe1 -o wide

   **Load Balancer: [expose] for CLI way**
- Create service or expose our deployment app to outside world:
 
      kubectl expose deployment mywe1 --type=ClusterIP --name=mywe-svc --port=80 --target-port
  
  <img width="1338" height="609" alt="Screenshot 2026-01-05 223512" src="https://github.com/user-attachments/assets/5ed83d67-6f74-4d85-bdeb-2e2a993e27fa" />

- Print list of LB:

      kubectl get svc 
      kubectl get service
  
<img width="835" height="90" alt="Screenshot 2026-01-05 223454" src="https://github.com/user-attachments/assets/db32fb30-7acb-4e7a-92db-35207b392c7a" />

- **Note:** `--type=NodePort/ClusterIP` is define give Public_IP & `--port=80` => This is port number of Container or If any app running inside pod/Container then give that port no for example Python-flask app port 5000.
      
      kubectl describe svc myweb

  - Here, We see all pods are attached to the Load Balancer, If we Scale-out or Scale-in that will automatic upadte to Load Balancer Service
  - 

### Manual Scaling using Adhoc command: [scale]
- Command for manual scale:

      kubectl scale deployment mywe1 --replicas=5  
    
 <img width="1010" height="227" alt="Screenshot 2026-01-05 223359" src="https://github.com/user-attachments/assets/b213a52e-f334-4873-bafc-3789944a926d" />

      kubectl scale deployment mywe1 --replicas=5  

<img width="854" height="147" alt="Screenshot 2026-01-05 223426" src="https://github.com/user-attachments/assets/a13e0102-0b75-4a32-98e7-cfc1b87eaeac" />

      
- delete command for delete all k8s resources:

      kubectl.exe delete pods -all
<img width="856" height="124" alt="Screenshot 2026-01-05 223643" src="https://github.com/user-attachments/assets/e54c6cd5-20b2-41b0-98eb-b52fe298132d" />

  ### Delete minikube single-node cluster:

     minikube delete
     
- **Note:** After deleted cluster then Go to windows file manager then go to C:\ then -> Users -> ownuser -> `.minikube` then delete this minikube file

***

# <a id="multi-node-cluster"></a>Multi-Node-Cluster:
Now here create multi-node cluster using minikube.


**Interact with Kubernetes:**
1. CLI (Adhoc commands)
2. Code (YAML - Yet Another Markup Language , Declarative Language)
3. API

**Start Minikube Multi-node Cluster Command:**

     minikube start -n 2 -p pscluster2
<img width="1399" height="121" alt="Screenshot 2026-01-05 223729" src="https://github.com/user-attachments/assets/00933fe4-dbca-47bd-9e8b-54d8f2c0cd48" />

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


    apiVersion: v1
kind: Pod
metadata:
   name: mypod
   labels:
   
spec:
   containers: 
     - name: mycontainer
       image: httpd

<img width="707" height="438" alt="Screenshot 2026-01-06 225844" src="https://github.com/user-attachments/assets/9c64b06e-3b75-45a4-926e-ca37ea842cef" />

## 1. Pod resource type (Only Launch Pod without any Deployment or else):

- Create file:
  
        vim first.yml
  
<img width="867" height="328" alt="Screenshot 2026-01-06 225834" src="https://github.com/user-attachments/assets/3fe59921-74b8-497a-b6cf-8d093869cbf7" />

-Check created pod:
      kubectl create -f first.yml
-Selectors For Specific details to search in Pod:
<img width="1140" height="782" alt="Screenshot 2026-01-06 225823" src="https://github.com/user-attachments/assets/ccec3c80-ac78-416b-8e07-2405afe9da6e" />

 -To check specific pod with all details :
 <img width="867" height="328" alt="Screenshot 2026-01-06 225834" src="https://github.com/user-attachments/assets/35d5080c-2eef-4f37-89d2-ffffce36d16e" />

## 2. Replication Controller resource type: [rc]
