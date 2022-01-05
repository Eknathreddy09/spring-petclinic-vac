# Deploying to Kubernetes

> NOTE: The provided `config/workload.yaml` file uses the Git URL for this sample. When you want to modify the source, you must push the code to your own Git repository and then update the `spec.source.git` information in the `config/workload.yaml` file.

## Deploying to Kubernetes as a TAP workload with Tilt

You can containerize this template app and deploy it as a Tanzu Application Platform (TAP) workload.
You need to have TAP installed on your cluster.
See the [VMware Tanzu Application Platform documentation](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/index.html) for details.

We have included a `Tiltfile` file to make this easier when deploying to a cluster.

For best results use Tilt version v0.23.2 or later. You can install Tilt by following these instructions: https://docs.tilt.dev/install.html

To set up the deployment environment set the CURRENT_CONTEXT environment variable.

Set CURRENT_CONTEXT using:

```
export CURRENT_CONTEXT=$(kubectl config current-context)
```

To build and deploy the app run:

```
tilt up
```

and follow the instructions (hitting space bar brings up the Tilt interface in your browser).

To uninstall the app run:

```
tilt down
```

## Accessing the app deployed to your cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

Determine the URL to use for the accessing the app by running:

```
tanzu apps workload get spring-petclinic
```

To invoke the deployed function run the following `curl` command in another terminal window:

```
curl <URL> -w'\n' -H 'Content-Type: text/plain' -d Fun
```

This depends on the TAP installation having DNS configured for the Knative ingress.