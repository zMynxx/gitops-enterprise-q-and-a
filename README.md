# gitops-enterprise-q-and-a
# Questions and Answers

## Splitting your manifests between infrastructure (nginx, cert-manager) and developer applications is generally a good practice because:

- They have different lifecycles and constraints
- Developers don't really care about infrastructure manifests
- Manifests for developer applications change much more often
- **✔️ All of the above**

## How many types of manifests are generally stored in a GitOps repository?

- **✔️ Four - ArgoCD manifests and Kubernetes manifests for infrastructure applications, and the same categories again for developer applications**
- Two - Helm manifests and Kustomize manifests
- Three - AWS manifests, GCP manifests and Azure manifests
- Just one. JSonnet manifests

## When a developer "promotes" an application in Kubernetes what do they want to do?

- Update the container image tag to a new version
- Update a configuration setting in a configmap
- Update a configuration setting in a deployment YAML
- **✔️ Any of the above or a combination of the above**

## If you want to define extra Helm values inside an Argo CD application manifest ideally you should use:

- The "helm.parameters" property
- The "helm.values" property
- The "helm.valuesObject" property
- **✔️ The "helm.valueFiles" property**

## What is the proper way to group multiple applications together in a large Argo CD instance?

- **✔️ You should use Application Sets or the App-of-Apps pattern**
- You should use the "multi-source" feature of Argo CD
- You should use a monorepo with different branches for each application
- You should use the "parameter overrides" feature of Argo CD with different configurations for each application

## It is best to force developers to have both Kubernetes and Argo CD on their workstations for testing locally their applications.

- True
- **✔️ False**

## Argo CD supports a "valuesObject" property inside an Application CRD. Is it a good practice to use it?

- Yes because it bundles everything an application needs in a single file
- Yes because you can add your own value overrides inside an Argo CD application
- **✔️ No because you are mixing different types of manifests in the same application, forcing developers to need Argo CD even for local deployments**
- No because this information is not stored in Git and therefore doesn't follow the GitOps principles.

## What is the main purpose of the "multi-sources" feature in Argo CD?

- You should use "multi-sources" to group several microservices in a single Argo CD application
- You should use "multi-sources" to group all infrastructure apps (certmanager, nginx) of a cluster in a single Argo CD application
- **✔️ You should use "multi-sources" to attach local Helm values on an external Helm chart from a Helm repository**
- You should use "multi-sources" to merge several Helm charts together in order to form an "umbrella"

## Argo CD supports a "kustomize" property inside an Application CRD. Is it a good practice to use it?

- Yes because it bundles everything an application needs in a single file
- Yes because you can add your own kustomize overrides inside an Argo CD application
- **✔️ No because you are mixing different types of manifests in the same application, forcing developers to need Argo CD even for local deployments**
- No because you shouldn't use Kustomize for Argo CD applications. Helm charts are the best recommendation for your own applications

## A developer wants to test locally a Helm application that is already deployed by Argo CD in the "Staging" environment. Ideally,

- The developer must get locally the Helm charts, the Helm values and the "Staging" Application Set manifest in order to recreate the same configuration
- The developer must first install locally the exact same Argo CD version as the instance that deploys apps to "Staging"
- **✔️ The developer doesn't need Argo CD at all. They can deploy the application locally with just the Helm CLI and associated value files from Git**
- The developer can use any Argo CD version locally as long as it is the same major version as the Argo CD instance that is deploying apps in "Staging"

## A developer wants to test locally a Kustomize application that is already deployed by Argo CD in the QA environment. Ideally

- The developer must get locally the base manifests, the QA overlays and the QA Application Set manifest in order to recreate the same configuration
- The developer must first install locally the exact same Argo CD version as the instance that deploys apps to QA
- **✔️ The developer doesn't need Argo CD at all. They can deploy the application locally with just the kustomize CLI and associated overlays as stored in Git files**
- The developer can use any Argo CD version locally as long as it is the same major version as the Argo CD instance that is deploying apps in QA

## Does Argo CD support Kustomize components and Kustomize transformers?

- Argo CD supports only Kustomize Overlays. Neither components nor transformers are supported
- **✔️ Argo CD has built-in support for both Kustomize components and Kustomize transformers**
- Argo CD supports Kustomize overlays and Kustomize transformers but not Kustomize components
- Argo CD supports Kustomize overlays and Kustomize components but not transformers

## How many value files can you attach to an Argo CD application?

- Only one value file is supported in a single Application. Same restriction as the Helm CLI
- **✔️ A single Argo CD application can define multiple value files with a clear order precedence in a similar manner to the Helm CLI**
- A single Argo CD application supports a single value file. You must use application sets if you need multiple value files
- In the default configuration only one value file is supported. With the new multi-sources feature of Argo CD, multiple value files are supported

## A new developer has joined the team and they want to find all settings for a Helm application as it runs in the QA environment. Ideally:

- **✔️ The developer looks at a single place - the Helm values of the application as they are stored in Git. No Argo CD knowledge is necessary**
- The developer need to look at two places. The Helm values as stored in the Git and the QA application Set (also stored in Git)
- The developer needs to look at 3 places. The Helm values of the app, the parameter overrides in Argo CD and the QA application Set
- The developer needs to look at 4 places. The Helm values of the app, the parameter overrides in Argo CD, the QA application Set and the parent Helm chart that creates all Application Sets.

## A new developer has joined the team and they want to find all settings for a Kustomize application as it runs in the Staging environment.

- **✔️ The developer looks at a single place - the Kustomize overlays of the application as they are stored in Git. No Argo CD knowledge is necessary**
- The developer need to look at two places. The Kustomize overlays as stored in the Git and the Staging application Set (also stored in Git)
- The developer needs to look at 3 places. The Kustomize overlays of the app, the parameter overrides in Argo CD and the Staging application Set
- The developer needs to look at 4 places. The Helm values of the app, the parameter overrides in Argo CD, the Staging application Set and the parent Helm chart that creates all Application Sets.

## What is the major disadvantage of promoting Argo CD applications by using branch names in the "targetRevision" property?

- Branches are not allowed in the "targetRevision" property. Only Git commit hashes are allowed
- Branches should not be used for shadow releases. Only Git tags should be used in the "targetRevision" property.
- There isn't a disadvantage if you agree with your team to use Semantic versioning in the "targetRevision" property and proper ranges
- **✔️ You lose several auditing benefits of GitOps. Simply looking at the Git repository history doesn't tell you anymore what version was deployed in the past as branch names are moving targets.**

## How many levels of templating should you use in your Argo CD applications?

- **✔️ Just one. Helm and Kustomize are enough on their own. For extra flexibility you can also template Application Sets with the different generator options.**
- If you use Helm charts you need at least two. The Helm charts for the applications themselves and a parent Helm chart for creating Application Sets
- You always need at least two. Helm or Kustomize for the applications themselves and a Helm umbrella chart for all Application CRDs.
- It depends on if you use Helm or Kustomize. Helm application should always be post-processed with Kustomize. Kustomize applications should also be grouped with an Application Set.

## What is the proper mechanism to create multiple Argo CD applications with different configurations?

- **✔️ Application Sets are created exactly for this scenario. They offer different generators for automatically creating a large number of applications.**
- You must use CUE or HCL to create multiple Argo CD applications
- You can create multiple Helm applications with Application Sets. For Kustomize apps you need App-of-Apps.
- Argo CD can natively handle multiple applications with just "envsubst" and the Argo CD CLI. Nothing extra is needed.

## How many Application Sets should you have in your organization?

- Just one. That is the whole point of using Application Sets
- You should have one application set per Argo CD instance
- You should have always 2. One application set for developers applications and one application set for infrastructure (cert-manager, nginx etc).
- **✔️ You can have as many application sets as you like. It depends on your teams, environments, clusters, deployment options etc.**

## What is the implicit requirement for using the cluster generator in an Application Set?

- **✔️ You are using the hub-and-spoke model so that your Argo CD instance has access to several clusters**
- You have already placed labels in your clusters, so that the generator can pick the correct ones
- Each cluster that belongs to the generator must have Argo CD installed in advance
- You have removed all list generators from the application set as they cannot work together with cluster generators

## If you choose to store your Application Set in a Git repository

- It has to be in the same Git repository with the Kubernetes manifests it will deploy
- It has to be in the same Git repository as all other application sets deployed in the same cluster
- It has to be in the same Git repository as all other application sets managed by the same ArgoCD instance
- **✔️ it can be a different Git repository than the one that contains the Kubernetes manifests**

## Should you store all manifests from all applications from all clusters ln a single GitOps monorepo?

- **✔️ It depends. Even though in some aspects it is easier to manage your Argo CD apps this way, you might have several performance bottlenecks.**
- No. You should use one Git repository per Kubernetes cluster
- Yes. This is a strict requirement as all Application Sets of the same Argo CD instance must be placed in the same Git repository.
- It depends. If you follow the hub-and-spoke model you need a Git monorepo. If you have multiple Argo CD instances you need a Git repository per cluster.

## Where should you store Application manifests for infrastructure applications (cert-manager, nginx etc)?

- In the same application sets as the ones that define developer applications. It is so easy!
- **✔️ In different application sets than developer applications. They have different requirements, deployment velocity and target audience.**
- If they are Helm charts, they should be stored in an external Helm repository. If they are Kustomize they should be stored in Git.
- They should be stored in the same Application Set as the ones that define the respective source code repositories.

## Why are preview/ephemeral environments useful to developers?

- Because they can test their features in isolation
- Because they are not limited by a static number of test environments anymore
- Because they can create/delete environments at will without opening tickets anymore
- **✔️ All of the above**

## What is the recommended way to use preview environments for developers?

- Developers will open a ticket when they need a new environment and a second ticket when they want it shut down
- **✔️ Developers will get automatically an environment when they open a pull request. The environment will disappear when they merge/close the Pull request**
- Developers will need to run a special Cl pipeline for creating a new environment and another pipeline to shut it down
- Developers will need to create a new namespace on a cluster to create a new environment and delete the namespace to discard it

## What is the best way to create preview environments with Argo ?

- **✔️ Use the Pull Request Generator of Argo CD**
- Use the Event Source of Argo Events
- Use the Analysis of Argo Rollouts
- Use the Artifact Repository Reference in Argo Workflows

## The Pull Request generator can monitor pull requests

- only from the Git repository that contains source code
- only from the Git repository that contains Helm charts
- only from the Git repository that has the Application Set that defines the PullRequest Generator
- **✔️ from any Git repository where correct credentials are provided**

## If a Pull Request generator monitors a repository with source code you need to account

- for the case where developers don't put labels in their Kubernetes manifests
- for the case where the Application Set is in a different repository than the one that hold source code
- **✔️ for the case where the container image is not yet built, when the preview environment is created**
- for the case where the target Kubernetes cluster doesn't have enough namespaces for preview environments

## The "requeueAfterSeconds" property in a Pull Request generator must be set

- with a low value so that developers do not have to wait for their new environment
- with a high value so that the Kubernetes cluster has enough namespaces for preview environments
- to 0 so that no pull requests are monitored at all
- **✔️ with a value that honors the rate limits of the Git installation while still providing a good experience to developers**

## What happens if a developer commits again on a PR that already has a preview environment via the Pull Request generator?

- Argo CD will delete the application and recreate from scratch with the new container image
- **✔️ Argo CD will update the existing application with the new container image**
- Nothing will happen unless the developer syncs manually the application again
- Nothing will happen. The developer must create a new Pull Request for any additional changes

## When using the Pull Request Generator how are preview environments cleaned up?

- **✔️ A preview environment is automatically discarded when the respective pull request is closed**
- You must delete the Application Set so that all active environments are deleted as well
- You must create a custom Kubernetes job to automatically delete preview environments
- Developers will need to run a special Cl job in order to clean their environment

## What is the recommended way to keep track of all preview environments created by the Pull Request generator?

- Use the same namespace for all environments but different configmaps
- **✔️ Use different namespaces, one for each preview environment**
- Use different Kubernetes nodes, one for each preview environment
- Use different application sets, one for each environment

## What are Helm value hierarchies?

- **✔️ A set of different value files for a single Helm application with a specific order**
- A new Helm capability of Argo CD that was added with the "multi-source" feature
- The pattern where you apply Kustomize modifications to an existing Helm chart
- The pattern where you store all of your Helm charts in the same repository as the source code

## What are the requirements for using Helm value hierarchies?

- **✔️ Only Helm is required. They are a built-in feature of Helm**
- You need a recent version of Argo CD with the "multi-source" feature
- You need Argo CD plus Application Sets to use Helm value hierarchies
- It is a built-in feature of Helm available to umbrella Helm charts only

## If you define multiple value files in a single Argo CD application the order of precedence

- **✔️ is the same at the Helm CLI. The last value file mentioned "wins" in case of conflicts.**
- is the opposite from the Helm CLI. The first value file mentioned "wins" in case of conflicts.
- is the same as the list generator in the same application set
- is undefined. Unless you use the "multi-source" feature of Argo CD. In that case the last "source" entry wins.

## How can you load Helm values from Git with a chart stored in a Helm repository in a single Argo CD application?

- You cannot do that. The Helm chart must be also placed in Git along with the value files.
- **✔️ You can do that with the "multi-source" feature of Argo CD**
- You cannot do that in a single application unless you use an Application Set with the SCM and file generators.
- You can do that only if the Helm repository is OCI compliant.

## If you use the "multi-source" feature of Argo CD how many source entries should you typically have in the same file?

- **✔️ 2 or 3. One of the external chart and one for you local Helm values or extra configuration**
- You need one source entry for each application deployed on the same cluster
- You need one source entry for each Helm chart deployed on the same cluster
- You need one source entry for each cluster that is part of the same application set.

## How can you make Application Sets work with Helm value hierarchies?

- You need to add the "go Template:true" property at the top of the application set first.
- **✔️ Nothing special is needed. Application Sets support Helm value hierarchies like normal ArgoCD applications**
- You need to make sure first that the chart you define is in Git and not in a Helm repository
- You need to make that you have a recent version of Argo CD that supports the "multi-source" feature.

## You have a set of different configurations of a Helm application that you want to deploy with Argo CD.

- **✔️ The different configuration should be saved as different Helm value files or a Helm value hierarchy (same as the Helm CLI)**
- The different configurations must be mapped to the "multi-source" feature of Argo CD
- The different configurations should be saved in the "helm" property in the main Application CRD
- The different configurations should be saved on different Umbrella charts that are stored in OCI repositories

## If you want to change the application configuration for an application that is using a Helm value hierarchy

- **✔️ You need to find the respective Values file in git and edit/commit/push your changes.**
- You need to find the appropriate List generator in the parent Application Set and change the order of entries there
- You need to locate the respective Application CRD and change your setting in the "helm" property
- You need to download the whole Helm chart from the OCI repository and commit it locally in Git first.

## What is the correct way to use Secrets with Argo CD?

- You must use the sealed secrets controller
- You must use Hashicorp vault and the Argo CD Vault plugin
- You must use 1Password and the external secret operator
- **✔️ Argo CD does not prescribe a specific secret solution. It depends on your requirements, risk acceptance, legal limitations etc.**

## If you are using Argo CD, you are forced to store all your secrets in Git as well.

- True
- **✔️ False**

## What is the External Secret Operator?

- **✔️ It is Kubernetes controller that can fetch secrets from external sources and pass them to your Argo CD applications**
- It is an Argo CD plugin that can fetch secrets from external sources and pass them to your Argo CD applications
- It is fast caching solution for Kubernetes secrets
- It is a cloud agnostic secret provider like Hashicorp Vault

## What is the main advantage of having an application read its secrets from plain files?

- The application is very easy to run locally for developers even outside of Kubernetes
- The application can automatically reload secrets on its own by monitoring files without any pod restarts
- Kubernetes has a built-in feature for mounting secrets as files making deployment very simple
- **✔️ All of the above**

## Can you use Argo CD without storing any kind of secret in Git?

- **✔️ Yes, you can have Argo CD fetch secrets from an external provider using a trust policy (e.g.**
- No, you always need sealed secrets in the same cluster as Argo CD
- No, even if your external secrets are stored somewhere else, you still need to store in Git the authentication token for retrieving all secrets
- Yes, but only for stateless workloads

## How does the External Secret Operator integrate with Argo CD?

- The external secret operator works as an Argo CD configuration plugin
- **✔️ The external secret operator introduces an External Secret CRD that is applied by Argo CD in the cluster like any other resource**
- The external secret operator calls the Argo CD API to inject secrets into applications
- The external secret operator runs as a pre-sync hook in Argo CD sync operations in order to add secrets in the application

## How do you rotate your secrets in Argo CD, if you use the External Secret Operator?

- You need to undeploy the appropriate ExternalSecret resource and apply it again so that changes take effect
- You need to undeploy the ClusterSecretStore resource and apply it again so that changes take effect
- You need to deploy/restart the controller so that it fetches all new secret values
- **✔️ Nothing special is needed. The external secret operator automatically refreshes secrets (with a configurable period)**

## What is the easiest way for an Argo CD application to reload its Kubernetes secrets?

- You should delete all the local volumes of the pod and recreate them by hand
- You should kill the pod and restart it so that it fetches the new secrets
- **✔️ You should make sure that the application reads secrets from files and is also setup to monitor those files for new changes. Then no special action is required.**
- You should send the SIGKILL unix signal to the application that is running inside the pod

## If you are using Argo CD where should you store your secrets?

- In Git only
- In Hashicorp Vault
- In the external secret operator (ESO)
- **✔️ Argo CD is secret agnostic. You can keep your secrets in your existing secret provider and inject them in your Argo CD applications**

## How do you define dependencies between different Argo CD applications and define a strict deployment order?

- Using the "dependOn" keyword
- Using Sync hooks
- Using Sync Windows
- **✔️ There is no mechanism in vanilla Argo CD for ordering the deployment of applications in a graph like manner**

## The Argo CD Pull Request generator can be combined with the vCluster project

- **✔️ to create preview environments with a full cluster instead of just a namespace**
- to install Argo CD with Helm charts instead of Kustomize files
- to pass the proper values from Terraform to Argo CD
- to cleanup preview environments automatically after a specific period of time

## Can you use Sync waves to define a dependency order between different Argo CD applications?

- **✔️ No. Sync waves work by default only on individual Kubernetes resources and not Argo CD applications.**
- No. Sync waves also need to be combined with Sync Phases for creating a dependency graph between Argo CD applications.
- Yes, sync waves work on both Kubernetes resources and Argo CD applications in similar manner out of the box
- Yes, but only if Sync waves are used with positive numbers and not negative numbers.

## How can you make Sync Waves apply to Argo CD applications for defining a deployment order?

- You need to modify Argo CD with custom health check for applications that is not part of the default installation
- You need to make sure that your applications have proper readiness and liveness probes
- You need to place all your applications in a parent application following the app-of-apps pattern
- **✔️ All of the above**

## Out of the box, Argo CD supports a custom deployment order only between

- **✔️ individual Kubernetes resources**
- individual Argo CD applications
- individual Argo CD Application Sets
- List generators

## If you are not familiar with Argo CD finalizers you risk the danger of:

- Removing Argo CD applications and Kubernetes resources by mistake
- Keeping Kubernetes resources around even when the parent Argo CD application was removed
- Thinking that a resource will be recreated when in fact it is deleted completely
- **✔️ All of the above**

## What are Argo CD finalizers?

- **✔️ A mechanism that defines cascading removal instructions between different Argo CD resources**
- A way to auto-clean namespaces when their Kubernetes deployments no longer exist
- A way to stop developers from clicking the "delete" button in the Argo CD UI
- A way to make sure that all Argo CD application Sets are always committed to Git first

## What is the relationship between Argo CD finalizers and Kubernetes finalizers?

- **✔️ Argo CD finalizers are a form of Kubernetes finalizers but for Argo CD resources**
- Argo CD finalizers are a replacement for Kubernetes finalizers
- Argo CD finalizers are a special Kubernetes finalizer that only works on namespaces
- Argo CD finalizers only take effect when accessed by the Argo CD UI. Kubernetes finalizers don't work in the Argo CD UI

## Where can you place Argo CD finalizers?

- **✔️ on any Argo CD resource.**
- on any Kubernetes resource
- on any Application Set
- on any resource that is already marked with a sync wave

## What does an Argo CD finalizer line do when added inside an Argo CD yaml file?

- **✔️ It doesn't do anything on its own. It is just an instruction for the different Argo CD controllers on how to react to deletion events**
- It automatically clears the target namespace when the last Argo CD application is removed
- It removes the parent Application Set when a child Application is deleted
- It blocks the removal of a namespace while it still contains Argo CD applications inside.

## If you delete an Application Set then all child applications will also be deleted

- Yes, because an Application Set always adds finalizers in child applications
- **✔️ Not always, it depends on whether the flag syncPolicy preserveResourcesOnDeletion was used or not**
- No, child applications will never be deleted.
- Not always, it depends on the sync waves inside the child applications.

## Is it possible to delete an Argo CD application but keep the underlying resources in the cluster?

- No this is not possible.
- **✔️ Yes you can do this if you remove the finalizer from the Application CRD and then delete the Application Resource itself**
- If the Argo CD application is part of Application Set you cannot do it. If the application is part of app-of-apps then you can do it.
- Yes but you must delete the application with the Argo CD CLI and not the Argo CD UI

## When you add a finalizer to an Argo CD resource, you essentially:

- define that you want the target deployment namespace to be removed as well when you delete the application
- instruct ArgoCD to never delete this application
- **✔️ say to the respective Argo CD controller that removing this resource should also remove its children resources**
- make this resource delete its parent Application Set

## You can easily rename an Argo CD application without downtime:

- by editing the application name from the Argo CD UI
- by editing the backing Git file and committing/pushing it again
- by adding the Application to a parent application Set with a different child name
- **✔️ You can't. Renaming any application will make Argo CD delete it and recreate from scratch.**

## How can you migrate an Argo CD application between 2 Argo CD instances without downtime?

- You can't. You need to use Argo Rollouts to avoid downtime when moving applications between Argo CD instances
- **✔️ You can make both instances manage the application and then delete the application from the first instance ensuring that no finalizers are present**
- You need to add the application to an Application Set and migrate the Application Set first
- You deploy the same application again in the second Argo CD instance but with a different sync wave.

## You look at an Argo CD application inside your cluster and your colleague just removed the finalizer:

- This is really bad because somebody will now delete the application and leave Kubernetes resources behind
- This is really good because now you can migrate easily the application to a different cluster
- **✔️ This can be good or bad depending on the use case. It is best to ask the colleague what they want to do.**
- This is bad because now the parent Application Set will be deleted as well

## What is the correct way of migrating an Application between 2 Argo CD instances without downtime?

- Deploying the application to the second cluster, removing finalizers from the first instance only and removing it from the first instance
- Removing finalizers from the first instance, deleting the application and then deploying it again on the second instance
- Removing the application from the UI of the first instance using the orphan prune propagation
- **✔️ Any of the above procedures will have the same end result**

## Does Argo CD support multi tenant Kubernetes clusters?

- **✔️ Yes, and there is even an RBAC mechanism for multi-tenant installations**
- Yes, but only if you use multiple Argo CD instances (one per namespace)
- No, a single Argo CD instance can only work with a single Kubernetes cluster
- Yes but only if you install Argo CD without the Web UI

## When can you use the multi-tenant features of Argo CD?

- Only when Argo CD is installed in the hub-and-spoke model
- Only when Argo CD doesn't deploy applications on the same cluster as it is running on
- Only when Argo CD deploys applications to the same cluster it is running on.
- **✔️ You always have access to multi-tenant features regardless of the number of clusters managed by the Argo CD instance**

## What is the best way to use the Argo CD UI?

- Make it read-only for developers and read-write for operators
- Hide it completely from developers and only allow operators to access it
- Give access to developers for syncing their applications but not allow them to delete anything
- **✔️ You can use the Argo CD UI in any way that is compliant with your organizational needs and requirements.**

## The Argo CD RBAC mechanism:

- is a superset of the built-in Kubernetes RBAC
- is a replacement for Kubernetes RBAC
- **✔️ can be used in tandem with Kubernetes RBAC.**
- is a custom implementation of the Kubernetes RBAC

## What can you define with an Argo CD AppProject?

- What users can do to Argo CD applications (edit, view, delete)
- Which Git repositories can be used for deploying Applications
- What clusters can be used for deploying Applications
- **✔️ All of the above**

## Can you define a policy in Argo CD that defines which specific action a specific user can do to an individual resource?

- No, Argo CD RBAC always works with groups of users and never individual users
- No, Argo CD always works the groups of actions and never single actions
- **✔️ Yes you can, but in most production setups Argo CD works with groups of entities instead of individual entities**
- Yes you can but only if you use a global policy setting and not a per Project policy setting

## What model does the RBAC policy in Argo CD follow?

- **✔️ the who-what-how model**
- the who-what-when model
- the how-when-why model
- the who-when-what-how model

## How do you define Argo CD RBAC policies?

- You can only define what actions are "not allowed" for a user. Everything else is allowed by default
- You can only define what actions are "allowed". Everything else is disabled by default
- **✔️ You can define both "allowed" and "not allowed" actions. Default behavior depends on several factors including global policies and parent AppProjects**
- You can define "not allowed" policies for groups of users and "allowed" policies for individual users

## An Argo CD RBAC policy:

- connects specific users to specific Argo CD resources
- connects specific users to specific Argo CD actions
- **✔️ is not tied to specific users. It only defines what somebody can do on an Argo CD resource**
- connects specific users to specific clusters

## Where should you store Argo CD RBAC policies?

- in the ArgoCD UI via the friendly editor
- **✔️ in Git like all other Argo CD resources**
- in a special namespace in your Argo CD cluster that contains all other policies
- in the same namespace where the affected application resides

## How can you secure the Argo CD UI with many developers teams?

- All teams will see all applications from all other teams. But you can disable syncing for applications that belong to different teams.
- All teams will be able to look and sync all other applications. You need to talk to developers and warn them about this
- **✔️ All teams will only look at the applications you will allow them to. For their own applications they can only do what your policy defines.**
- All teams will have read access to the UI. Only developers that belong to the "superuser" group will be able to sync and delete applications

## What are the components that take part in a multi-tenant Argo CD installation?

- **✔️ SSO users, RBAC policies for actions, constraints on what clusters and Git repos are allowed.**
- Global RBAC policies, per project RBAC policies and autoscalers.
- SSO users, local users and custom ingresses
- Application Sets and AppProjects

## Argo Rollouts implements Progressive Delivery for:

- **✔️ Rollout objects (a superset of Deployments)**
- Deployments and StatefulSets
- Deployments and Configmaps
- Deployments, Configmaps and Secrets

## What is a major limitation of Argo Rollouts?

- **✔️ Argo Rollouts doesn't monitor or handle changes in Configmaps**
- Argo Rollouts always needs a traffic provider for its canary support
- Argo Rollouts does not deal with ReplicaSets
- Argo Rollouts doesn't work with Kustomize applications

## Argo Rollouts has built in support for scenarios where a developer:

- **✔️ Changes the container tag in a Rollout resource**
- Changes both the container tag in a Rollout resource and a parameter in a configmap
- rotates a Kubernetes Secret to a new value

## If you are trying to use Argo Rollouts with configmap changes, rollbacks will fail because:

- **✔️ Argo Rollouts doesn't keep the previous version of the configmap, it keeps only the previous version of the rollout**
- Argo Rollouts will create an endless loop with Argo CD rollbacks
- Argo Rollouts will not save the new version in Git
- Argo Rollouts doesn't support Helm applications

## You can use Kustomize ConfigMap generators with Argo Rollouts in order to:

- make Argo Rollouts work with Helm applications
- **✔️ make Argo Rollouts keep both the old and new version of a configmap**
- instruct Argo Rollouts how to handle Kustomize applications
- detect when a secret is compromised

## What is the purpose of the Rollout transformer (rollout-transform.yaml)?

- **✔️ It teaches Kustomize how to understand Rollout resources**
- it teaches Argo Rollouts how to deploy Kustomize applications
- It teaches Argo Rollouts how to detect changes in Kubernetes Secrets
- It teaches Kustomize how to create ConfigMap generators

## If you use ConfigMap generators with Argo Rollouts you need to remember:

- That this technique is only possible for Kustomize applications
- That you need a way to cleanup orphan Configmaps when the Rollout has been promoted
- **✔️ All of the above**

## Why Argo Rollout has issues with Progressive Delivery for stateful applications (queues and databases)?

- These kinds of network connections are not monitored or controlled by a traffic manager known to Argo Rollouts
- A second instance of the application that is launched as a canary will use by default the production queue/db. Most times developers want to avoid this scenario.
- The application doesn't know by default if it is part of a canary or not
- **✔️ All of the above**

## What is the recommended way to use a queue while a canary is active?

- **✔️ Use a separate queue for the canary so that canary messages can be handled differently than**
- Block the canary from having access to any queue
- Block all network access to the canary so that clients cannot connect to it
- Inform users in advance that when a canary is happening their application might have issues

## What is the Kubernetes Downward API?

- **✔️ A Kubernetes API that allows you to mount pod labels as normal files**
- An Argo Rollouts capability for defining custom metadata labels when a canary is active.
- A way to combine the Kubernetes Gateway API with Argo Rollouts
- A custom Argo Rollouts plugin for interfacing with Kubernetes volumes

## What are Argo Rollouts Ephemeral labels?

- **✔️ Temporary labels for Kubernetes resources that Argo Rollouts applies only when a canary/blue-green deployment takes place**
- Custom Kubernetes labels that notify Kubernetes pods when a secret is rotated
- Temporary labels that change the number of replicas while a canary is underway
- Custom labels applied to the Argo Rollouts controller for exposing different metrics while a canary is active

## You can use the Kubernetes Downward API and Argo Rollouts Ephemeral labels together:

- **✔️ so that the application knows when a canary is active and can change its configuration accordingly**
- so that you can scale canary traffic proportional to the number of canary pods that are ready
- so that Argo Rollouts automatically detects new versions of Stateful Sets.
- so that changes to configmaps trigger a new canary process

## How can you instruct a canary application to stop using the production queue and send messages to a preview queue when a canary has started?

- You should call special API manually in the application to make it aware of the production queue settings
- **✔️ You should make the application load the configuration of the queue from files and then use the Downward API and ephemeral labels so that while a canary is running a different queue can be defined**
- You should go to your DNS provider and manually update the queue URL to a different setting while the canary is running
- You should just use the production queue and hope that nothing goes wrong while a canary is running.

## What is the main advantage of using Argo Rollouts Ephemeral labels?

- **✔️ It makes your applications smarter as they know when a canary is happening and they can temporarily change their configuration**
- It allows you to use Argo Rollouts with Stateful Sets
- It makes the integration of Argo Rollouts and Argo CD very easy
- it allows you to get better metrics from the Argo Rollouts controller while a canary is underway

## Having your application read its configuration from files and reload it automatically:

- **✔️ Is a good practice to employ as it allows configuration changes without pod restarts (even when not using Argo Rollouts)**
- is a bad practice because all your applications should load their configuration from environment values instead
- is a practice that goes against the Twelve-Factor App principles
- is not possible anymore when your application runs in Kubernetes

## Before adopting Argo Rollouts for an application:

- you should talk with the developers of the application and explain to them how this application will be deployed
- you should do some research to understand all the external dependencies of the application including services such as databases and/or queues
- verify with developers that two instances of the application can indeed run at the same time without any conflicts
- **✔️ All of the above**

## The proper way to use Argo Rollouts for a frontend and a backend is:

- to deploy the backend first
- to deploy the frontend first
- deploy both of them together and hope for the best
- **✔️ make the new versions of both services backwards compatible with each other so that deployment order doesn't matter**

## An important requirement of using Argo Rollouts with both a frontend and backend application is:

- **✔️ that the location of the backend should be a configuration parameter in the frontend**
- that both applications should use the same programming framework
- that only the backend should use a database
- that both applications should have a shared database

## You need to use Argo Rollouts for two applications (frontend and backend). Your first question is:

- if the frontend is written in Nodejs and the backend in Python
- **✔️ if during a canary the frontend must also use canary version of the backend or not**
- if during a canary users see a different color theme in the frontend
- if you need to run smoke tests on the frontend or the backend first

## You decide to use Argo Rollouts for two applications (backend and frontend). The canary frontend must only talk with the canary backend:

- **✔️ You use Argo Rollouts Ephemeral labels to make the frontend smarter so that during the canary it connects to the preview backend (and not the stable one)**
- You setup nginx in front of the backend and manually redirect requests from the canary frontend to the canary backend. You remember to revert your changes when the canary has finished.
- You hack the /etc/hosts file in the canary pod of the frontend to make it connect to the canary backend.
- You tell management that what they are asking is not technically possible.

## Having your application read the URLs of external services as a configuration parameter:

- **✔️ Is a good practice to employ as it allows easy testing on non-production environments (even when not using Argo Rollouts)
- is a bad practice because hardcoded URLs are much better for security purposes**
- is a practice that goes against the Twelve-Factor App principles
- is not possible anymore when your application runs in Kubernetes

## If you want to use Progressive Delivery with multiple applications, Argo Rollouts:

- has built-in support for coordinating canary deployments to multiple applications at the same time
- offers the capability to create a dependency graph between all involved applications
- **✔️ only works with a single application so you need to manually orchestrate multi-service deployments**
- can automatically handle this scenario for blue/green deployments (but not canary deployments)
