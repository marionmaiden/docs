# Helm - Concepts
- Chart: Helm package (equivalent to one dpkg)
- Repository: place to store and retrieve **charts** (equivalent to one maven repository)
- Release: instance of a **chart** running in a kubernetes cluster. Every chart deployment creates a new release. If you deploy the same chart twice in a cluster, both will be assigned with different release names.

## Helm Repository

### Public repo (
- Search a chart over the public Artifact hub: `helm search hub wordpress`

### Local repo
- List local repos: `helm repo list`
- Add a repository (e.g. github) to the local helm client: `helm repo add reponame https://brigadecore.github.io/charts`
- Update a repository (e.g. github) to the local helm client: `helm repo update reponame https://brigadecore.github.io/charts`
- Remove a repository (e.g. github) to the local helm client: `helm repo remove reponame`
- Search a chart over the repositories added to the local client: `helm search repo dispatcher`

## Helm Install
- Installing a package with a release name: `helm install happy-panda bitnami/wordpress` (release name and chart name)
- Installing a package with a random release name: `helm install --generate-name bitnami/wordpress`(only chart name is provided)
- Installing a package from a chart archive: `helm install foo foo-1.0.tgz`
- Installing a package from a chart folder:  `helm install foo /home/mario/foo`
- Installing a package from one url: `helm install foo https://example.com/charts/foo-1.0.tgz`

## Helm Status
- Check Helm release state: `helm status happy-panda` (release name)
- Check Helm release values: `helm get values happy-panda` (release name)
- Check Helm release history: `helm history happy-panda`(release name)
- List Helm deployed releases: `helm list`
- List uninstalled releases (which used --keep-history flag): `helm list --uninstalled`
- List all releases (deployed, failed or uninstalled with **--keep-history**): `helm list --all`
- View configurable options in the chart: `helm show values bitnami/wordpress` (chart name)

## Managing Helm charts
- Customizing one chart with configurable data
  ```
      # Addind properties to a yaml file
      $ echo '{mariadb.auth.database: user0db, mariadb.auth.username: user0}' > values.yaml
      # Installing a chart with the custom properties
      $ helm install -f values.yaml bitnami/wordpress --generate-name
  ```
## Update or Rollback a Chart Release
- Upgrading a chart with a different yaml properties file: `helm upgrade -f panda.yaml happy-panda bitnami/wordpress` (assuming that chart was installed before, it will be redeployed with the content of the panda.yaml file)
- Rollback a release to a specific revision: `helm rollback happy-panda 1` (rolls back the release to its first version)
- Rollback a release to the previous revision: `helm rollback happy-panda`

## Uninstall a Release
- Uninstall a release: `helm delete happy-panda`
- Uninstall a release but keep release history: `helm delete happy-panda --keep-history`

## Creating Charts
- Create a new chart: `helm create chartname` (creates a chart folder under **./chartname**)
- Validate the chart: `helm lint chartname``
- Package a chart for distribution: `helm package chartname` (after that, you can `helm install`it)
