# DevOps
Reppsitory for course of Devops with Adaltas

3 IOC
vagrant :
vagrant box add centos/7
use virtualbox
vagrant up

vagrant ssh devops_server

docker build -t devopszak .
docker images

docker run -dp 3000:3000  devopszak4

docker tag devopszak4  zack242/devopszak4
docker push zack242/devopszak4

docker-compose up


minukube start
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods


 kubectl expose deployments/userapi --type="NodePort" --port 3000

 kubectl get services

 minikube ip

 minikube service userapi

 docker ignore !!!


 kubectl apply -f samples/addons
 kubectl rollout status deployment/kiali -n istio-system


 kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.12/samples/addons/grafana.yaml


 kubectl get svc -n istio-system
