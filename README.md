<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a id="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
<!-- [![LinkedIn][linkedin-shield]][linkedin-url]
[![Github][github-shield]][github-url] -->


<!-- ABOUT THE PROJECT -->
## About the project

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/HansDoh2404/basic_mongo_db_cluster_with_k8s.git">
  <img src="architecture.png" alt="archi" width="800" height="800">
  </a>
 
  <h3 align="center">basic_mongo_db_cluster_with_k8s</h3>

  <!-- <p align="center">
    An awesome README template to jumpstart your projects!
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/othneildrew/Best-README-Template">View Demo</a>
    &middot;
    <a href="https://github.com/othneildrew/Best-README-Template/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/othneildrew/Best-README-Template/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p> -->
</div>

This project explains and demonstrates how to deploy a simple MongoDB cluster within Kubernetes. Through this hands-on demonstration, we aim to provide practical insights into successfully setting up MongoDB and performing basic operations within a real-world scenario.

<!-- GETTING STARTED -->
## Prerequisites

- **Minikube** - https://minikube.sigs.k8s.io/docs/start/ : local cluster with master and worker for using kubernetes
- **Kubectl** - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/ : command line tool to interact with your k8s cluster
- **Docker** - https://www.docker.com/get-started/ : container manager for launching container inside pod

## Quickstart

1. Clone the repo
   ```sh
   git clone https://github.com/HansDoh2404/basic_mongo_db_cluster_with_k8s.git 
   ```

2. Starting minikube :
   ```sh
   minikube status
   minikube start # if stopped
   ```

3. Run the command below to apply the persisting volume :
   ```sh
   kubectl apply -f pvc.yaml
   ```

4. After being sure that docker is launching, run these commands :
   ```sh
   kubectl apply -f mongo.yaml # launching the mongodb pod and his service
   kubectl apply -f mongo-express.yaml # launching the mongo-express pod (web app to manage mongo databases) and his service
   kubectl apply -f mongo-secret.yaml # configuring the secret (usernames and passwords for databas and web app)
   kubectl apply -f mongo-configmap.yaml # configuring the database url
   ```

5. Authorize and apply ingress :
  ```sh
  minikube addons enable ingress # authorize ingress
  kubectl apply -f mongo-secret-tls.yaml # configuring the certificates for secure connection
  kubectl apply -f mongo-ingress.yaml # apply ingress
  ```

6. Mapping the ip address and the domain name :
  ```sh
  -- run the command below
  minikube service mongo-express-service

  -- Copy the ip_address into the URL section and go to that file
  sudo nano /etc/hosts 

  -- Copy and paste it into the file, replace <ip_address> with the right
  <ip_address>   mongo-express.com 
  ```

7. Ensure that all is running fine :
  ```sh
  kubectl get pods # checking the pods
  kubectl get services # checking the pods
  kubectl get pv # checking the persistent volume
  kubectl get pvc # checking the persistent volume claim
  kubectl get nodes # cheking the nodes
  ```

8. Access the wep app in the browser :

  host : *mongo-express.com*
  username : *username*
  password : *password*

<!-- CONTACT -->
## Contact

Contributor : [@Hans Ariel](https://www.linkedin.com/in/hans-ariel-doh-59a31a2ba/) - hansearieldo@gmail.com
<br />
Project link: https://github.com/HansDoh2404/youtube_videos_2025_lakehouse.git


<!-- ACKNOWLEDGMENTS -->
## Useful

* [Shields.io](https://shields.io/) : for making badged dynamically
* [Kubernetes Tutorial for begineers(Full course in 4 hours)](https://www.youtube.com/watch?v=X48VuDVv0do&t=9791s) : full tutorial for learning kubernetes

<!-- MARKDOWN LINKS & IMAGES -->
[linkedin-shield]: https://img.shields.io/badge/linkedin-%230072B1?style=for-the-badge&logo=LinkedIn
[linkedin-url]: https://www.linkedin.com/in/hans-ariel-doh-59a31a2ba/
[github-shield]: https://img.shields.io/badge/github-black?style=for-the-badge
[github-url]: https://github.com/HansDoh2404