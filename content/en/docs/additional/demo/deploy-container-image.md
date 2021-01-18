---
title: "9.9.2 Deploy a container image"
linkTitle: "Deploy image"
weight: 992
sectionnumber: 9.9.2
description: >
  This section covers deploying a container image to OpenShift.
---

## Task {{% param sectionnumber %}}.2: Deploy a container image

As you know from other techlabs, an easy way to create applications in OpenShift is using [oc new-app](https://docs.openshift.com/container-platform/latest/cli_reference/openshift_cli/developer-cli-commands.html#new-app)

Let's create an application for the go-hello-world image that we built before.

```bash
oc new-app appuio/go-hello-world --as-deployment-config
```

{{% alert  color="primary" %}}
Since [OpenShift 4.5](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-developer-experience) `oc new-app` creates a Deployment not a DeploymentConfig. We let it create a DeploymentConfig by adding the `--as-deployment-config` flag.
{{% /alert %}}

```
--> Found container image 5779c56 (11 days old) from  for "appuio/go-hello-world:latest"

    * This image will be deployed in deployment config "go-hello-world"
    * Port 8080/tcp will be load balanced by service "go-hello-world"
      * Other containers can access this service through the hostname "go-hello-world"

--> Creating resources ...
    deploymentconfig.apps.openshift.io "go-hello-world" created
    service "go-hello-world" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose svc/go-hello-world'
    Run 'oc status' to view your app.
```

To access the application from outside OpenShift, a route is needed:

```bash
oc create route edge --service=go-hello-world --insecure-policy=Redirect
```

Run the following command to determine the host of the newly created route.

```bash
oc get routes.route.openshift.io go-hello-world -o template --template '{{.spec.host}}{{"\n"}}'
```

```
go-hello-world-<username>.{{% param techlabClusterDomainName %}}
```

Now you can test the go-hello-world application over the route.
