# Create and Manage Cloud Resources: Challenge Lab

## Challenge scenario

    You have started a new role as a Junior Cloud Engineer for Jooli, Inc. You are expected to help manage the infrastructure at Jooli. Common tasks include provisioning resources for projects.

    You are expected to have the skills and knowledge for these tasks, so step-by-step guides are not provided.

    Some Jooli, Inc. standards you should follow:

    Create all resources in the default region or zone, unless otherwise directed.

    Naming normally uses the format team-resource; for example, an instance could be named nucleus-webserver1.

    Allocate cost-effective resource sizes. Projects are monitored, and excessive resource use will result in the containing project's termination (and possibly yours), so plan carefully. This is the guidance the monitoring team is willing to share: unless directed, use f1-micro for small Linux VMs, and use n1-standard-1 for Windows or other applications, such as Kubernetes nodes.

### Task 1: Create a project jumphost instance

    Name the instance nucleus-jumphost.
    Use an f1-micro machine type.
    Use the default image type (Debian Linux).

#### Solution

```shell
gcloud compute instances create nucleus-jumphost \
    --machine-type=f1-micro
```

### Task 2: Create a Kubernetes service cluster

    The team is building an application that will use a service running on Kubernetes. You need to:

    Create a cluster (in the us-east1-b zone) to host the service.
    Use the Docker container hello-app (gcr.io/google-samples/hello-app:2.0) as a place holder; the team will replace the container with their own work later.
    Expose the app on port 8080.

#### Solution

```shell

gcloud container clusters create nucleus-cluster --zone=us-east1-b

gcloud container clusters get-credentials nucleus-cluster

kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:2.0

kubectl expose deployment hello-server --type=LoadBalancer --port 8080

kubectl get service

```
