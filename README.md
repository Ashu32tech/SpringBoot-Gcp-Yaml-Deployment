# SpringBoot-Gcp-Yaml-Deployment
//Deploying spring boot application via deployment.yaml with configMap
mvn clean package
docker build -t spring-boot-gke .
docker tag spring-boot-gke eu.gcr.io/crypto-truck-334202/spring-boot-gke


gcloud auth configure-docker 
docker push eu.gcr.io/crypto-truck-334202/spring-boot-gke


gcloud container clusters create "spring-boot-cluster" --scopes "https://www.googleapis.com/auth/cloud-platform" --num-nodes "1" --zone "europe-central2-a" --project "crypto-truck-334202"
gcloud container clusters get-credentials spring-boot-cluster --zone europe-central2-a --project crypto-truck-334202

kubectl apply -f deployment.yaml
kubectl get pods
kubectl get service

gcloud container clusters delete spring-boot-cluster --zone=europe-central2-a --project "crypto-truck-334202"