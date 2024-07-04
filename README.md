# kubernetes-training
Kubernetes Training Material

Slide: https://docs.google.com/presentation/d/1-dmZFjMTp3SOQxQZr7hnMs91K8SRQWJRUTACKRFDgq4/edit?usp=sharing

Activities to try:
* **List Nodes & Other K8s Resources**
    * *kubectl get nodes*
    > This will list nodes
    * *kubectl get po*
    > This will list pods
    * *kubectl get svc*
    > This will list services
    * *kubectl get deploy*
    > This will list deployments

* **Create a Deployment**
    * *kubectl create deployment nginx-deployment --image=nginx*
    > This will create a deployment named *nginx-deployment* using *nginx* docker image
    * *kubectl get rs*
    > This will list replica sets
    * *kubectl create deployment nginx-deployment1 --image=nginx --replicas=2*
    > This will create a deployment named *nginx-deployment* with 2 replica pods

* **Edit a Deployment**
    * *kubectl edit deploy nginx-deployment* 
    > Edit the nginx image name from *nginx* to *nginx:1.16*
    * *kubectl get deploy,po,rs* 
    > This will list deployment, pods and replicasets

* **Describing a Pod**  
    * *kubectl describe po [pod name]* 
    > This will provide the details of the given pod

* **Debugging a Pod**
    * *kubectl create deploy mongo-dep --image=mongo*
    > This will create a mongo db deployment
    * *kubectl get po*
    * *kubectl logs [pod name]*
    > This will provide the logs for the given pod

* **Interacting with Pod**
    * *kubectl exec -it [pod name] -- /bin/bash*
    > This will get you inside the shell of the pod. Now, you can run any command here and interact with the pod

* **Delete Deployment & Pod**
    * *kubectl delete deploy [deployment name]*
    * *kubectl delete po [pod name]*

* **Restart Deployment**
    * *kubectl rollout restart deploy [deployment name]*

* **Creating a Namespace**
    * *kubectl create ns demo*
    > This will create a namespace called *demo*
    * *kubectl get ns*
    > This will list the available namespaces

* **Creating resources in a Namespace**
    * *kubectl create deploy nginx-depl --image=nginx -n demo*
    > This will create *nginx* deployment in *demo* namespace
    * *kubectl get deploy -n demo*
    > This will list deployments in *demo* namespace

* **Checking K8s components which are namespaced**
    * *kubectl api-resources --namespaced=false*
    > This will list K8s components which are not namespaced
    * *kubectl api-resources --namespaced=true*
    > This will list K8s components which are namespaced

* **Creating & Deleting Resources using Configuration file**
    * *kubectl apply -f nginx-deployment.yaml -n demo*
    > This will create deployment in *demo* namespace with the provided deployment yaml file
    * *kubectl apply -f nginx-service.yaml -n demo*
    > This will create service in *demo* namespace with the provided service yaml file
    * *kubectl get po,svc -n demo*
    > This will list pods and services in *demo* namespace
    * *kubectl describe svc nginx-service -n demo*
    > This will provide the details for *nginx-service* in *demo* namespace
    * *kubectl get pod -o wide -n demo*
    > This will list the pods in *demo* namespace with more details. Compare the IP shown in the pod with the one in service, and see if they match
    * *kubectl get deploy nginx-deployment -o yaml -n demo*
    > This will show the yaml file for the *nginx-deployment*. Check the auto-generated *status* part 
    * *kubectl delete -f nginx-deployment.yaml -n demo*
    > This will delete deployment in *demo* namespace which was created with the provided deployment yaml file
    * *kubectl delete -f nginx-service.yaml -n demo*
    > This will delete service in *demo* namespace which was created with the provided service yaml file

* **Deploying Your Own Application**
    * *kubectl apply -f simple-flask-app/deployment.yaml -n demo*
    > This will create deployment in *demo* namespace with the provided deployment yaml file
    * *kubectl apply -f simple-flask-app/service.yaml -n demo*
    > This will create service in *demo* namespace with the provided service yaml file
    * *kubectl apply -f simple-flask-app/ingress.yaml -n demo*
    > This will create ingress in *demo* namespace with the provided ingress yaml file
    * *kubectl -n demo get po,svc,ing -o wide*
    > This will list pods, services and ingresses in *demo* namespace with more details
    * *kubectl port-forward -n demo service/simple-flask-app-service 8000:80*
    > This will do the port-forwarding of the service, so that it can be accessed through *localhost*

    > Go to *http://localhost:8000* in your browser, and see the *simple-flask-app* running

* **Helm Chart Commands**
    * *helm repo add examples https://helm.github.io/examples*
    > This will add *examples* repo to your helm repositories
    * *helm repo ls*
    > This will list the available helm repositories
    * *helm install ahoy examples/hello-world -n demo*
    > This will install the *ahoy* helm chart from the repo *examples/hello-world* in *demo* namespace
    * *helm ls -n demo*
    > This will list the installed helm charts in *demo* namespace 
    * *helm history ahoy -n demo*
    > This will list the revisions done on *ahoy* helm chart 
    * *helm upgrade ahoy examples/hello-world -n demo*
    > This will upgrade *ahoy* helm chart to the latest version
    * *helm history ahoy -n demo*
    > See the revisions now showing *2* revisions on *ahoy*
    * *helm rollback ahoy 1 -n demo*
    > This will rollback *ahoy* helm chart to the version with revision number *1*
    * *helm history ahoy -n demo*
    > See the revisions now showing *3* revisions on *ahoy*