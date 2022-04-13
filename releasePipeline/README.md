# Release procedures

## Introduction

With many repos making up the Galasa project and many different types of artifacts being produced, the build and release of Galasa has become a little complicated.   These instructions detail the process of building, testing and releasing a version of Galasa and related components.

Galasa has been broken up into multiple components, and these components are only released if the component has changed.  These components (and related repos) are:-

1. Galasa (gradle, maven, framework, extensions, managers, obr, eclipse, isolated, docker)
1. CLI (cli)
1. Docker Operator (docker-operator)
1. Kubernetes Operator (kubernetes-operator)

The Galasa component is always released,  but the others are only cloned, built, tested and released if there are changes.

## Release process

### 1. Setup

1. Clone the argocd repo, main branch.  All the yaml and scripts you will be using can be found in the releasePipeline folder.
1. Ensure you are logged onto ArgoCD, `argocd login -sso argocd-cicsk8s.hursley.ibm.com`
1. Ensure you have the latest `galasabld` program from <https://galasadev-cicsk8s.hursley.ibm.com/prod/binary/bld/> and it is on the path.
 
For each of the Kubernetes Tekton command, you can follow with `tkn -n galasa-branch-release pr logs -f --last` to watch it's progress.  Only move onto the next command once the previous is completed successfully.

### 1. Create branch and ArgoCD applications

1. `01-create-namespace.sh` - Create the `galasa-branch-release` namespace in kubernetes.
1. `02-argocd-galasa.sh` - Create the deployments and tekton resources in kubernetes.
1. `03-argocd-cli.sh` - **Only if CLI being released** - Create the deployments in kubernetes.
1. `kubectl -n galasa-branch-release create -f 10-clone-galasa.yaml` - clone all the repos main branch to release branch.
1. `kubectl -n galasa-branch-release create -f 11-clone-cli.yaml` - **Only if CLI being released** - clone the repos main branch to release branch.
1. `kubectl -n galasa-branch-release create -f 12-clone-docker-operator.yaml` - **Only if Docker Operator being released** - clone the repos main branch to release branch.
1. `kubectl -n galasa-branch-release create -f 13-clone-kubernetes-operator.yaml` - **Only if Kubernetes Operator being released** - clone the repos main branch to release branch.

### 2. Build the components

1. `kubectl -n galasa-branch-release create -f 20-build-galasa.yaml` - Build the Galasa main component.
1. `kubectl -n galasa-branch-release create -f 21-build-cli.yaml` - **Only if CLI being released** - Build the CLI.
1. `kubectl -n galasa-branch-release create -f 22-build-docker-operator.yaml` - **Only if Docker Operator being released** - Build the Docker Operator.
1. `kubectl -n galasa-branch-release create -f 23-build-kubernetes-operator.yaml` - **Only if Kubernetes Operator being released** - Build the Kubernetes Operator.

### 3. Regression Test

1. Amend `29-regression-test-galasa.yaml` - set the correct version,  the bootVersion is unlikely to change. 
1. `kubectl -n galasa-branch-release create -f 29-regression-test-galasa.yaml` - Test Galasa.
1. Manually install and test the SimBank example in Eclipse.

All the test must past, reruns need to be managed manually at the moment.

### 4. Obtain release approval

1. Ask the Team and Product managers for release approval.

### 5. Deployment

1. Amend `30-deploy-maven-galasa.yaml` and amend the version parameter to the release.
1. `kubectl -n galasa-branch-release create -f 30-deploy-maven-galasa.yaml` - Deploy the maven artifacts to OSS Sonatype.
1. `31-oss-sonatype-actions.md` - Do the Sonatype actions detailed in this document.
1. `32-wait-maven.sh` - run the watch command to wait for the artifacts to reach Maven Central.  The release will appear in the BOM metadata.
1. Wait until Maven Central is updated.
1.  Amend `33-resources-image.yaml` - Set the version.
1. `kubectl -n galasa-branch-release create -f 33-resources-image.yaml` - Build the resources-image.
1.  Amend `34-deploy-docker-galasa.sh` - Set the version.
1. `34-deploy-docker-galasa.sh` - Deploy the Container images to ICR.
1.  Amend `35-deploy-docker-cli.sh` - **Only if CLI being released** - Set the version.
1. `35-deploy-docker-cli.sh`- **Only if CLI being released** - Deploy the CLI images to ICR.
1.  Amend `36-deploy-docker-docker-operator.sh` - **Only if Docker Operator being released** - Set the version.
1. `36-deploy-docker-docker-operator.sh`- **Only if Docker Operator being released** - Deploy the Docker Operator images to ICR.
1.  Amend `37-deploy-docker-kubernetes-operator.sh` - **Only if Kubernetes Operator being released** - Set the version.
1. `37-deploy-docker-kubernetes-operator.sh`- **Only if Kubernetes Operator being released** - Deploy the Kubernetes Operator images to ICR.

### 6. Update Reference Sites

1. `40-argocd-ibmcloud.md` - Follow the instructions to update the IBM Cloud Galasa external sites.
1. `41-eclipse-marketplace.md` - Follow the instructions to update the Eclipse Marketplace to advertise the latest Eclipse plugin.

### 7. Tag Release and Deploy CLI

1. Amend `50-tag-galasa.yaml` - Update the tag name,  must be prefixed with lowercase v.
1. `kubectl -n galasa-branch-release create -f 50-tag-galasa.yaml` - Tag the release on ALL repos.
1. `52-deploy-cli-release.md` - **Only if CLI being released** - Follow instructions to deploy the CLI to the repo release.

### 8. Clean up

1. `kubectl -n galasa-branch-release create -f 90-delete-branches-all.yaml` - Delete the release branch in ALL repos.
1. `92-delete-argocd.sh` - Remove the ArgoCD applications, and therefore the Kubernetes resources.
1. `93-delete-namespace.sh` - Delete the `galasa-branch-release` namespace in Kubernetes.

### 9. Bump to new version

1. Create a new Issue to cover the version bump and the appropriate branch development environment.
1. `99-Move-to-new-version.md` - Change the repos and files as listed in this file.
1. Run a complete build to verify everything looks ok.
1. Raise PRs to push the version changes.   Due to the nature of Galasa build,  later PRs will fail until the previous PRs are pushed and built.
