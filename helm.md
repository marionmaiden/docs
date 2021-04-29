# Helm - Concepts
- Chart: Helm package (equivalent to one dpkg)
- Repository: place to store and retrieve **charts** (equivalent to one maven repository)
- Release: instance of a **chart** running in a kubernetes cluster. Every chart deployment creates a new release. If you deploy the same chart twice in a cluster, both will be assigned with different release names.

## Helm Repository
- Adding a repository (e.g. github) to the local helm client: `helm repo add https://brigadecore.github.io/charts`
- Search a chart over the public Artifact hub: `helm search hub wordpress`
- Search a chart over the repositories added to the local client: `helm search repo dispatcher`

## Helm Install
- Installing a package in kubernetes with a release name: `helm install happy-panda bitnami/wordpress` (release name and chart name)
- Installing a package in kubernetes with a random release name `helm install --generate-name bitnami/wordpress`(only chart name is provided)

## Helm Status
- Check Helm release state: `helm status happy-panda` (release name)
- View configurable options in the chart: `helm show values bitnami/wordpress` (chart name)
