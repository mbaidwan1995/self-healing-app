# Kubernetes GitOps and monitoring case study

**Author:** Manjit Baidwan | **Scope:** Personal learning lab

I practised connecting Terraform-provisioned EKS infrastructure with Argo CD deployment management and Prometheus/Grafana monitoring. My project notes call this a self-healing cloud platform. The recorded work supports a GitOps and monitoring lab; an automated recovery experiment has not yet been documented here.

The base repository is forked from [devopsbyraham/self-healing-app](https://github.com/devopsbyraham/self-healing-app). Its application and template code retain upstream attribution. This document explains my lab work rather than claiming original authorship of that code.

## My recorded work

- Worked on EKS cluster creation through Terraform.
- Installed Argo CD using a Helm chart and patched its service to use a load balancer.
- Installed Prometheus and Grafana and worked with a Grafana dashboard.
- Updated a deployment file and pushed it to a repository.
- Created an Argo CD application and corrected its source directory.

These activities come from my project report. The report does not identify the exact commits for each configuration change.

## Architecture practised

~~~text
Git repository -> Argo CD -> Kubernetes workloads on EKS
                              |
                         Prometheus -> Grafana
Terraform -> AWS cluster infrastructure
~~~

The CI phase in my notes describes a goal: build an application, run tests, build a Docker image and push it to Amazon ECR. No CI run or ECR publication evidence was supplied, so those steps remain design goals in this case study.

## Troubleshooting Argo CD source configuration

**Problem:** The application source path was set to the repository root, represented by a dot.

**Correction recorded:** Changed the path to the manifests directory used in my lab repository.

**Why it matters:** Deployment tooling must read the directory containing the intended manifests. The correct path depends on the actual repository layout; this fork currently has apps, argocd, base, monitoring and network directories, so the path from my local exercise should not be copied blindly into every repository.

**Result recorded:** My notes state that the path error was solved. A final Argo CD Synced/Healthy screenshot or command output has not been attached.

## Verification and evidence still needed

- Link the deployment-file change and Argo CD source-path correction to their commits.
- Capture sanitized Argo CD sync and application-health results.
- Record Prometheus target status and the Grafana dashboard metrics used.
- In an isolated lab, document a controlled failure, observed replacement/recovery and elapsed time before claiming demonstrated self-healing.
- Preserve the CI log and image tag/digest before claiming a successful ECR publication.

No recovery time, uptime improvement or production availability result is claimed. Avoid publishing secrets, kubeconfig credentials or unredacted cloud account details.

## Relevant skills

Terraform, AWS EKS, Kubernetes, Helm, Argo CD, GitOps, Prometheus, Grafana and deployment troubleshooting.

[Professional profile](https://www.linkedin.com/in/manjit-baidwan-a6a477406/)
