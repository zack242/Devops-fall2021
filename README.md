# Project of Devops

Repository of our project of DevOps

## Students

Zakaria Tozy <br>
email : Zakaria.tozy@edu.ece.fr <br>

Dan Nezri <br>
email : dan.nezri@edu.ece.fr <br>


## Projet

### 1. Create a web application

We used as support the lab 4 of DevOps, Where the front end will show us a Hello world page.

### 2. Apply CI/CD pipeline

We want to implement Continuous integration and Continuous Delivery so :<br>
-For the Continuous integration We implemented a main.yaml file which allows us to configure github action.Github action will perform tests at each push or pull request on the main branch <br>

<img src = "images/githubaction.png" width = 500 alt ="github-action">

- For the Continuous Delivery, We used Heroku : https://dashboard.heroku.com.
We configurated our workflows to deploy our application in heroku after the Continuous Testing.<br>

<img src = "images/CI-CD.png" width = 500 align="center" alt ="CI-CD">

In heroku, we created an application and this is the dashboard
<img src = "images/HerokuDashboard.jpg" width = 500 alt ="herokuDashboard">

If we go on Heroku we got a link and we can see our application.
<img src = "images/HerokuDeployement.png" width = 500 alt ="heroku deployment">

### 3. Configure and provision a virtual environment and run your application using the IaC approach

Vagrant is an open-source software product for building and maintaining portable virtual software development environments.We use vagrant with the centos7 distribution of linux,to configure the linux environment we use the following command.<br>

```
vagrant box add centos/7
```
chose the option 3 : virtual box.<br>

Now we can run our vagrant configuration file using : <br>
```
vagrant up
```
<img src = "images/vagrantup.png" width = 500 alt ="vagrant up">

Now we can acces to our virtual machine using ssh : <br>
```
vagrant ssh devops_server
```
<img src = "images/ssh.png" width = 500 alt ="vagrant ssh">

Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code.<br>

In our Vagrantfile,we configurate provision with Ansible

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
#language runtime
#database
#your application (use sync folders)
#health check of your application

But sadly, we didn't success !

### 4. Build Docker image of your application

First we used DockerDestop we run on our cli in the correct folder :
```
docker build -t dockerfile
```
We get on our DockerDestop the following image :
<img src = "images/4.1.jpg" width = 600 alt ="screen lab">

We run on the correct port using this command.
```
docker run -p 3000:3000 -d dockerfile
```
And we get : <br>
<img src = "images/4.2.jpg" width = 600 alt ="screen lab">

Then we want to implement it on dockerhub https://hub.docker.com/<br>
my profile name is arthur92i and link it to my dockerdestop
I push the image on it :
```
docker tag dockerfile arthur92i/Dockerfile
docker push arthur92i/dockerfile
```
And get this on my page.

<img src = "images/4.3.jpg" width = 600 alt ="screen lab">

### 5. Make container orchestration using Docker Compose

We add a file docker-compose.yaml for the container orchestration and using the following command :
```
docker-compose up -d
```
on the localhost we find again the Hello World
<img src = "images/5.1.jpg" width = 600 alt ="screen lab">
And on the DockerDestop we have also now a devops running :
<img src = "images/5.2.jpg" width = 600 alt ="screen lab">

### 6. Make docker orchestration using Kubernetes

We implement a new folder call k8s where our deployment.yaml and our services.yaml. After using the following command for activating our minikube :
```
minikube start
kubectl apply -f deployment.yaml
kubectl apply -f services.yaml
kubectl get pods
```
We see the following pods running :
<img src = "images/6.1.jpg" width = 600 alt ="screen lab">

And with the command :
```
minikube ip
```
We get the following table that indicate the url and target port
<img src = "images/6.2.jpg" width = 600 alt ="screen lab">

And the following page open :
<img src = "images/6.2.jpg" width = 600 alt ="screen lab">
### 7. Make a service mesh using Istio

### 8. Implement Monitoring to your containerized application
