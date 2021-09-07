# Helm Chart Repository

[Helm](https://helm.sh) is a package manager for Kubernetes.

[Helm Charts](https://helm.sh/docs/topics/charts/) help you define, install, and upgrade even the most complex Kubernetes application.

This repository contains an example `Helm Chart` to deploy a [Nginx](https://www.nginx.com) web-server on Kubernetes.

> This repository was designed to support the [Medium Article](https://medium.com/) created to demonstrate how to create and use Helm Charts.

## Managing applications using charts

### Prerequisites

- `Helm 3` - Refer to the [Helm Installation Guide](https://helm.sh/docs/intro/install/) for instructions.
- Active `Kubernetes` installation

The charts in this repository were created using `helm 3.2.4` on `macOS` with a local [Minikube](https://minikube.sigs.k8s.io/docs/) installation.

### Helm Chart file structure

```text
my-nginx-chart
├── Chart.yaml           # A YAML file containing information about the chart
├── templates            # A directory of templates that, when combined with values, 
                         # will generate valid Kubernetes manifest files.
│   ├── NOTES.txt        # A plain text file containing short usage notes
│   ├── namespace.yaml   # A template to create a Kubernetes namespace
│   └── pod.yaml         # A template to create a Kubernetes pod to run Nginx
└── values.yaml          # The default configuration values for this chart
```

Refer to [Chart File Structure](https://helm.sh/docs/topics/charts/) documentation for more details.

### Testing the Helm Chart

Use the `--dry-run` flag from the `helm install` command to simulate an installation and verify potential problems.

`helm install my-nginx-chart -f my-nginx-chart/values.yaml my-nginx-chart --dry-run`

### Using this repository

#### Add the repository to helm client

Via the `helm repo add [NAME] [URL]` command with any name you would like to use to reference the repository.

`helm repo add my-nginx-chart https://rafaelmnatali.github.io/helm-charts/my-nginx-chart`

Confirm if the repository was added with the `helm repo list` command.

```text
NAME                    URL                                                                                  
my-nginx-chart          https://rafaelmnatali.github.io/helm-charts/my-nginx-chart
```

#### Install the helm chart

Deploy the Nginx chart with the `helm install` command.

`helm install nginx my-nginx-chart`

Output

```text
NAME: nginx
LAST DEPLOYED: Wed Apr  7 14:56:51 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. Get the application URL running with these commands:
export POD_NAME=$(kubectl get pods --namespace nginx -l "app=nginx-app" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace nginx port-forward $POD_NAME 8080:80
```

#### Confirming the installation

Confirm the deploy was successfully executed with the `helm list` command.

Output

```text
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
nginx   default         1               2021-04-07 14:56:51.547384 +0100 WEST   deployed        my-nginx-chart-0.1.0    1.16.0 
```

#### Uninstalling the helm chart

Uninstall the Helm Chart with the `helm uninstall` command.

`helm uninstall nginx`

Output

```text
release "nginx" uninstalled
```

## References

Visit the [Helm Documentation](https://helm.sh/docs/chart_template_guide/getting_started/) for more information and details on how to work with `helm`.
