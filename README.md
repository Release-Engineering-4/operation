# Group 4 Operation repository
This repository contains everything to run the application.

# Vagrant
Go into the `/operation` directory and run `vagrant up` to start up the the application through vagrant. It should also automatically use ansible playbooks to setup the environment.

# Note
We have decided to not use Vagrant and skip the provisioning part since we could not get it to work. However, it can still be graded and parts of the provisioning and Vagrant are working, like booting up the VM's and using Ansible playbooks. Though installing kubernetes that works across machines was not viable in the time. So to showcase it works in a kubernetes cluster we use Minikube.

# Deploying the app
You can deploy the app using any kubernetes cluster distribution. We used minikube to work and test the deployment of the application and the backend model service. 

To deploy just use the following command:

```bash
kubectl apply -f deploy.yml
```

This deploys the front-end application and hosts the model service backend which the front end can POST a request. The website you can access through `http://localhost/`.

The kubernetes yaml file pulls the two container images from their respective github package repository.

## Setting up a local kubernetes cluster to deploy the application
See this page for instructions to install [minikube](https://minikube.sigs.k8s.io/docs/): https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download

First start your cluster:

```bash
minikube start --driver=docker
```

Make sure to enable ingress:
```bash
minikube addons enable ingress
```

Furthermore, to allow monitoring of the app you must install the full [Prometheus stack](https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack) to the Kubernetes cluster. We recommend using [Helm](https://helm.sh/) to install the Prometheus stack. The followings steps assume you've installed Helm.

After you've installed Helm we first must get the Helm repository info:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

Now you can install the Prometheus Stack with:

```bash
helm install myprom prom-repo/kube-prometheus-stack
```

Apply the `kubernetes.yml` file to deploy the application, change the `replicas` variable to change the amount of copies to deploy:

```bash
kubectl apply -f kubernetes.yml
```

Because we use Minikube, there are limitations with virtualization through the Docker network. So, we need to create a Minikube tunnel to access the Ingress:

```bash
minikube tunnel
```

Run this command in a separate terminal and keep it open to be able to access the application through the following URL: `http://localhost/`.

