
# GitLab Helm Chart

This chart is an easy way to get started with GitLab on Kubernetes. It includes everything needed to run GitLab, GitlabCI Runners, Docker Container Registry (with S3 storage backend), automatic SSL, and a dedicated load balancer for everything.

## Setup

```sh
# clone this repo
git clone git@github.com:reactioncommerce/chart-gitlab.git
cd chart-gitlab

# Copy the default `values.yaml` and fill in your custom options.
cp values.yaml custom.values.yaml

# Install Gitlab, Docker Registry, and Gitlab Runner
helm install --name gitlab --namespace gitlab -f custom.values.yaml ./

# Copy the default nginx-ingress values and set the ssh service name to "gitlab-gitlab"
cp nginx-ingress.values.yaml nginx-ingress.custom.values.yaml

# Install the Nginx ingress controller
# On AWS, this will provision an ELB for you. Retrieve that address in the next step
helm install --name nginx-ingress-gitlab --namespace gitlab -f ./nginx-ingress.custom.values.yaml stable/nginx-ingress

# Get the load balancer (ELB) URL
kubectl describe svc -n gitlab nginx-ingress-gitlab-nginx-ingress-controller | grep "LoadBalancer Ingress"

# point git.yourdomain.com and registry.yourdomain.com at that ELB address
```

More detailed descriptions of the above steps coming soon...
