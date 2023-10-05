# Task 3  
1.	Deploy Minikube  
2.	Deploy Argo CD.  
3.	Deploy Jenkins into you k8s cluster via Argo CD.  
4.	Install Jenkins k8s plugin  
5.	Create 2 namespaces, dev and prod  
6.	Write pipeline that will:  
 - implement hadolint check  
 - build Docker image in k8s agent (it can be basic python app for example)   
 - implement image substitution in the helm chart before pushing to the Chartmuseum  
 - deploy helm chart from Chartmuseum into k8s (perform install or rolling upgrade if already installed)  
7.	Modify your pipeline using ENV vars, so it will deploy your app differently, depending on ENV vars:  
 - with 1 replica if ENV = dev, 3 replicas if ENV = prod  
 - app should be deployed in different namespaces depending on same ENV var  
 - add 2 Jenkins secrets (some passwords) for dev and prod  
 - pass different k8s secrets (previously created passwords) depending on same ENV var  

# Implementation 
1. The task was done in GCP.  
   gcloud clusters container create task3
2. kubectl create namespace argocd  
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml  
   kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'  
3. kubectl create namwspace jenkins  
   kubectl apply -f jenkins-app.yaml  
   kubectl apply -f sa.yaml  
4. In complect with argo cd
5. kubectl create namespace dev
   kubectl create namespace prod
   jenkinsfile_build of pipeline attached
   jenkinsfile_deploy
   kubectl apply -f chartmuseum.yaml
6. kubectl apply -f app-secrets.yaml

   
   
