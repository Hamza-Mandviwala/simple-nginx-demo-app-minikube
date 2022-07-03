# Simple Nginx-demo application pod on Minikube cluster

This GitHub project is intended to help you deploy a simple nginxdemo application on a minikube cluster.

The minikube cluster was deployed using the steps mentioned here - https://minikube.sigs.k8s.io/docs/start/

If you do not have the kubectl cli installed, you can install it from here - https://kubernetes.io/docs/tasks/tools/#kubectl

Please note that minikube makes use of level 2 hypervisor and runs the minikube cluster as a Virtual machine. It would be advisable to have tools like VirtualBox, or any other hypervisor readily installed.

Once the minikube cluster is started, try running basic commands like `kubectl get pods` to see if it returns valid results like ‘No resources found in default namespace.'

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
      
To run this yaml file on your minikube cluster (or any other kubernetes cluster):

1. Clone this repository:
    
       git clone https://github.com/Hamza-Mandviwala/simple-nginx-demo-app-minikube.git

2. Run the following command. This should create the `nginxdemo` pod and the `nginxdemo-svc` service.

       kubectl apply -f nginxdemo-pod-svc.yaml
       
3. Run a `kubectl get svc` command to get the port number on which the nginxdemo-svc service will be serving the UI:

    Output:
    
    <img width="950" alt="Screenshot 2022-07-03 at 12 30 15 PM" src="https://user-images.githubusercontent.com/53118271/177031498-f2caa8a9-ee5c-47c0-b4d3-2c8e6baf31b2.png">
    
    As we can see from the above screenshot, port number 32165 on the machine will be used to serve the app requests.
    
4. We can now try to access the nginxdemo UI through the browser using the IP address of the minikube VM and port 32165. Alternatively, we can also run the command `minikube service nginxdemo-svc` (where 'nginxdemo-svc' is the service name) which will automatically open up the browser tab with the nginxdemo UI:

    <img width="1792" alt="Screenshot 2022-07-03 at 12 35 36 PM" src="https://user-images.githubusercontent.com/53118271/177031634-c6c9ed4c-214c-439f-8778-71cd3a098aeb.png">

=======================================================================================================

**Congratulations! We just deployed a simple nginxdemo application on a locally hosted minikube cluster.**

=======================================================================================================


## Must try out:
1. Detailed guide for [RedHat OpenShift 4.10 installation on GCP using UPI (User Provisioned Infrastructure method)](https://github.com/Hamza-Mandviwala/OCP4.10.3-install-GCP-UPI)

    



