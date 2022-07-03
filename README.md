# simple-nginx-demo-app-minikube

This GitHub project is intended to help you deploy a simple nginxdemo application on a minikube cluster.

The minikube cluster was deployed using the steps mentioned here - https://minikube.sigs.k8s.io/docs/start/

If you do not have the kubectl cli installed, you can install it from here - https://kubernetes.io/docs/tasks/tools/#kubectl

Please note that minikube makes use of level 2 hypervisor and runs the minikube cluster as a Virtual machine. It would be advisable to have tools like VirtualBox, or any other hypervisor readily installed.

Once the minikube cluster is started, try running basic commands like kubectl get pods to see if it returns valid results like ‘No resources found in default namespace.'

Below is a sample manifest file that creates a simple nginxdemo pod using the image `nginxdemos/hello` and a service of type NodePort that helps expose the nginxdemo pod locally on the machine.

    apiVersion: v1
    kind: Pod
    metadata:
      labels:
        run: nginxdemo
      name: nginxdemo
    spec:
      containers:
      - image: nginxdemos/hello
        name: nginxdemo
    ---
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        run: nginxdemo
      name: nginxdemo-service
    spec:
      ports:
      - port: 80
        protocol: TCP
        targetPort: 80
      selector:
        run: nginxdemo
      type: NodePort
      
To run this yaml file on your minkube cluster (or any other kubernetes cluster):
1. Clone this repository:
    git clone
