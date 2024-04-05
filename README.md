# DEVOPS_Pract
ArgoCD
What Is Argo CD?
Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.
preview

Why should I use ArgoCD?
Application definitions, configurations, and environments should be declarative and version controlled.
Application deployment and lifecycle management should be automated, auditable, and easy to understand.
ArgoCD does watch not only the changes in Git Repository but also the changes in the cluster.
Any time a change happens in the git repository or cluster, it compares the actual state with the desired state.
ArgoCD compares the desired configuration in the Git repo with the actual state in the K8S cluster.
Argo CD architecture overview
Argo CD automatically deploys the desired state of an application in a specified target environment.
Updates are traceable as tags, branches, or pinned specific versions of a manifest at Git commits.
preview

What are the components of ArgoCD?
Argo CD control plane consists of three essential components- Application Controller, API Server, and Repository Service.
API Server:
The API server is a gRPC/REST server which exposes the API consumed by the Web UI, CLI, and CI/CD systems. It has the following responsibilities:

application management and status reporting
invoking of application operations (e.g. sync, rollback, user-defined actions)
repository and cluster credential management (stored as K8s secrets)
authentication and auth delegation to external identity providers
RBAC enforcement
listener/forwarder for Git webhook events
Repository Server:
The repository server is an internal service which maintains a local cache of the Git repository holding the application manifests. It is responsible for generating and returning the Kubernetes manifests when provided the following inputs:

repository URL
revision (commit, tag, branch)
application path
template specific settings: parameters, helm values.yaml
Application Controller:
The application controller is a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the repo). It detects OutOfSync application state and optionally takes corrective action. It is responsible for invoking any user-defined hooks for lifecycle events (PreSync, Sync, PostSync)

What is the deployment model of Argo CD?
Argo CD follows the GitOps model of deployment, where desired configuration changes are first pushed to Git, and the cluster state then syncs to the desired state in git.
This is a departure from imperative pipelines which do not traditionally use Git repositories to hold application config.
What is the difference between Kubernetes and Argocd?
Argo CD is a Kubernetes-native continuous deployment (CD) tool.
Unlike external CD tools that only enable push-based deployments, Argo CD can pull updated code from Git repositories and deploy it directly to Kubernetes resources.
Core Concepts
Let's assume you're familiar with core Git, Docker, Kubernetes, Continuous Delivery, and GitOps concepts. Below are some of the concepts that are specific to Argo CD. Referhere

Application A group of Kubernetes resources as defined by a manifest. This is a Custom Resource Definition (CRD).
Application source type Which Tool is used to build the application.
Target state The desired state of an application, as represented by files in a Git repository.
Live state The live state of that application. What pods etc are deployed.
Sync status Whether or not the live state matches the target state. Is the deployed application the same as Git says it should be?
Sync The process of making an application move to its target state. E.g. by applying changes to a Kubernetes cluster.
Sync operation status Whether or not a sync succeeded.
Refresh Compare the latest code in Git with the live state. Figure out what is different.
Health The health of the application, is it running correctly? Can it serve requests?
Tool A tool to create manifests from a directory of files. E.g. Kustomize. See Application Source Type.
Configuration management tool See Tool.
Configuration management plugin A custom tool.
Argo CD Best Practices:
Separating Source Code and Configuration Repositories
Selecting a Suitable Number of Deployment Configuration Repositories
Testing Manifests Before Each Commit
Preventing External Changes to Manifests
Workflow to Install ArgoCD
First preference - Referhere
Second Preference - Referhere
