# Google-Kubernetes-Engine-Pipeline-using-Cloud-Build

## In this lab, you learn how to perform the following:

<br>Create Kubernetes Engine clusters.
<br>Create GitHub repositories.
<br>Trigger Cloud Build from GitHub repositories.
<br>Automate tests and publish a deployable container image via Cloud Build.
<br>Manage resources deployed in a Kubernetes Engine cluster via Cloud Build.</br>

## Overview

Cloud Build is a service that executes your builds on Google Cloud. It can import source code, execute builds, and more.

In this lab, you create a continuous integration and continuous deployment (CI/CD) pipeline that automatically builds a container image from committed code, stores the image in Artifact Registry, updates a Kubernetes manifest in a Git repository, and deploys the application to Google Kubernetes Engine using that manifest.

<img src="https://cdn.qwiklabs.com/7swem2VpBgLbbDMGVgWrtmVQtBlYOADPBh89k%2Bbb1S4%3D" />

For this lab you create 2 Git repositories:

app: contains the application source code
env: contains the Kubernetes deployment manifests
When you push a change to the app repository, the Cloud Build pipeline runs tests, builds a container image, and pushes the change to Artifact Registry. After pushing the image, Cloud Build updates the deployment manifest and pushes it to the env repository. This triggers another Cloud Build pipeline that applies the manifest to the GKE cluster and, if successful, stores the manifest in another branch of the env repository.

The app and env repositories are kept separate because they have different lifecycles and uses. The app repository is dedicated to a specific application, and is used mostly by actual humans. The env repository may be shared by several applications and is used by automated systems (such as Cloud Build). The env repository can have several branches, each mapping to a specific environment and reference a specific container image; the app repository does not.

When you finish this lab, your system can easily:

Distinguish between failed and successful deployments by looking at the Cloud Build history.
Access the manifest currently used by looking at the production branch of the env repository.
Rollback to any previous version by re-executing the corresponding Cloud Build build.


<img src="https://cdn.qwiklabs.com/qEN8Qxr82h1FkL8DhD5sqJmblM11i7JjhZv14OGahr0%3D" />
