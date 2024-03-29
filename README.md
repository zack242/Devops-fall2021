# Project of Devops

Repository of our project of DevOps

## Students

Zakaria Tozy <br>
email : Zakaria.tozy@edu.ece.fr <br>

Dan Nezri <br>
email : dan.nezri@edu.ece.fr <br>


## Projet

### 1. Create a web application

- We used as support the lab 4 of DevOps, where the front end will show us a Hello world page.

### 2. Apply CI/CD pipeline

We want to implement Continuous integration and Continuous Delivery so :<br>
- For the Continuous integration We implemented a main.yaml file which allows us to configure github action.Github action will perform tests at each push or pull request on the main branch <br>

<img src = "images/githubaction.png" width = 500 alt ="github-action">

- For the Continuous Delivery, We used Heroku : https://dashboard.heroku.com.
We configurated our workflows to deploy our application in heroku after the Continuous Testing.<br>

<img src = "images/CI-CD.png" width = 500 align="center" alt ="CI-CD">

- In heroku, we created an application and this is the dashboard
<img src = "images/HerokuDashboard.png" width = 500 alt ="herokuDashboard">

If we go on Heroku we got a link and we can see our application.
<img src = "images/HerokuDeployement.png" width = 500 alt ="heroku deployment">

### 3. Configure and provision a virtual environment and run your application using the IaC approach

- Vagrant is an open-source software product for building and maintaining portable virtual software development environments.We use vagrant with the centos7 distribution of linux,to configure the linux environment we use the following command.<br>

```
vagrant box add centos/7
```
- we chose the option 3 : virtual box.<br>

- Now we can run our vagrant configuration file using : <br>
```
vagrant up
```
<img src = "images/vagrantup.png" width = 500 alt ="vagrant up">

- Now we can acces to our virtual machine using ssh : <br>
```
vagrant ssh devops_server
```
<img src = "images/ssh.png" width = 500 alt ="vagrant ssh">

- Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.<br>

- In our Vagrantfile,we configurate provision with Ansible

```
# Use Vagrant Ansible provisioner
config.vm.provision "ansible_local" do |ansible|
  # The path to the playbooks entry point
  ansible.playbook = "playbooks/run.yml"
  # Only run the roles with these tags
  ansible.tags = "install"
end
```
We try to do the provision of <br>
- language runtime
- database
- your application (use sync folders)
- health check of your application

But sadly, we didn't success !

### 4. Build Docker image of your application
- Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.<br>

- We created an image of our application using docker :
```
docker build -t devopszak .
```
<img src = "images/builddocker.png" width = 600 alt ="docker build">

- We get see our docker image using : <br>
```
docker images
```
<img src = "images/images.png" width = 600 alt ="images docker">

- We can run our images using : <br>
```
docker run -dp 3000:3000  devopszak
```
- We get acces to it at  : <br>
```
127.0.0.1:3000
```
<img src = "images/rundocker.png" width = 600 alt ="run docker">

- Now we push the image of our application in the dockerhub https://hub.docker.com/, but before that we need to configure a .dockerignore file to avoid pushing not necessary files <br>

- We tag our image and after we push it : <br>
```
docker tag devopszak  zack242/devopszak
docker push zack242/devopszak
```
- Now we can find it on the dockerhub.<br>

<img src = "images/dockerhub.png" width = 600 alt ="docker hub">

### 5. Make container orchestration using Docker Compose

- Compose is an orchestration tool that makes spinning up multi-container distributed applications with Docker.

- We add a file docker-compose.yaml for the container orchestration and using the following command to run it : <br>
```
docker-compose up
```
<img src = "images/docker-composeup.png" width = 600 alt ="docker compsoe">

And like for the docker image we can get acces to our application :
```
127.0.0.1:3000
```
<img src = "images/rundocker.png" width = 600 alt ="rundocker">


### 6. Make docker orchestration using Kubernetes

- Kubernetes is an open-source container-orchestration system for automating computer application deployment, scaling, and management. <br> <br>

- We implement a new folder call k8s where we set our Manifest yaml files
(deployment.yaml and our services.yaml).After we use the following command to start minikube and apply our manifest files to our cluster : <br>

```
minikube start
kubectl apply -f deployment.yaml
kubectl apply -f services.yaml
kubectl get pods
```

- We see the following pods running thanks to the commande kubectl get pods : <br>

<img src = "images/k8s.png" width = 600 alt ="k8s pods">

- With the following comande :
```
minikube service userapi

minikube ip
```
- We expose our Kubernetes service to the outside :

<img src = "images/openservice.png" width = 600 alt ="minikube ip">

And on the host :
```
192.168.99.101:31406
```
- We can find our application running :

<img src = "images/k8shost.png" width = 600 alt ="k8shost">

- We also setup 2 different persistent volume :

- PersistentVolume (PV) - a piece of storage in the cluster that has been provisioned by an administrator. It has a life cycle independent of any individual Pod that uses the PV.

- PersistentVolumeClaim (PVC) - a request for storage by a user.

- We apply this volume configuration to the pods of our deployment.

### 7. Make a service mesh using Istio

- Istio is an open source service mesh that layers transparently onto existing distributed applications.

- We deploy your application using Istio :

<img src = "images/istio2.png" width = 600 alt ="istio1">

<img src = "images/deployementIstio.png" width = 600 alt ="istio2">

- We didn't get 2 version of our app, for this we used the samples of the lab to the trafing-shifting and the route-request.

### 8. Implement Monitoring to your containerized application

- Install Prometheus and Grafana to your K8s cluster

```
kubectl apply -f samples/addons
```

<img src = "images/addons.png" width = 600 alt ="addons">


```
kubectl rollout status deployment/kiali -n istio-system
```
<img src = "images/addons2.png" width = 600 alt ="addons">

- Sadly we didin't get acces to the grafana or Prometheus dashboard.
