## Gitlab runner on k8s
- Tình huống: Mục đích của việc chạy `gitlab-runner` trên k8s là bởi vì `runner` được register trên k8s, sẽ dùng để deploy các resource trên k8s mà không cần cung cấp file `kubeconfig` cho nó.
- Các bước làm:
  ## B1: Tạo service account
  `kubectl -n gitlab-runner create serviceaccount gitlab-runner`
  ## B2: Tạo ClusterRole
  
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  kind: ClusterRole
  metadata:
    name: gitlab-runner
  rules:
  - apiGroups:
    - '*'
    resources:
    - '*'
    verbs:
    - '*'
  ```
  ## B3: Tạo ClusterRoleBinding
  
  ```
  apiVersion: rbac.authorization.k8s.io/v1
  # This cluster role binding allows anyone in the "manager" group to read secrets in any namespace.
  kind: ClusterRoleBinding
  metadata:
    name: gitlab-runner
  subjects:
  - kind: ServiceAccount
    name: gitlab-runner
    namespace: gitlab-runner
  roleRef:
    kind: ClusterRole
    name: gitlab-runner
    apiGroup: rbac.authorization.k8s.io
  ```
  
  ## B4: Tạo gitlab-runner trên k8s
  
    - file `ci-lab.yaml`
  
  ```
  fullnameOverride: ci-lab

  gitlabUrl: https://git.devopsnd95.cf/

  runnerRegistrationToken: "jAT4uc4xzTzbkznwXD9h"
  #runnerToken: "aTC53ufsf57cNfmLSxvU"

  concurrent: 1
  ## For RBAC support:
  rbac:
    create: true

    ## Run the gitlab-bastion container with the ability to deploy/manage containers of jobs
    ## cluster-wide or only within namespace
    clusterWideAccess: true

    ## If RBAC is disabled in this Helm chart, use the following Kubernetes Service Account name.
    ##
    # serviceAccountName: default

  ## Configuration for the Pods that the runner launches for each new job
  ##
  runners:
    ## Default container image to use for builds when none is specified
    ##
    image: ubuntu:18.04

    ## Run all containers with the privileged flag enabled
    ## This will allow the docker:stable-dind image to run if you need to run Docker
    ## commands. Please read the docs before turning this on:
    ## ref: https://docs.gitlab.com/runner/executors/kubernetes.html#using-docker-dind
    ##
    privileged: true
    tags: ci-lab
    serviceAccountName: gitlab-runner

    ## Namespace to run Kubernetes jobs in (defaults to 'default')
    ##
    # namespace:

    ## Build Container specific configuration
    ##
    builds:
      # cpuLimit: 200m
      # memoryLimit: 256Mi
      cpuRequests: 100m
      memoryRequests: 128Mi
  ```
    - Tạo gitlab-runner:
    `helm install -f ci-lab.yaml --name gitlab-runner --namespace=gitlab-runner gitlab/gitlab-runner`
    
 ## Done
 - Lúc này bạn có thể viết gitlab-ci sử dụng runner có tag là `ci-lab` để cài đăt, deploy các reource trên k8s
 

