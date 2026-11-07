# Contents

- [Part 1: Study guide](#part-1-study-guide)
    - [How to use this guide](#how-to-use-this-guide)
    - [Lab architecture](#lab-architecture)
    - [Modules](#modules)
        - [Phase 1: Foundations (language, OS, terminal, Git)](#phase-1-foundations-language-os-terminal-git)
        - [Phase 2: Networking, protocols and web servers](#phase-2-networking-protocols-and-web-servers)
        - [Phase 3: Containers, cloud and infrastructure as code](#phase-3-containers-cloud-and-infrastructure-as-code)
        - [Phase 4: CI/CD, artifacts and secrets](#phase-4-cicd-artifacts-and-secrets)
        - [Phase 5: Container orchestration and GitOps](#phase-5-container-orchestration-and-gitops)
        - [Phase 6: Monitoring, logs and observability](#phase-6-monitoring-logs-and-observability)
        - [Phase 7: Service mesh and cloud design patterns](#phase-7-service-mesh-and-cloud-design-patterns)
    - [Capstone projects](#capstone-projects)
    - [Progress tracker](#progress-tracker)
- [Part 2: Step-by-step runbooks](#part-2-step-by-step-runbooks)
    - [Before you start](#before-you-start)
    - [Placeholders](#placeholders)
    - [IP plan](#ip-plan)
    - [Phase 1 runbook: Foundations](#phase-1-runbook-foundations)
        - [Step 1: Make cloud-init templates](#step-1-make-cloud-init-templates)
        - [Step 2: Build the admin VM](#step-2-build-the-admin-vm)
        - [Step 3: Build an Ubuntu and a Rocky VM and do the same admin tasks on both](#step-3-build-an-ubuntu-and-a-rocky-vm-and-do-the-same-admin-tasks-on-both)
        - [Step 4: Run Gitea in an LXC container](#step-4-run-gitea-in-an-lxc-container)
        - [Step 5: Set up the lab repo](#step-5-set-up-the-lab-repo)
        - [Step 6: Write the Proxmox inventory script](#step-6-write-the-proxmox-inventory-script)
        - [Step 7: Break things and find them](#step-7-break-things-and-find-them)
    - [Phase 2 runbook: Networking and web servers](#phase-2-runbook-networking-and-web-servers)
        - [Step 1: Lab DNS with Unbound](#step-1-lab-dns-with-unbound)
        - [Step 2: Your own certificate authority with step-ca](#step-2-your-own-certificate-authority-with-step-ca)
        - [Step 3: Two backends](#step-3-two-backends)
        - [Step 4: Nginx load balancer](#step-4-nginx-load-balancer)
        - [Step 5: TLS from your CA with ACME](#step-5-tls-from-your-ca-with-acme)
        - [Step 6: Fail over, cache, and break the cert](#step-6-fail-over-cache-and-break-the-cert)
        - [Step 7: Squid forward proxy](#step-7-squid-forward-proxy)
        - [Step 8: Firewalls](#step-8-firewalls)
        - [Step 9: Harden SSH and add a jump host](#step-9-harden-ssh-and-add-a-jump-host)
    - [Phase 3 runbook: Containers and infrastructure as code](#phase-3-runbook-containers-and-infrastructure-as-code)
        - [Step 1: Containers with Docker, and a look at LXC](#step-1-containers-with-docker-and-a-look-at-lxc)
        - [Step 2: S3 storage for Terraform state (SeaweedFS)](#step-2-s3-storage-for-terraform-state-seaweedfs)
        - [Step 3: Terraform builds the VMs](#step-3-terraform-builds-the-vms)
        - [Step 4: Ansible configures them](#step-4-ansible-configures-them)
        - [Step 5: The one-command rebuild](#step-5-the-one-command-rebuild)
        - [Step 6 (stretch): The golden image as code with Packer](#step-6-stretch-the-golden-image-as-code-with-packer)
        - [Step 7: A taste of serverless (OpenFaaS)](#step-7-a-taste-of-serverless-openfaas)
    - [Phase 4 runbook: CI/CD, artifacts and secrets](#phase-4-runbook-cicd-artifacts-and-secrets)
        - [Step 1: Add the new VMs to Terraform](#step-1-add-the-new-vms-to-terraform)
        - [Step 2: Harbor registry](#step-2-harbor-registry)
        - [Step 3: Gitea Actions runner](#step-3-gitea-actions-runner)
        - [Step 4: The CI pipeline](#step-4-the-ci-pipeline)
        - [Step 5: The same pipeline in Jenkins](#step-5-the-same-pipeline-in-jenkins)
        - [Step 6: Vault](#step-6-vault)
        - [Step 7: SOPS and age for secrets in Git](#step-7-sops-and-age-for-secrets-in-git)
        - [Step 8: Terraform from the pipeline](#step-8-terraform-from-the-pipeline)
    - [Phase 5 runbook: Kubernetes and GitOps](#phase-5-runbook-kubernetes-and-gitops)
        - [Step 1: Add the cluster VMs to Terraform](#step-1-add-the-cluster-vms-to-terraform)
        - [Step 2: Install kubeadm and build the cluster](#step-2-install-kubeadm-and-build-the-cluster)
        - [Step 3: CKA drills on a single control plane](#step-3-cka-drills-on-a-single-control-plane)
        - [Step 4: Swap Flannel for Cilium, and prove NetworkPolicy works](#step-4-swap-flannel-for-cilium-and-prove-networkpolicy-works)
        - [Step 5: HA control plane behind the LB](#step-5-ha-control-plane-behind-the-lb)
        - [Step 6: Storage on the NAS](#step-6-storage-on-the-nas)
        - [Step 7: Argo CD and the app-of-apps](#step-7-argo-cd-and-the-app-of-apps)
        - [Step 8: Pods read secrets from Vault (External Secrets Operator)](#step-8-pods-read-secrets-from-vault-external-secrets-operator)
        - [Step 9: Flux on a throwaway cluster](#step-9-flux-on-a-throwaway-cluster)
        - [Step 10: The 30-minute rebuild](#step-10-the-30-minute-rebuild)
    - [Phase 6 runbook: Monitoring, logs and observability](#phase-6-runbook-monitoring-logs-and-observability)
        - [Step 1: Make room](#step-1-make-room)
        - [Step 2: kube-prometheus-stack](#step-2-kube-prometheus-stack)
        - [Step 3: Watch the VMs and the Proxmox host](#step-3-watch-the-vms-and-the-proxmox-host)
        - [Step 4: An app worth watching, and PromQL drills](#step-4-an-app-worth-watching-and-promql-drills)
        - [Step 5: Dashboards as code](#step-5-dashboards-as-code)
        - [Step 6: Alerts that reach you](#step-6-alerts-that-reach-you)
        - [Step 7: Logs with Loki and Alloy](#step-7-logs-with-loki-and-alloy)
        - [Step 8: Traces with OpenTelemetry and Jaeger](#step-8-traces-with-opentelemetry-and-jaeger)
    - [Phase 7 runbook: Service mesh and design patterns](#phase-7-runbook-service-mesh-and-design-patterns)
        - [Step 1: Linkerd](#step-1-linkerd)
        - [Step 2: Retries, timeouts and a canary](#step-2-retries-timeouts-and-a-canary)
        - [Step 3: SLOs and burn-rate alerts with Sloth](#step-3-slos-and-burn-rate-alerts-with-sloth)
        - [Step 4: Game days](#step-4-game-days)
        - [Step 5: Design patterns on your own stack](#step-5-design-patterns-on-your-own-stack)
        - [Step 6: Take it back to Azure](#step-6-take-it-back-to-azure)
- [Sources](#sources)

# Part 1: Study guide

## How to use this guide

Work the [roadmap.sh DevOps roadmap](https://roadmap.sh/devops) in 7 phases, each one built and broken on your Proxmox lab, about 3 to 5 evenings a phase. The roadmap lists 140 topics; this guide keeps the ones worth lab time and marks the rest *read only*.

- **Skim** what you already run at work: Kubernetes (8 years), Jenkins, Azure, Bash. Do the lab, skip the reading.
- **Go deep** on the gaps the roadmap expects and your skills list lacks: Terraform, Ansible, running Prometheus and Grafana yourself, Loki, Vault, GitOps, service mesh, OpenTelemetry, SLOs.
- **Read only**: other clouds (AWS, GCP, PaaS hosts), the BSDs, email protocols, Windows/IIS. Know what they are; don't build them.
- Each module ends with a *Done when* check. Snapshot the VM before every exercise so a broken lab costs one rollback.

The lab work also feeds your open certs: Phase 5 is CKA practice, and Phases 3 and 4 cover the pipeline, IaC and secrets domains of AZ-400.

**How this differs from the chart (checked against the live page 2026-11-06).** The phases follow lab dependencies, not the chart. That moves two things. The chart puts containers before networking and web servers. It puts monitoring, logs and artifact management after CI/CD but before Kubernetes. The guide builds Kubernetes first so that monitoring can be deployed onto it through Argo CD. Where the chart marks a recommended pick, this guide uses it or says why not: Terraform, Ansible, Docker, Kubernetes, Argo CD, Prometheus, Grafana and Azure match. The chart recommends CircleCI and Artifactory; the guide swaps in Gitea Actions and Harbor or Nexus, because they self-host free on Proxmox. Topic links come from the roadmap's open-source repo.


## Lab architecture

By the end of Phase 5, your one Proxmox host runs a small copy of a real platform. Gitea holds the code for everything else, so any VM can be destroyed and rebuilt.

![Target lab layout: one Proxmox host, four tiers](diagram.png)

Argo CD in the cluster pulls its manifests from Gitea. DNS and the internal CA serve every box.

**Resource budget.** Your 3 nodes at 2 CPU / 4 GB each are enough for Phases 1 to 5. Phase 6 (Prometheus, Loki, Grafana) and Phase 7 (a service mesh) need more. Before then, raise workers to 8 GB or add a fourth node from the golden image. Plan on about 10 to 12 GB more for the platform VMs: Harbor about 4 GB, Vault about 1 GB per node, a 2 GB CI runner, a 1 GB load balancer. The LXCs need under 512 MB each.

**Snapshot rules.** Take a named snapshot before each phase (for example `pre-phase3`) and before any exercise marked "break". Keep your clean-state cluster snapshot untouched as the reset point.

**Open question:** how much CPU, RAM and disk does the Proxmox host have? That decides whether Phases 6 and 7 fit at the same time or need to take turns.


## Modules

Seven phases, in roadmap order. Each one leaves something running that the next phase builds on.

Step-by-step commands for each phase are in Part 2.

### Phase 1: Foundations (language, OS, terminal, Git)

**Roadmap topics:** Learn a programming language (Python, Go) · Operating system (Ubuntu/Debian, RHEL derivatives) · Terminal knowledge (Bash, text manipulation, process and performance monitoring, networking tools, editors) · Version control (Git) and VCS hosting.

**Your angle:** You can skim the Bash and Linux topics. Spend the time on Python or Go, since the roadmap asks for one real language and your list has Bash only.

**Lab exercises**

1. Clone two VMs from your golden image: one Ubuntu LTS, one Rocky Linux (the RHEL side). Do the same admin tasks on both: users, sudo, systemd units, package installs, `journalctl`.
2. Run Gitea in a Proxmox LXC container. It is your lab's GitHub for the rest of the guide, and every config you write from here on gets committed to it.
3. Write a Python (or Go) CLI that calls the Proxmox API and lists VMs with their CPU, RAM and state. Commit it to Gitea.
4. Break a VM on purpose: fill the disk, run a CPU hog, leak a port. Find each one with `df`, `top`/`htop`, `ss`, `lsof` and `vmstat`.

**Done when:** your Proxmox inventory script runs from a fresh clone of the Gitea repo, and you can find a runaway process in under 2 minutes.

**Free resources:** [A Tour of Go](https://go.dev/tour/welcome/1) · [Go by Example](https://gobyexample.com/) · [Python Crash Course resources](https://ehmatthes.github.io/pcc_3e/) · [Linux text processing commands](https://earthly.dev/blog/linux-text-processing-commands/) · [Git by Example](https://antonz.org/git-by-example/) · [Proxmox VE API](https://pve.proxmox.com/wiki/Proxmox_VE_API)

### Phase 2: Networking, protocols and web servers

**Roadmap topics:** Networking and protocols (OSI model, DNS, HTTP, HTTPS, SSL/TLS, SSH, FTP/SFTP; email protocols read only) · Web servers (Nginx; Apache, Caddy, Tomcat, IIS read only) · Forward proxy, reverse proxy, caching server, load balancer, firewall.

**Your angle:** You know Cloudflare and Application Gateway from the managed side. Here you build each one by hand, so you can see what those services hide.

**Lab exercises**

1. Stand up lab DNS (Unbound or BIND in an LXC) with a private zone such as `lab.internal`. Point every VM at it and give each one a name.
2. Create a small internal CA with `step-ca` or `openssl`. Issue certs and trust the root on your VMs. Then break a cert (expired, wrong SAN) and read the `curl -v` and `openssl s_client` output.
3. Put two web VMs behind an Nginx reverse proxy that terminates TLS and load-balances them. Kill one backend and watch traffic fail over.
4. Add Nginx response caching, then a Squid forward proxy that a test VM must use to reach the internet.
5. Lock it down with the Proxmox firewall plus `nftables` or `ufw` on the hosts. Prove with `nmap` that only 22 and 443 are open.
6. Harden SSH: keys only, no root login, a jump host for the lab subnet.

**Done when:** `https://app.lab.internal` loads with a trusted cert through the load balancer while one backend is down.

**Free resources:** [How DNS Works (comic)](https://howdns.works/) · [Cloudflare: What is TLS?](https://www.cloudflare.com/en-gb/learning/ssl/transport-layer-security-tls/) · [Cloudflare: Reverse proxy](https://www.cloudflare.com/en-gb/learning/cdn/glossary/reverse-proxy/) · [Cloudflare: Load balancing](https://www.cloudflare.com/en-gb/learning/performance/what-is-load-balancing/) · [Nginx docs](https://nginx.org/) · [How SSH works (video)](https://www.youtube.com/watch?v=5JvLV2-ngCI)

### Phase 3: Containers, cloud and infrastructure as code

**Roadmap topics:** Containers (Docker, LXC) · Cloud providers and serverless (Azure is your home; AWS, GCP and PaaS hosts read only) · Provisioning (Terraform, Pulumi; CloudFormation and CDK read only) · Configuration management (Ansible; Chef, Puppet, Salt read only).

**Your angle:** This is the biggest gap. The roadmap treats Terraform and Ansible as core, and you've only written Bicep. Proxmox is a good target for both, because each has a mature Proxmox integration.

**Lab exercises**

1. Containers: write a multi-stage Dockerfile for your Phase 1 CLI. Make it run as non-root and get the image under 50 MB. Compare that with running the same thing in a Proxmox LXC, and note what differs in isolation, kernel and startup.
2. Terraform: use the `bpg/proxmox` provider to clone your golden image into VMs, with cloud-init for hostname, IP and SSH keys. Keep state in a remote backend (SeaweedFS S3 on the NAS, since MinIO's free edition is no longer maintained). Then `terraform destroy` and rebuild until it is boring.
3. Ansible: write roles for the work you did by hand in Phases 1 and 2 (users, SSH hardening, Nginx, certs, firewall). Use a dynamic inventory from Proxmox. Prove idempotence: a second run reports zero changes.
4. Golden image as code: rebuild the golden image with Packer plus your Ansible roles, so the image is reproducible and not hand-made.
5. Serverless taste: run OpenFaaS or Knative on the cluster and deploy one function. Map it to what you know from Azure Functions.
6. Optional: redo exercise 2 in Pulumi with Python, to see IaC written in a general-purpose language.

**Done when:** one command (`terraform apply && ansible-playbook site.yml`) takes you from an empty Proxmox to the Phase 2 web stack.

**Free resources:** [DevOps with Docker (Univ. of Helsinki)](https://courses.mooc.fi/org/uh-cs/courses/devops-with-docker) · [Docker docs](https://docs.docker.com/) · [Complete Terraform Course (video)](https://www.youtube.com/watch?v=7xngnjfIlK4) · [Terraform docs](https://www.terraform.io/docs) · [bpg/proxmox provider](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) · [Ansible Full Course (video)](https://www.youtube.com/watch?v=9Ua2b06oAr4) · [Pulumi](https://www.pulumi.com/)

### Phase 4: CI/CD, artifacts and secrets

**Roadmap topics:** CI/CD tools (GitHub Actions, GitLab CI, Jenkins; CircleCI, TeamCity, Octopus read only) · Artifact management (Nexus, Artifactory, Cloudsmith) · Secret management (Vault, SOPS, Sealed Secrets, External Secrets Operator; cloud-specific tools).

**Your angle:** You've migrated Jenkins at work, so skim that part. The new ground is running your own runners and registry, and doing secrets without Key Vault.

**Lab exercises**

1. Turn on Gitea Actions (it uses GitHub Actions syntax) with a self-hosted runner VM. Build the pipeline: lint, test, build image, scan with Trivy, push.
2. Run the same pipeline in Jenkins as a declarative `Jenkinsfile` with agents on Kubernetes. Note where each tool hurts.
3. Run a registry: Harbor (images plus scanning) or Nexus (images plus PyPI/npm proxy). Make CI push there and the cluster pull from there.
4. Run Vault in dev mode first, then as a 3-node Raft cluster. Use KV v2, dynamic database credentials and short-lived SSH certs. Have CI read secrets through AppRole, so no secret sits in Gitea.
5. Encrypt a values file with SOPS plus age and commit it. Decrypt it in CI.
6. Run Terraform from the pipeline (plan on PR, apply on merge), with Proxmox API tokens pulled from Vault.

**Done when:** a merge to `main` builds, scans and pushes a tagged image to your registry, with no plain-text secret anywhere in Git.

**Free resources:** [GitHub Actions docs](https://docs.github.com/en/actions) · [Jenkins pipeline tour](https://www.jenkins.io/doc/pipeline/tour/getting-started/) · [Using Nexus Repository](https://help.sonatype.com/en/using-nexus-repository.html) · [HashiCorp Vault](https://www.vaultproject.io/) · [SOPS](https://getsops.io) · [CI/CD secret exposure exercise](https://ransomleak.com/exercises/cicd-secret-exposure/)

### Phase 5: Container orchestration and GitOps

**Roadmap topics:** Container orchestration (Kubernetes; GKE/EKS/AKS, ECS/Fargate, Docker Swarm, OpenShift read only) · GitOps (Argo CD, Flux CD).

**Your angle:** After 8 years of running Kubernetes, the value here isn't using it. It's building and repairing it from scratch, which is exactly what CKA tests. Treat this phase as CKA practice.

**Lab exercises**

1. Rebuild the cluster with `kubeadm`, using your Phase 3 Terraform and Ansible: 1 control plane and 2 workers, then a 3-node HA control plane behind your Phase 2 load balancer. Time each rebuild.
2. CKA drills on the live cluster: back up and restore etcd, upgrade with `kubeadm upgrade` one minor version, drain and cordon, then fix a broken kubelet and a broken CNI.
3. Swap the CNI (Flannel to Calico or Cilium) and write NetworkPolicies that isolate a namespace.
4. Storage: an NFS CSI driver backed by the NAS VM, a StorageClass, a StatefulSet with PVCs. Kill a node and watch the pod reschedule.
5. Install Argo CD and point it at a Gitea repo (app-of-apps). From here on, every cluster add-on in this guide goes in through Git, never through `kubectl apply`.
6. Install External Secrets Operator so pods read from your Phase 4 Vault. Try Flux on a second, throwaway cluster from your clean-state snapshot and compare it with Argo CD.

**Done when:** you can destroy the cluster and get it back, apps included, from Terraform, Ansible and Argo CD in under 30 minutes, and you've passed a full CKA practice exam on it.

**Free resources:** [Kubernetes docs](https://kubernetes.io/) · [roadmap.sh Kubernetes roadmap](https://roadmap.sh/kubernetes) · [Argo CD docs](https://argo-cd.readthedocs.io/en/stable/) · [What is GitOps](https://octopus.com/devops/gitops/) · [External Secrets Operator](https://external-secrets.io/latest/) · [Sealed Secrets](https://github.com/bitnami-labs/sealed-secrets)

### Phase 6: Monitoring, logs and observability

**Roadmap topics:** Infrastructure monitoring (Prometheus, Grafana, Zabbix; Datadog read only) · Logs management (Loki, Elastic Stack, Graylog; Splunk and Papertrail read only) · Observability and application monitoring (OpenTelemetry, Jaeger; New Relic, Dynatrace and Datadog read only).

**Your angle:** You've been near Prometheus and Grafana but have never run them. This phase makes them skills you can claim. It's also the open-source version of the centralized observability platform you're pitching at work.

**Lab exercises**

1. Deploy kube-prometheus-stack through Argo CD. Add node\_exporter on the Proxmox host and on non-cluster VMs, plus the Proxmox VE exporter.
2. Learn PromQL properly: CPU saturation, memory pressure, `rate()` against `irate()`, and the 4 golden signals for the Phase 2 Nginx stack. Build one Grafana dashboard per layer (host, cluster, app), saved as JSON in Git.
3. Alerting: write Alertmanager rules for node down, disk 85% full and a cert expiring in 14 days. Route them to a test channel. Fire each one on purpose.
4. Logs: run Loki plus Grafana Alloy (or Promtail) to ship pod and VM logs. Write LogQL that finds the Phase 1 "runaway process" incident from its logs alone.
5. Traces: add OpenTelemetry to a small Python service. Send traces through an OTel Collector to Jaeger (or Tempo) and link traces to logs in Grafana.
6. Optional: index the same logs in a single-node Elastic or OpenSearch and compare its cost in RAM with Loki's.

**Done when:** you can break something in the lab, get an alert, and trace it from metric to log to span without SSHing to a box.

**Free resources:** [Prometheus getting started](https://prometheus.io/docs/tutorials/getting_started/) · [Prometheus and Grafana tutorial (video)](https://www.youtube.com/watch?v=9TJx7QTrTyo) · [Loki docs](https://grafana.com/docs/loki/latest/) · [OpenTelemetry docs](https://opentelemetry.io/docs/) · [Jaeger docs](https://www.jaegertracing.io/docs/latest) · [4 golden signals (video)](https://www.youtube.com/watch?v=PHcnmTdVPT0)

### Phase 7: Service mesh and cloud design patterns

**Roadmap topics:** Service mesh (Istio, Linkerd, Consul, Envoy) · Cloud design patterns (availability, data management, design and implementation, management and monitoring).

**Your angle:** You own availability and incident response, but not SLOs as a named practice. This phase gives your existing work that vocabulary, and the evidence to go with it.

**Lab exercises**

1. Install Linkerd first (it's light enough for 4 GB nodes) and get automatic mTLS, golden metrics and a canary traffic split. Then try Istio on a bigger or throwaway cluster and compare their footprint and how hard each is to run.
2. Write SLOs for your Phase 2 app (for example, 99.5% of requests under 300 ms over 28 days). Build the SLI and the error-budget burn-rate alerts in Prometheus, using Sloth or Pyrra to generate the rules.
3. Game day: kill a worker, cut the NAS VM off the network, fill a disk on the control plane. Record time to detect and time to recover, and write a short postmortem for each.
4. Use the patterns on your own stack: retries and circuit breakers in the mesh, health endpoints, queue-based load leveling (with a small RabbitMQ or NATS), and backup and restore with Velero to SeaweedFS.
5. Take the patterns back to Azure: map each one to what you run on 30+ subscriptions at work.

**Done when:** your app has a published SLO, burn-rate alerts that fired during the game day, and 3 postmortems in Gitea.

**Free resources:** [Linkerd docs](https://linkerd.io/) · [Istio and service mesh explained (video)](https://www.youtube.com/watch?v=16fgzklcF7Y) · [SLIs, SLOs, SLAs (video)](https://www.youtube.com/watch?v=tEylFyxbDLE) · [Azure data management patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/data-management) · [Google SRE book, free online](https://sre.google/sre-book/table-of-contents/)


## Capstone projects

Three builds that tie the phases together. Each one is a portfolio repo you can link from your resume or themorsecode.com.

1. **Lab from zero (Phases 1 to 5).** One repo, one README, one command: Terraform provisions VMs on Proxmox, Ansible builds a kubeadm cluster, and Argo CD installs every add-on. Show the rebuild time in the README.
2. **Commit to production with guardrails (Phases 3 to 6).** A sample app goes through Gitea Actions with tests, a Trivy scan and a signed image (cosign) to Harbor. Argo CD rolls it out as a Linkerd canary and rolls back on its own if the error rate climbs.
3. **Observability platform in a box (Phases 6 and 7).** Prometheus, Loki, Tempo or Jaeger, and Grafana, with SLO dashboards and burn-rate alerts, all installed from Git. It's an open-source counterpart to your Azure observability proposal, and worth a short write-up comparing the two.


## Progress tracker

Pick a status as you go. *Depth* is how hard to push each roadmap area given what you already run at work.

| Roadmap area | Phase | Depth | Status |
| --- | --- | --- | --- |
| Learn a programming language (Python or Go) | 1 | Deep | Not started |
| Operating system (Ubuntu, RHEL derivatives) | 1 | Skim | Not started |
| Terminal knowledge | 1 | Skim | Not started |
| Version control and VCS hosting | 1 | Skim | Not started |
| Networking and protocols | 2 | Deep | Not started |
| Web servers, proxies, load balancer, firewall | 2 | Deep | Not started |
| Containers (Docker, LXC) | 3 | Skim | Not started |
| Cloud providers | 3 | Read only beyond Azure | Not started |
| Serverless | 3 | Skim | Not started |
| Provisioning (Terraform) | 3 | Deep | Not started |
| Configuration management (Ansible) | 3 | Deep | Not started |
| CI/CD tools | 4 | Skim | Not started |
| Artifact management | 4 | Deep | Not started |
| Secret management | 4 | Deep | Not started |
| Container orchestration (Kubernetes, CKA) | 5 | Deep | Not started |
| GitOps | 5 | Deep | Not started |
| Infrastructure monitoring | 6 | Deep | Not started |
| Logs management | 6 | Deep | Not started |
| Observability and tracing | 6 | Deep | Not started |
| Service mesh | 7 | Deep | Not started |
| Cloud design patterns and SLOs | 7 | Deep | Not started |
| Capstone 1: Lab from zero | 1-5 | Build | Not started |
| Capstone 2: Commit to production | 3-6 | Build | Not started |
| Capstone 3: Observability platform | 6-7 | Build | Not started |


# Part 2: Step-by-step runbooks

One sub-tab per phase. Work them in order: each phase leaves running what the next one needs. Every command assumes the placeholders and IP plan below, so set those once and swap in your real values.

## Before you start

1. Snapshot the Proxmox host's config (`/etc/pve`) and your clean-state cluster nodes.
2. Fill in the placeholder table with your real values, then search-and-replace as you copy commands.
3. Keep a terminal log: `script -a ~/lab-$(date +%F).log` on your admin VM records everything you type.

## Placeholders

| Placeholder | Meaning | Example |
| --- | --- | --- |
| `<PVE_HOST>` | Proxmox host IP | 192.168.1.10 |
| `<NODE>` | Proxmox node name | pve |
| `<TEMPLATE_ID>` | VM ID of your golden image, converted to a template | 9000 |
| `<STORAGE>` | Proxmox storage for VM disks | local-lvm |
| `<BRIDGE>` | Proxmox network bridge | vmbr0 |
| `<GW>` | LAN gateway | 192.168.1.1 |
| `<NAS_IP>` | Your existing NAS VM | 192.168.1.15 |
| `lab.internal` | Private DNS zone for the lab | lab.internal |

## IP plan

| Host | IP (example) | Built in |
| --- | --- | --- |
| admin (your workstation VM) | .19 | Phase 1 |
| dns | .20 | Phase 2 |
| gitea | .21 | Phase 1 |
| squid | .22 | Phase 2 |
| lb (Nginx) | .30 | Phase 2 |
| web1, web2 | .31, .32 | Phase 2 |
| runner | .40 | Phase 4 |
| harbor | .41 | Phase 4 |
| vault1 to vault3 | .42 to .44 | Phase 4 |
| k8s cp1 to cp3 | .50 to .52 | Phase 5 |
| k8s w1 to w3 | .53 to .55 | Phase 5 |

Use your own subnet. Reserve these addresses in your router's DHCP so nothing else takes them.


## Phase 1 runbook: Foundations

By the end you have an admin VM, an Ubuntu and a Rocky VM built from templates, Gitea running in an LXC, and a Python script in Gitea that lists your Proxmox VMs. Run Proxmox commands as root in the host shell (Datacenter > your node > Shell, or SSH to `<PVE_HOST>`).

### Step 1: Make cloud-init templates

Cloud-init lets every clone get its own hostname, IP and SSH key at first boot. If your golden image already has cloud-init and `qemu-guest-agent`, just make sure it has a cloud-init drive and is a template:

```bash
qm set <TEMPLATE_ID> --ide2 <STORAGE>:cloudinit --agent enabled=1
qm template <TEMPLATE_ID>
```

If it doesn't, build fresh templates from the official cloud images. Ubuntu 24.04 as VM 9000:

```bash
cd /var/lib/vz/template/iso
wget https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img
qm create 9000 --name ubuntu-2404-tpl --memory 2048 --cores 2 \
  --net0 virtio,bridge=<BRIDGE> --scsihw virtio-scsi-pci
qm set 9000 --scsi0 <STORAGE>:0,import-from=/var/lib/vz/template/iso/noble-server-cloudimg-amd64.img
qm set 9000 --ide2 <STORAGE>:cloudinit --boot order=scsi0 \
  --serial0 socket --vga serial0 --agent enabled=1
qm template 9000
```

Rocky Linux 9 as VM 9001 (the RHEL side of the roadmap):

```bash
wget https://dl.rockylinux.org/pub/rocky/9/images/x86_64/Rocky-9-GenericCloud-Base.latest.x86_64.qcow2
qm create 9001 --name rocky-9-tpl --memory 2048 --cores 2 \
  --net0 virtio,bridge=<BRIDGE> --scsihw virtio-scsi-pci --cpu host
qm set 9001 --scsi0 <STORAGE>:0,import-from=/var/lib/vz/template/iso/Rocky-9-GenericCloud-Base.latest.x86_64.qcow2
qm set 9001 --ide2 <STORAGE>:cloudinit --boot order=scsi0 \
  --serial0 socket --vga serial0 --agent enabled=1
qm template 9001
```

Rocky 9 needs `--cpu host` (or x86-64-v2) or it may not boot.

### Step 2: Build the admin VM

This is where you run every CLI tool for the rest of the guide (git, terraform, ansible, kubectl).

```bash
# on the Proxmox host; paste your workstation's public key into ~/admin.pub first
qm clone 9000 119 --name admin --full
qm set 119 --ciuser jason --sshkeys ~/admin.pub \
  --ipconfig0 ip=192.168.1.19/24,gw=<GW> --nameserver <GW>
qm resize 119 scsi0 +28G
qm start 119
```

Then from your workstation:

```bash
ssh jason@192.168.1.19
sudo apt update && sudo apt install -y git python3-venv jq htop ncdu stress-ng tmux
ssh-keygen -t ed25519 -C admin@lab   # this key goes into Gitea in Step 5
```

### Step 3: Build an Ubuntu and a Rocky VM and do the same admin tasks on both

```bash
# on the Proxmox host
qm clone 9000 131 --name ubu1 --full
qm set 131 --ciuser jason --sshkeys ~/admin.pub --ipconfig0 ip=192.168.1.31/24,gw=<GW>
qm clone 9001 132 --name rocky1 --full
qm set 132 --ciuser jason --sshkeys ~/admin.pub --ipconfig0 ip=192.168.1.32/24,gw=<GW>
qm start 131 && qm start 132
qm snapshot 131 clean && qm snapshot 132 clean
```

These two VMs use .31 and .32, so they become web1 and web2 in Phase 2. On **each** VM, do these tasks and note how they differ (apt against dnf, ufw against firewalld, `/etc/sudoers.d` on both):

1. Create a user and give it passwordless sudo.

    ```bash
    sudo useradd -m -s /bin/bash ops
    echo 'ops ALL=(ALL) NOPASSWD:ALL' | sudo tee /etc/sudoers.d/ops
    sudo visudo -cf /etc/sudoers.d/ops
    ```
2. Install a package with the native tool: `sudo apt install -y nginx` on Ubuntu, `sudo dnf install -y nginx` on Rocky.
3. Write your own systemd service and timer that logs disk usage every 5 minutes.

    ```bash
    sudo tee /etc/systemd/system/diskreport.service <<'EOF'
    [Unit]
    Description=Log disk usage
    [Service]
    Type=oneshot
    ExecStart=/usr/bin/bash -c 'df -h / | logger -t diskreport'
    EOF
    sudo tee /etc/systemd/system/diskreport.timer <<'EOF'
    [Unit]
    Description=Run diskreport every 5 minutes
    [Timer]
    OnBootSec=1min
    OnUnitActiveSec=5min
    [Install]
    WantedBy=timers.target
    EOF
    sudo systemctl daemon-reload
    sudo systemctl enable --now diskreport.timer
    ```
4. Read its output: `journalctl -t diskreport --since '15 min ago'` and `systemctl list-timers`.
5. Rocky only: check that SELinux is enforcing with `getenforce`, then see what it blocks: `sudo ausearch -m avc -ts recent`.

### Step 4: Run Gitea in an LXC container

On the Proxmox host, get a Debian template and create the container:

```bash
pveam update
pveam available --section system | grep debian   # pick the newest debian-1x-standard
pveam download local <debian-template-file>
pct create 121 local:vztmpl/<debian-template-file> --hostname gitea \
  --cores 2 --memory 1024 --rootfs <STORAGE>:16 --unprivileged 1 --features nesting=1 \
  --net0 name=eth0,bridge=<BRIDGE>,ip=192.168.1.21/24,gw=<GW> \
  --ssh-public-keys ~/admin.pub --onboot 1
pct start 121
pct enter 121
```

Inside the container, install Gitea as a systemd service. Set `GITEA_VERSION` to the newest release listed at [dl.gitea.com/gitea](https://dl.gitea.com/gitea/):

```bash
apt update && apt install -y git curl
GITEA_VERSION=<latest, e.g. 1.24.x>
adduser --system --shell /bin/bash --group --disabled-password --home /home/git git
mkdir -p /var/lib/gitea/{custom,data,log} /etc/gitea
chown -R git:git /var/lib/gitea && chmod -R 750 /var/lib/gitea
chown root:git /etc/gitea && chmod 770 /etc/gitea
curl -fsSL -o /usr/local/bin/gitea \
  https://dl.gitea.com/gitea/${GITEA_VERSION}/gitea-${GITEA_VERSION}-linux-amd64
chmod +x /usr/local/bin/gitea

cat >/etc/systemd/system/gitea.service <<'EOF'
[Unit]
Description=Gitea
After=network.target
[Service]
User=git
Group=git
WorkingDirectory=/var/lib/gitea/
ExecStart=/usr/local/bin/gitea web --config /etc/gitea/app.ini
Restart=always
Environment=USER=git HOME=/home/git GITEA_WORK_DIR=/var/lib/gitea
[Install]
WantedBy=multi-user.target
EOF
systemctl daemon-reload && systemctl enable --now gitea
```

Open `http://192.168.1.21:3000`. In the installer, choose SQLite, set the server domain to `192.168.1.21` (you'll switch it to `gitea.lab.internal` in Phase 2), and create your admin account. Then lock the config back down:

```bash
chmod 750 /etc/gitea && chmod 640 /etc/gitea/app.ini
```

### Step 5: Set up the lab repo

1. In Gitea, add the admin VM's public key (`cat ~/.ssh/id_ed25519.pub`) under Settings > SSH / GPG Keys.
2. Create a repo named `homelab`. It holds everything you build in this guide, with one folder per phase.
3. On the admin VM:

    ```bash
    git config --global user.name "Jason"
    git config --global user.email "<your email>"
    git clone git@192.168.1.21:jason/homelab.git && cd homelab
    mkdir -p phase1 phase2 phase3 phase4 phase5 phase6 phase7
    printf '.env\n.venv/\n*.tfstate*\n.terraform/\n' > .gitignore
    ```

### Step 6: Write the Proxmox inventory script

First create a read-only API token on the Proxmox host:

```bash
pveum user add automation@pve
pveum aclmod / -user automation@pve -role PVEAuditor
pveum user token add automation@pve inventory --privsep 0
```

Copy the token secret; Proxmox shows it only once. On the admin VM:

```bash
cd ~/homelab/phase1
python3 -m venv .venv && source .venv/bin/activate
pip install proxmoxer requests && pip freeze > requirements.txt
printf 'PVE_HOST=<PVE_HOST>\nPVE_TOKEN=<token secret>\n' > .env
```

Save this as `pve_inventory.py`:

```python
#!/usr/bin/env python3
"""List every VM and container on the Proxmox host."""
import os
from proxmoxer import ProxmoxAPI

pve = ProxmoxAPI(
    os.environ["PVE_HOST"],
    user="automation@pve",
    token_name="inventory",
    token_value=os.environ["PVE_TOKEN"],
    verify_ssl=False,  # self-signed for now; Phase 2 gives you a trusted CA
)

print(f"{'VMID':>5}  {'NAME':<20} {'TYPE':<5} {'STATUS':<8} {'CPU':>3} {'MEM GB':>6}")
for r in sorted(pve.cluster.resources.get(type="vm"), key=lambda r: r["vmid"]):
    print(f"{r['vmid']:>5}  {r['name']:<20} {r['type']:<5} {r['status']:<8} "
          f"{r['maxcpu']:>3} {r['maxmem'] / 2**30:>6.1f}")
```

Run it, then commit:

```bash
set -a && source .env && set +a
python pve_inventory.py
cd .. && git add . && git commit -m "Phase 1: Proxmox inventory script" && git push
```

Stretch goals: add `argparse` with `--json` and `--running-only` flags, and add one test with `pytest`. Doing the same in Go (with `net/http` and `encoding/json`) is a good way to learn Go.

### Step 7: Break things and find them

Work on `ubu1`, and roll back after each drill with `qm rollback 131 clean` on the host. Better still, write `chaos.sh` to pick one drill at random so you don't know which you're hunting.

| Break it | Find it |
| --- | --- |
| `fallocate -l 5G /var/tmp/big.bin` | `df -h`, then `sudo du -xh / --max-depth=2 \| sort -h \| tail`, or `ncdu /` |
| `stress-ng --cpu 2 --timeout 600 &` | `top` (press P), `ps -eo pid,comm,%cpu --sort=-%cpu \| head` |
| `stress-ng --vm 1 --vm-bytes 75% --timeout 300 &` | `free -h`, `vmstat 1`, `top` (press M) |
| `python3 -m http.server 8099 &` | `ss -tlnp`, `sudo lsof -i :8099` |
| `exec 3>/var/tmp/ghost.log; yes > /var/tmp/ghost.log & rm /var/tmp/ghost.log` | `df` says full but `du` doesn't: `sudo lsof +L1` |
| `sudo systemctl stop ssh`, then try to SSH in | Proxmox console, then `systemctl status ssh` and `journalctl -u ssh` |

### Done when

- [ ] Both templates (9000, 9001) clone and boot with your SSH key
- [ ] The diskreport timer runs on Ubuntu and Rocky
- [ ] Gitea runs on boot and the `homelab` repo has the Phase 1 code
- [ ] `pve_inventory.py` works from a fresh `git clone`
- [ ] You can find each drill's cause in under 2 minutes

## Phase 2 runbook: Networking and web servers

By the end, `https://app.lab.internal` is served with a cert from your own CA, through an Nginx load balancer in front of web1 (Ubuntu, .31) and web2 (Rocky, .32) from Phase 1. Copy every config file you write into `homelab/phase2/` and commit it as you go.

### Step 1: Lab DNS with Unbound

On the Proxmox host, create the LXC (same Debian template as Gitea):

```bash
pct create 120 local:vztmpl/<debian-template-file> --hostname dns \
  --cores 1 --memory 512 --rootfs <STORAGE>:8 --unprivileged 1 \
  --net0 name=eth0,bridge=<BRIDGE>,ip=192.168.1.20/24,gw=<GW> \
  --ssh-public-keys ~/admin.pub --onboot 1
pct start 120 && pct enter 120
apt update && apt install -y unbound dnsutils
```

Create `/etc/unbound/unbound.conf.d/lab.conf`:

```
server:
  interface: 0.0.0.0
  access-control: 127.0.0.0/8 allow
  access-control: 192.168.1.0/24 allow
  local-zone: "lab.internal." static
  local-data: "pve.lab.internal.    A 192.168.1.10"
  local-data: "nas.lab.internal.    A <NAS_IP>"
  local-data: "admin.lab.internal.  A 192.168.1.19"
  local-data: "dns.lab.internal.    A 192.168.1.20"
  local-data: "ca.lab.internal.     A 192.168.1.20"
  local-data: "gitea.lab.internal.  A 192.168.1.30"   # served through the LB, Step 8
  local-data: "git-ssh.lab.internal. A 192.168.1.21"
  local-data: "squid.lab.internal.  A 192.168.1.22"
  local-data: "lb.lab.internal.     A 192.168.1.30"
  local-data: "app.lab.internal.    A 192.168.1.30"
  local-data: "web1.lab.internal.   A 192.168.1.31"
  local-data: "web2.lab.internal.   A 192.168.1.32"
  local-data-ptr: "192.168.1.31 web1.lab.internal"
  local-data-ptr: "192.168.1.32 web2.lab.internal"

forward-zone:
  name: "."
  forward-addr: 1.1.1.1
  forward-addr: 9.9.9.9
```

Check and start it, then test from the admin VM:

```bash
unbound-checkconf && systemctl restart unbound
# from admin:
dig @192.168.1.20 web1.lab.internal +short
dig @192.168.1.20 -x 192.168.1.31 +short
dig @192.168.1.20 github.com +short
```

Point every machine at it. On the Proxmox host, for each VM and container:

```bash
qm set <vmid> --nameserver 192.168.1.20 --searchdomain lab.internal   # then reboot the VM
pct set <ctid> --nameserver 192.168.1.20 --searchdomain lab.internal  # then pct reboot <ctid>
```

Cloud-init applies the new DNS on the next boot. Check with `resolvectl status` on Ubuntu or `cat /etc/resolv.conf` on Rocky.

### Step 2: Your own certificate authority with step-ca

Run the CA on the dns container (it already answers to `ca.lab.internal`):

```bash
apt install -y curl
curl -fsSLO https://dl.smallstep.com/cli/docs-ca-install/latest/step-cli_amd64.deb
curl -fsSLO https://dl.smallstep.com/certificates/docs-ca-install/latest/step-ca_amd64.deb
dpkg -i step-cli_amd64.deb step-ca_amd64.deb

export STEPPATH=/etc/step-ca
openssl rand -base64 24 > /root/ca-password && chmod 600 /root/ca-password
step ca init --deployment-type standalone --name "Lab CA" \
  --dns ca.lab.internal --address :8443 --provisioner admin@lab \
  --password-file /root/ca-password
step ca provisioner add acme --type ACME
```

Copy the **root fingerprint** that `step ca init` prints. Run the CA as a service:

```bash
cat >/etc/systemd/system/step-ca.service <<'EOF'
[Unit]
Description=step-ca
After=network-online.target
[Service]
Environment=STEPPATH=/etc/step-ca
ExecStart=/usr/bin/step-ca /etc/step-ca/config/ca.json --password-file /root/ca-password
Restart=on-failure
[Install]
WantedBy=multi-user.target
EOF
systemctl daemon-reload && systemctl enable --now step-ca
```

Running as root keeps this simple for a lab. A real CA runs as its own user with the key on an HSM.

Trust the root everywhere. Get it onto the admin VM first:

```bash
# on admin
curl -k https://ca.lab.internal:8443/roots.pem -o lab-root.crt
step certificate fingerprint lab-root.crt   # must match the fingerprint you copied
```

Then install it on each machine:

```bash
# Ubuntu / Debian
sudo cp lab-root.crt /usr/local/share/ca-certificates/lab-root.crt && sudo update-ca-certificates
# Rocky
sudo cp lab-root.crt /etc/pki/ca-trust/source/anchors/lab-root.crt && sudo update-ca-trust
```

Add it to your workstation's trust store too, so your browser trusts lab sites.

### Step 3: Two backends

Give each web VM a page that says which one it is:

```bash
# web1 (Ubuntu)
echo '<h1>web1</h1>' | sudo tee /var/www/html/index.html
# web2 (Rocky)
echo '<h1>web2</h1>' | sudo tee /usr/share/nginx/html/index.html
sudo systemctl enable --now nginx
sudo firewall-cmd --add-service=http --permanent && sudo firewall-cmd --reload
```

Check both from admin: `curl web1.lab.internal` and `curl web2.lab.internal`.

### Step 4: Nginx load balancer

```bash
# on the Proxmox host
qm clone 9000 130 --name lb --full
qm set 130 --ciuser jason --sshkeys ~/admin.pub --ipconfig0 ip=192.168.1.30/24,gw=<GW> \
  --nameserver 192.168.1.20 --searchdomain lab.internal
qm start 130
# on lb
sudo apt update && sudo apt install -y nginx certbot
sudo rm /etc/nginx/sites-enabled/default
```

Start with plain HTTP. Create `/etc/nginx/conf.d/app.conf`:

```nginx
upstream app_backend {
    server 192.168.1.31:80 max_fails=2 fail_timeout=10s;
    server 192.168.1.32:80 max_fails=2 fail_timeout=10s;
}

server {
    listen 80;
    server_name app.lab.internal;

    location /.well-known/acme-challenge/ { root /var/www/html; }

    location / {
        proxy_pass http://app_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

```bash
sudo nginx -t && sudo systemctl reload nginx
for i in 1 2 3 4; do curl -s app.lab.internal; done   # alternates web1 / web2
```

### Step 5: TLS from your CA with ACME

Certbot uses its own CA bundle, so point it at the system store (which now has your root):

```bash
sudo REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt certbot certonly \
  --webroot -w /var/www/html -d app.lab.internal \
  --server https://ca.lab.internal:8443/acme/acme/directory \
  --agree-tos -m admin@lab.internal --no-eff-email \
  --deploy-hook 'systemctl reload nginx'
```

Make automatic renewals use the same bundle: run `sudo systemctl edit certbot.service`, add the two lines below, and save:

```
[Service]
Environment=REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
```

step-ca issues 24-hour certs by default, so renewal happens daily. That's a good habit to see working, and `certbot renew --dry-run` tests it. Now replace `app.conf` with the TLS version:

```nginx
upstream app_backend {
    server 192.168.1.31:80 max_fails=2 fail_timeout=10s;
    server 192.168.1.32:80 max_fails=2 fail_timeout=10s;
}

server {
    listen 80;
    server_name app.lab.internal;
    location /.well-known/acme-challenge/ { root /var/www/html; }
    location / { return 301 https://$host$request_uri; }
}

server {
    listen 443 ssl http2;
    server_name app.lab.internal;
    ssl_certificate     /etc/letsencrypt/live/app.lab.internal/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/app.lab.internal/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;

    location / {
        proxy_pass http://app_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

```bash
sudo nginx -t && sudo systemctl reload nginx
curl -v https://app.lab.internal   # look for 'SSL certificate verify ok'
```

### Step 6: Fail over, cache, and break the cert

1. **Failover.** In one terminal on admin run `while true; do curl -s https://app.lab.internal; sleep 0.5; done`. In another, stop nginx on web1 and watch every request go to web2. Start it again.
2. **Caching.** Add this line above the `server` blocks:

    ```nginx
    proxy_cache_path /var/cache/nginx/app levels=1:2 keys_zone=app_cache:10m max_size=1g inactive=60m;
    ```

    Then add these inside `location /` of the 443 block, reload, and run `curl -sI https://app.lab.internal` twice:

    ```nginx
    proxy_cache app_cache;
    proxy_cache_valid 200 1m;
    add_header X-Cache-Status $upstream_cache_status;
    ```

    The header goes from `MISS` to `HIT`. Stop both backends and see what a cached page still serves.
3. **Break the cert.** On admin, bootstrap the step CLI with `step ca bootstrap --ca-url https://ca.lab.internal:8443 --fingerprint <fingerprint>`. Then issue a cert for the wrong name with `step ca certificate wrong.lab.internal wrong.crt wrong.key`. Copy it to lb, point `ssl_certificate` at it, and reload. Read the failure:

    ```bash
    curl -v https://app.lab.internal
    openssl s_client -connect app.lab.internal:443 -servername app.lab.internal </dev/null 2>/dev/null \
      | openssl x509 -noout -subject -ext subjectAltName -dates
    ```

    Repeat with a cert that expires quickly (`--not-after 2m`), wait 3 minutes, and compare the errors. Put the real cert back when you're done.

### Step 7: Squid forward proxy

```bash
# on the Proxmox host
pct create 122 local:vztmpl/<debian-template-file> --hostname squid \
  --cores 1 --memory 512 --rootfs <STORAGE>:8 --unprivileged 1 \
  --net0 name=eth0,bridge=<BRIDGE>,ip=192.168.1.22/24,gw=<GW> \
  --nameserver 192.168.1.20 --ssh-public-keys ~/admin.pub --onboot 1
pct start 122 && pct enter 122
apt update && apt install -y squid
```

Create `/etc/squid/conf.d/lab.conf` (Debian's `squid.conf` includes it before the final `deny all`):

```
acl labnet src 192.168.1.0/24
acl allowed_sites dstdomain .ubuntu.com .rockylinux.org .github.com .githubusercontent.com .pypi.org .pythonhosted.org
http_access deny !allowed_sites
http_access allow labnet
```

Run `squid -k parse && systemctl restart squid`, then test from web1:

```bash
curl -x http://squid.lab.internal:3128 -I https://github.com      # allowed
curl -x http://squid.lab.internal:3128 -I https://example.com     # 403 from squid
echo 'Acquire::http::Proxy "http://squid.lab.internal:3128";' | sudo tee /etc/apt/apt.conf.d/95proxy
sudo apt update
```

Watch it on squid with `tail -f /var/log/squid/access.log`. In Step 8 you block web1's direct internet access, so the proxy becomes its only way out.

### Step 8: Firewalls

**Proxmox firewall.** VM firewalls only work once the datacenter firewall is on. Keep the host itself open while you learn by creating `/etc/pve/firewall/cluster.fw` on the host:

```
[OPTIONS]
enable: 1
policy_in: ACCEPT
```

For the lb VM, tick **Firewall** on its network device (VM > Hardware > Network Device), then create `/etc/pve/firewall/130.fw`:

```
[OPTIONS]
enable: 1
policy_in: DROP

[RULES]
IN ACCEPT -p tcp -dport 80,443
IN ACCEPT -source 192.168.1.19 -p tcp -dport 22
IN ACCEPT -p icmp
```

Do the same for web1 (131). Allow port 80 only from the lb (`-source 192.168.1.30`) and SSH only from admin, and add an OUT rule set (`policy_out: DROP`) that allows only DNS to .20 and port 3128 to .22. Now apt on web1 works only through Squid.

**Host firewall.** On lb, add ufw as a second layer:

```bash
sudo ufw allow from 192.168.1.19 to any port 22 proto tcp
sudo ufw allow 80,443/tcp
sudo ufw enable
```

Prove it from admin with `nmap -Pn lb.lab.internal`, then from web2 with `nmap -Pn lb.lab.internal`. Only admin should see port 22.

**Gitea through the LB.** Add a TLS server block on lb for `gitea.lab.internal` that proxies to `http://192.168.1.21:3000`, and get its cert with the same certbot command. In `/etc/gitea/app.ini`, under `[server]`, set:

```
DOMAIN = gitea.lab.internal
ROOT_URL = https://gitea.lab.internal/
SSH_DOMAIN = git-ssh.lab.internal
```

Then run `systemctl restart gitea`. Git over SSH still goes straight to the container: update your clone with `git remote set-url origin git@git-ssh.lab.internal:jason/homelab.git`.

### Step 9: Harden SSH and add a jump host

On every VM, create `/etc/ssh/sshd_config.d/10-hardening.conf`:

```
PasswordAuthentication no
KbdInteractiveAuthentication no
PermitRootLogin no
AllowUsers jason ops
```

Check it before you reload, keeping your current session open in case it fails:

```bash
sudo sshd -t && sudo systemctl reload ssh    # Rocky: reload sshd
```

On your workstation, make admin the jump host in `~/.ssh/config`:

```
Host admin
  HostName 192.168.1.19
  User jason

Host *.lab.internal
  User jason
  ProxyJump admin
```

Now `ssh web1.lab.internal` goes through admin, which matches the firewall rules that allow SSH only from .19. The Proxmox console is your way back in if you lock yourself out.

Stretch goal: give the Proxmox web UI a cert from your CA. Install the root on the host, then add an ACME account under Datacenter > ACME with your CA's directory URL.

### Done when

- [ ] Every VM and container resolves `*.lab.internal` through Unbound
- [ ] `curl https://app.lab.internal` verifies with no `-k`, from admin and from your workstation browser
- [ ] Requests keep working with one backend stopped
- [ ] You can explain the curl and openssl output for a wrong-SAN cert and an expired cert
- [ ] web1 reaches the internet only through Squid
- [ ] `nmap` shows only 22 (from admin), 80 and 443 open on lb
- [ ] Password SSH is off everywhere, and Phase 2 configs are committed to Gitea

## Phase 3 runbook: Containers and infrastructure as code

By the end, `terraform apply && ansible-playbook site.yml` rebuilds lb, web1 and web2 from nothing. Code lives in `homelab/phase3/`. Run everything from the admin VM unless a step says otherwise.

### Step 1: Containers with Docker, and a look at LXC

Install Docker on admin:

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER && newgrp docker
```

In `homelab/phase1`, write a multi-stage `Dockerfile` for the inventory script:

```dockerfile
FROM python:3.12-alpine AS build
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

FROM python:3.12-alpine
RUN adduser -D -u 10001 app
COPY --from=build /install /usr/local
COPY pve_inventory.py /app/
USER app
ENTRYPOINT ["python", "/app/pve_inventory.py"]
```

```bash
docker build -t pve-inventory:0.1 .
docker image ls pve-inventory          # note the size
docker history pve-inventory:0.1       # which layer is biggest?
docker run --rm --env-file .env pve-inventory:0.1
docker run --rm --entrypoint id pve-inventory:0.1   # proves it isn't root
```

Python on Alpine lands around 60 to 80 MB. To get under 50 MB, build the Go version from Phase 1 into a `FROM scratch` image (usually under 15 MB) and compare.

Now compare with LXC. Create a throwaway container on the host (`pct create 140 ...`, as in Phase 1), install Python, and run the script there. Then check three things:

- `uname -r` inside the Docker container, inside the LXC and on the host: all three are the same kernel.
- On the host, `ps -ef | grep pve_inventory` while each runs: both show up as ordinary host processes.
- `time` from start to output for each.

Write down what that means for isolation. Delete the LXC when done.

### Step 2: S3 storage for Terraform state (SeaweedFS)

Terraform state needs a shared backend. MinIO's free edition is no longer maintained, so this guide uses [SeaweedFS](https://github.com/seaweedfs/seaweedfs), which has an S3 API.

1. On your NAS VM, create an NFS export for the lab (for example `/export/lab`, readable and writable from `<PVE_HOST>`).
2. Add it to Proxmox as storage: `pvesm add nfs nas --server <NAS_IP> --export /export/lab --content images,rootdir,backup`.
3. Create an LXC (ID 123, IP .23, hostname `s3`, 1 core, 1 GB) the same way as Phase 2, with `--rootfs nas:20` so its data lives on the NAS. Add `s3.lab.internal` to Unbound.
4. Inside it, install the `weed` binary. Download `linux_amd64.tar.gz` from the [SeaweedFS releases page](https://github.com/seaweedfs/seaweedfs/releases), extract it, and move `weed` to `/usr/local/bin`.
5. Create the S3 credentials file `/etc/seaweedfs/s3.json`, using keys you generate with `openssl rand -hex 16`:

    ```json
    {
      "identities": [
        {
          "name": "admin",
          "credentials": [{ "accessKey": "<ACCESS_KEY>", "secretKey": "<SECRET_KEY>" }],
          "actions": ["Admin", "Read", "Write", "List", "Tagging"]
        }
      ]
    }
    ```
6. Run it as a service. Use `ExecStart=/usr/local/bin/weed server -dir=/var/lib/seaweedfs -s3 -s3.port=8333 -s3.config=/etc/seaweedfs/s3.json`, written as a systemd unit the same way as Gitea's.
7. From admin, create the bucket:

    ```bash
    python3 -m venv ~/.venvs/aws && ~/.venvs/aws/bin/pip install awscli
    export AWS_ACCESS_KEY_ID=<ACCESS_KEY> AWS_SECRET_ACCESS_KEY=<SECRET_KEY>
    ~/.venvs/aws/bin/aws --endpoint-url http://s3.lab.internal:8333 s3 mb s3://tfstate
    ```

### Step 3: Terraform builds the VMs

Install Terraform from [HashiCorp's apt repo](https://developer.hashicorp.com/terraform/install), or use OpenTofu (the open-source fork, same syntax). Create a token Terraform can use, on the Proxmox host:

```bash
pveum user add terraform@pve
pveum aclmod / -user terraform@pve -role Administrator   # broad for now; Phase 4 narrows it
pveum user token add terraform@pve tf --privsep 0
```

Remove the hand-built web1 and web2 first so Terraform can own those IDs and IPs: `qm stop 131 && qm destroy 131`, and the same for 132. Also destroy lb (130) after you've copied its Nginx config into Git.

Create `homelab/phase3/terraform/main.tf`. Check the [bpg/proxmox registry page](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) for the current version and pin it:

```hcl
terraform {
  required_providers {
    proxmox = {
      source  = "bpg/proxmox"
      version = "~> 0.XX" # set to the current release
    }
  }

  backend "s3" {
    bucket                      = "tfstate"
    key                         = "phase3/terraform.tfstate"
    region                      = "us-east-1"
    endpoints                   = { s3 = "http://s3.lab.internal:8333" }
    use_path_style              = true
    skip_credentials_validation = true
    skip_region_validation      = true
    skip_requesting_account_id  = true
    skip_metadata_api_check     = true
    skip_s3_checksum            = true
  }
}

provider "proxmox" {
  endpoint  = "https://pve.lab.internal:8006/"
  api_token = var.pve_api_token
  insecure  = true # false once the Proxmox UI has a cert from your CA
}

resource "proxmox_virtual_environment_vm" "vm" {
  for_each  = var.vms
  name      = each.key
  vm_id     = each.value.id
  node_name = var.node

  clone {
    vm_id = each.value.template
    full  = true
  }

  agent {
    enabled = true
  }

  cpu {
    cores = 1
    type  = "host"
  }

  memory {
    dedicated = 1024
  }

  disk {
    datastore_id = var.storage
    interface    = "scsi0"
    size         = 10
  }

  network_device {
    bridge = var.bridge
  }

  initialization {
    datastore_id = var.storage
    dns {
      servers = ["192.168.1.20"]
      domain  = "lab.internal"
    }
    ip_config {
      ipv4 {
        address = "${each.value.ip}/24"
        gateway = var.gateway
      }
    }
    user_account {
      username = "jason"
      keys     = [trimspace(file("~/.ssh/id_ed25519.pub"))]
    }
  }
}

output "ips" {
  value = { for k, v in var.vms : k => v.ip }
}
```

And `variables.tf`:

```hcl
variable "pve_api_token" {
  type      = string
  sensitive = true # "terraform@pve!tf=<secret>"
}
variable "node" { default = "pve" }
variable "storage" { default = "local-lvm" }
variable "bridge" { default = "vmbr0" }
variable "gateway" { default = "192.168.1.1" }

variable "vms" {
  default = {
    lb   = { id = 130, ip = "192.168.1.30", template = 9000 }
    web1 = { id = 131, ip = "192.168.1.31", template = 9000 }
    web2 = { id = 132, ip = "192.168.1.32", template = 9001 }
  }
}
```

Run it:

```bash
export TF_VAR_pve_api_token='terraform@pve!tf=<secret>'
export AWS_ACCESS_KEY_ID=<ACCESS_KEY> AWS_SECRET_ACCESS_KEY=<SECRET_KEY>
terraform init
terraform plan     # read every line before applying
terraform apply
```

Then practice the loop until it feels routine:

1. Change web1's memory to 2048 and `plan`. Is it an update in place or a replace?
2. Add `web3` to the map, `apply`, then remove it and `apply` again.
3. Change something in the Proxmox UI by hand, then `plan` to see the drift.
4. Run `terraform destroy` and then `terraform apply`, and time it.
5. Look at the state file in the bucket (`aws s3 ls s3://tfstate/phase3/ --endpoint-url ...`). Why must it never go into Git?

### Step 4: Ansible configures them

```bash
python3 -m venv ~/.venvs/ansible && source ~/.venvs/ansible/bin/activate
pip install ansible requests proxmoxer
ansible-galaxy collection install community.proxmox ansible.posix
```

Lay out `homelab/phase3/ansible/`:

```
ansible.cfg
inventory/hosts.ini
site.yml
files/lab-root.crt
roles/common/{tasks,handlers}/main.yml
roles/web/{tasks,templates}/...
roles/lb/{tasks,handlers,templates}/...
```

Create `ansible.cfg`:

```ini
[defaults]
inventory = inventory/hosts.ini
remote_user = jason
host_key_checking = False
```

Create a static inventory first, `inventory/hosts.ini`:

```ini
[lb]
lb.lab.internal

[web]
web1.lab.internal
web2.lab.internal
```

Create the `common` role, `roles/common/tasks/main.yml`. It works on Ubuntu and Rocky:

```yaml
- name: Trust the lab root CA (Debian family)
  ansible.builtin.copy:
    src: lab-root.crt
    dest: /usr/local/share/ca-certificates/lab-root.crt
    mode: "0644"
  notify: update ca debian
  when: ansible_os_family == "Debian"

- name: Trust the lab root CA (RedHat family)
  ansible.builtin.copy:
    src: lab-root.crt
    dest: /etc/pki/ca-trust/source/anchors/lab-root.crt
    mode: "0644"
  notify: update ca redhat
  when: ansible_os_family == "RedHat"

- name: Ops user
  ansible.builtin.user:
    name: ops
    shell: /bin/bash

- name: Passwordless sudo for ops
  ansible.builtin.copy:
    content: "ops ALL=(ALL) NOPASSWD:ALL\n"
    dest: /etc/sudoers.d/ops
    mode: "0440"
    validate: visudo -cf %s

- name: SSH hardening
  ansible.builtin.copy:
    dest: /etc/ssh/sshd_config.d/10-hardening.conf
    content: |
      PasswordAuthentication no
      KbdInteractiveAuthentication no
      PermitRootLogin no
      AllowUsers jason ops
    mode: "0644"
    validate: /usr/sbin/sshd -t -f %s
  notify: reload sshd
```

Its handlers, `roles/common/handlers/main.yml`:

```yaml
- name: update ca debian
  ansible.builtin.command: update-ca-certificates

- name: update ca redhat
  ansible.builtin.command: update-ca-trust

- name: reload sshd
  ansible.builtin.service:
    name: "{{ 'ssh' if ansible_os_family == 'Debian' else 'sshd' }}"
    state: reloaded
```

The `web` role installs Nginx, writes an `index.html` from a template that prints `{{ inventory_hostname }}`, and opens HTTP with `ansible.posix.firewalld` on Rocky. Write it yourself, using the common role as the pattern.

The `lb` role builds its upstream list from the inventory, so adding a web VM means one new inventory line. In `roles/lb/templates/app.conf.j2`:

```jinja
upstream app_backend {
{% for host in groups['web'] %}
    server {{ host }}:80 max_fails=2 fail_timeout=10s;
{% endfor %}
}
```

The rest of the file is your Phase 2 config. The lb role must do things in this order, or `nginx -t` fails before the cert exists:

1. Template an HTTP-only config.
2. Run certbot as an `ansible.builtin.command` with `creates: /etc/letsencrypt/live/app.lab.internal/fullchain.pem`, so it runs only once.
3. Template the full TLS config and notify a `reload nginx` handler.

Finally, `site.yml`:

```yaml
- hosts: all
  become: true
  roles: [common]

- hosts: web
  become: true
  roles: [web]

- hosts: lb
  become: true
  roles: [lb]
```

Run it and prove it's idempotent:

```bash
ansible all -m ping
ansible-playbook site.yml --check --diff   # dry run
ansible-playbook site.yml
ansible-playbook site.yml                  # second run: every host should show changed=0
```

**Dynamic inventory.** Replace `hosts.ini` with `inventory/pve.proxmox.yml`. It reuses the Phase 1 read-only token and puts hosts into groups by name:

```yaml
plugin: community.proxmox.proxmox
url: https://pve.lab.internal:8006
user: automation@pve
token_id: inventory
validate_certs: false
want_facts: true
compose:
  ansible_host: inventory_hostname ~ '.lab.internal'
keyed_groups: []
groups:
  web: inventory_hostname.startswith('web')
  lb: inventory_hostname == 'lb'
```

Pass the secret with `export PROXMOX_TOKEN_SECRET=<secret>`, then run `ansible-inventory -i inventory/pve.proxmox.yml --graph` to check the groups. If your Ansible is older, the plugin is `community.general.proxmox` instead.

### Step 5: The one-command rebuild

Add `homelab/phase3/rebuild.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail
cd "$(dirname "$0")"
(cd terraform && terraform apply -auto-approve)
for h in lb web1 web2; do
  until ssh -o ConnectTimeout=3 jason@$h.lab.internal true 2>/dev/null; do sleep 5; done
done
(cd ansible && ansible-playbook site.yml)
curl -sf https://app.lab.internal >/dev/null && echo "app is up"
```

Run `terraform destroy`, then `time ./rebuild.sh`. Do it three times.

### Step 6 (stretch): The golden image as code with Packer

Your golden image is hand-made today. Packer can build it from code instead:

1. Install Packer from the same HashiCorp repo, then add the `hashicorp/proxmox` and `hashicorp/ansible` plugins with `packer init`.
2. Use the `proxmox-clone` source to clone template 9000. Give it the Terraform API token and a new `vm_id` (for example 9100) and `template_name`.
3. Add an `ansible` provisioner that runs your `common` role, so every new VM starts already hardened and trusting your CA.
4. Run `packer build .`, then point Terraform's `template` values at 9100.

The SSH settings Packer uses to reach the clone differ between plugin versions, so follow the plugin's [proxmox-clone docs](https://developer.hashicorp.com/packer/integrations/hashicorp/proxmox/latest/components/builder/clone) for that part.

### Step 7: A taste of serverless (OpenFaaS)

On admin, copy the existing cluster's kubeconfig (`/etc/kubernetes/admin.conf` from the control-plane node) to `~/.kube/config`. Then:

```bash
curl -sLS https://get.arkade.dev | sudo sh
arkade get kubectl faas-cli && export PATH=$PATH:$HOME/.arkade/bin
arkade install openfaas
kubectl rollout status -n openfaas deploy/gateway
kubectl port-forward -n openfaas svc/gateway 8080:8080 &
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath='{.data.basic-auth-password}' | base64 -d)
echo -n "$PASSWORD" | faas-cli login --username admin --password-stdin
faas-cli store deploy figlet
echo "hello lab" | faas-cli invoke figlet
```

Then write your own function: `faas-cli new --lang python3-http hello`, build it, and deploy it. Compare triggers, scaling to zero and cold starts with Azure Functions. Remove it with `arkade uninstall openfaas` (or delete the `openfaas` and `openfaas-fn` namespaces) before Phase 5 rebuilds the cluster.

Optional: redo Step 3 in Pulumi with Python (`pulumi new python`, plus the `pulumi_proxmoxve` package) to see the same VMs defined in a general-purpose language.

### Done when

- [ ] Your image runs as non-root, and you can explain each layer in `docker history`
- [ ] Terraform state lives in the SeaweedFS bucket, not on disk or in Git
- [ ] `terraform destroy` followed by `rebuild.sh` gives you a working `https://app.lab.internal`
- [ ] The second `ansible-playbook` run shows `changed=0` on every host
- [ ] Adding a web VM takes one Terraform map entry and one inventory line
- [ ] One function has run on OpenFaaS

## Phase 4 runbook: CI/CD, artifacts and secrets

By the end, a push to `main` lints, tests, builds, scans and pushes an image to Harbor, using secrets fetched from Vault at run time. A pull request that touches Terraform shows a plan; merging it applies the plan. Pipelines live in `homelab/.gitea/workflows/`.

### Step 1: Add the new VMs to Terraform

Give the `vms` variable an explicit type with per-VM sizes, so bigger VMs don't need their own resource block:

```hcl
variable "vms" {
  type = map(object({
    id       = number
    ip       = string
    template = number
    cores    = optional(number, 1)
    memory   = optional(number, 1024)
    disk     = optional(number, 10)
  }))
  default = {
    lb     = { id = 130, ip = "192.168.1.30", template = 9000 }
    web1   = { id = 131, ip = "192.168.1.31", template = 9000 }
    web2   = { id = 132, ip = "192.168.1.32", template = 9001 }
    runner = { id = 140, ip = "192.168.1.40", template = 9000, cores = 2, memory = 4096, disk = 40 }
    harbor = { id = 141, ip = "192.168.1.41", template = 9000, cores = 2, memory = 4096, disk = 60 }
    vault1 = { id = 142, ip = "192.168.1.42", template = 9000 }
    vault2 = { id = 143, ip = "192.168.1.43", template = 9000 }
    vault3 = { id = 144, ip = "192.168.1.44", template = 9000 }
  }
}
```

In `main.tf`, change `cores = 1`, `dedicated = 1024` and `size = 10` to `each.value.cores`, `each.value.memory` and `each.value.disk`. Add the new names to Unbound, plus three `vault.lab.internal` A records (one per Vault IP). Run `terraform apply`, add the hosts to your Ansible inventory, and run `site.yml` so they get the common role.

Raise step-ca's maximum cert lifetime so long-running services don't need daily renewals. On the dns container:

```bash
export STEPPATH=/etc/step-ca
step ca provisioner update admin@lab --x509-max-dur 2160h --x509-default-dur 720h
systemctl restart step-ca
```

### Step 2: Harbor registry

On harbor, install Docker (as in Phase 3) and get a cert:

```bash
step ca bootstrap --ca-url https://ca.lab.internal:8443 --fingerprint <fingerprint>
step ca certificate harbor.lab.internal harbor.crt harbor.key --not-after 2160h
sudo mkdir -p /etc/harbor/tls && sudo mv harbor.crt harbor.key /etc/harbor/tls/
```

Download the **online installer** from the [Harbor releases page](https://github.com/goharbor/harbor/releases), then:

```bash
tar xzf harbor-online-installer-*.tgz && cd harbor
cp harbor.yml.tmpl harbor.yml
```

In `harbor.yml`, set `hostname: harbor.lab.internal`, point `https.certificate` and `https.private_key` at the two files, and change `harbor_admin_password`. Then:

```bash
sudo ./install.sh --with-trivy
```

In the Harbor UI (`https://harbor.lab.internal`):

1. Create a private project named `lab`. Turn on **Automatically scan images on push**.
2. Under the project, create a robot account `ci` with push and pull rights. Save its name (it looks like `robot$lab+ci`) and its secret.
3. Test from admin:

    ```bash
    docker login harbor.lab.internal
    docker tag pve-inventory:0.1 harbor.lab.internal/lab/pve-inventory:0.1
    docker push harbor.lab.internal/lab/pve-inventory:0.1
    ```

    Docker trusts Harbor because the common role installed your root CA. If it fails, run `sudo systemctl restart docker`.

### Step 3: Gitea Actions runner

On runner, install the build tools the pipelines need:

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo apt install -y python3-venv nodejs git jq
# Trivy: follow the apt steps at https://trivy.dev, then:
trivy --version
```

Actions needs Node.js on the runner, because `actions/checkout` is a JavaScript action.

In Gitea, go to Site Administration > Actions > Runners > **Create new runner** and copy the registration token. Then, with `RUNNER_VERSION` set to the newest release listed at [dl.gitea.com/act_runner](https://dl.gitea.com/act_runner/):

```bash
sudo useradd -m -s /bin/bash -G docker runner
sudo -iu runner
curl -fsSL -o act_runner https://dl.gitea.com/act_runner/${RUNNER_VERSION}/act_runner-${RUNNER_VERSION}-linux-amd64
chmod +x act_runner
./act_runner generate-config > config.yaml
./act_runner register --no-interactive --config config.yaml \
  --instance https://gitea.lab.internal --token <TOKEN> \
  --name runner1 --labels lab:host
exit
```

The `lab:host` label runs jobs directly on this VM with its own Docker, which is simpler than Docker-in-Docker. Create `/etc/systemd/system/act_runner.service` with `User=runner`, `WorkingDirectory=/home/runner` and `ExecStart=/home/runner/act_runner daemon --config /home/runner/config.yaml`, then run `sudo systemctl enable --now act_runner`. The runner should show as idle in Gitea.

In the `homelab` repo's settings, turn on **Actions**. Add repo secrets `HARBOR_USER` and `HARBOR_PASSWORD`; you'll replace them with Vault in Step 6.

### Step 4: The CI pipeline

Create `.gitea/workflows/ci.yml`:

```yaml
name: ci
on:
  push:
    branches: [main]
    paths: ['phase1/**']
  pull_request:
    paths: ['phase1/**']

env:
  IMAGE: harbor.lab.internal/lab/pve-inventory

jobs:
  build:
    runs-on: lab
    steps:
      - uses: actions/checkout@v4

      - name: Lint and test
        run: |
          python3 -m venv .venv && . .venv/bin/activate
          pip install ruff pytest -r phase1/requirements.txt
          ruff check phase1
          pytest phase1 || [ $? -eq 5 ]   # exit 5 = no tests yet

      - name: Build
        run: docker build -t $IMAGE:${{ github.sha }} phase1

      - name: Scan
        run: trivy image --exit-code 1 --severity HIGH,CRITICAL $IMAGE:${{ github.sha }}

      - name: Push
        if: github.event_name == 'push'
        run: |
          echo '${{ secrets.HARBOR_PASSWORD }}' | docker login harbor.lab.internal -u '${{ secrets.HARBOR_USER }}' --password-stdin
          docker push $IMAGE:${{ github.sha }}
          docker tag $IMAGE:${{ github.sha }} $IMAGE:latest && docker push $IMAGE:latest
```

Then exercise it:

1. Open a pull request with a deliberate lint error and watch it fail.
2. Fix it, merge, and watch the image land in Harbor.
3. Bump the base image to an old tag (for example `python:3.9-alpine`) and see the Trivy step block it.
4. In repo settings, protect `main`: require a pull request and a passing `ci` check.

### Step 5: The same pipeline in Jenkins

You've run Jenkins at work, so the point here is the comparison. Run the controller in Docker on runner, and use runner itself as an SSH build agent:

```bash
sudo apt install -y openjdk-21-jre-headless    # agents need Java
docker run -d --name jenkins --restart unless-stopped -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk21
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

1. Finish setup at `http://runner.lab.internal:8080` with the suggested plugins, then add the **Gitea** plugin.
2. Add a node named `lab` (label `lab`), launched over SSH as the `runner` user with a key credential.
3. Create a Pipeline job that reads `phase1/Jenkinsfile` from the Gitea repo:

    ```groovy
    pipeline {
      agent { label 'lab' }
      environment { IMAGE = "harbor.lab.internal/lab/pve-inventory" }
      stages {
        stage('Lint') {
          steps {
            sh 'python3 -m venv .venv && . .venv/bin/activate && pip install ruff && ruff check phase1'
          }
        }
        stage('Build') {
          steps { sh 'docker build -t $IMAGE:jenkins-$BUILD_NUMBER phase1' }
        }
        stage('Scan') {
          steps { sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL $IMAGE:jenkins-$BUILD_NUMBER' }
        }
      }
    }
    ```
4. Write down where each tool is easier: secrets, reuse, plugin upkeep, and how much state lives outside Git. After Phase 5, try the Kubernetes plugin so each build gets its own pod as an agent.

### Step 6: Vault

**Dev mode first (10 minutes).** On admin, install Vault from the HashiCorp apt repo and play with it before you build anything permanent:

```bash
sudo apt install -y vault
vault server -dev &          # prints a root token; in-memory only
export VAULT_ADDR=http://127.0.0.1:8200
vault kv put secret/hello msg=world && vault kv get secret/hello
```

**A 3-node Raft cluster.** On each of vault1, vault2 and vault3, install Vault the same way, then get a cert that names both the node and the shared name:

```bash
N=vault1   # change per node
step ca certificate $N.lab.internal vault.crt vault.key \
  --san $N.lab.internal --san vault.lab.internal --not-after 2160h
sudo install -o vault -g vault -m 640 vault.crt vault.key /opt/vault/tls/
```

Write `/etc/vault.d/vault.hcl`, changing `vault1` to the node's own name in `node_id`, `api_addr` and `cluster_addr`:

```hcl
ui           = true
cluster_name = "lab"
api_addr     = "https://vault1.lab.internal:8200"
cluster_addr = "https://vault1.lab.internal:8201"

storage "raft" {
  path    = "/opt/vault/data"
  node_id = "vault1"
  retry_join {
    leader_api_addr     = "https://vault1.lab.internal:8200"
    leader_ca_cert_file = "/usr/local/share/ca-certificates/lab-root.crt"
  }
  retry_join {
    leader_api_addr     = "https://vault2.lab.internal:8200"
    leader_ca_cert_file = "/usr/local/share/ca-certificates/lab-root.crt"
  }
  retry_join {
    leader_api_addr     = "https://vault3.lab.internal:8200"
    leader_ca_cert_file = "/usr/local/share/ca-certificates/lab-root.crt"
  }
}

listener "tcp" {
  address       = "0.0.0.0:8200"
  tls_cert_file = "/opt/vault/tls/vault.crt"
  tls_key_file  = "/opt/vault/tls/vault.key"
}
```

Start Vault on all three nodes, then initialize once, on vault1 only:

```bash
sudo systemctl enable --now vault
export VAULT_ADDR=https://vault1.lab.internal:8200
vault operator init -key-shares=5 -key-threshold=3   # store the keys and root token OFF the lab
vault operator unseal    # run 3 times, with 3 different keys
```

Unseal vault2 and vault3 the same way, each with its own `VAULT_ADDR`. Check with `vault operator raft list-peers`; you should see one leader and two followers. Every reboot seals a node again. Auto-unseal is a stretch goal for later.

**Put your secrets in, and give CI a narrow way to read them:**

```bash
export VAULT_ADDR=https://vault.lab.internal:8200
vault login     # root token for setup only

vault secrets enable -path=lab kv-v2
vault kv put lab/harbor username='robot$lab+ci' password='<robot secret>'
vault kv put lab/proxmox token='terraform@pve!tf=<secret>'
vault kv put lab/s3 access_key=<ACCESS_KEY> secret_key=<SECRET_KEY>

vault policy write ci - <<'EOF'
path "lab/data/harbor"  { capabilities = ["read"] }
path "lab/data/proxmox" { capabilities = ["read"] }
path "lab/data/s3"      { capabilities = ["read"] }
path "lab/data/sops"    { capabilities = ["read"] }
EOF

vault auth enable approle
vault write auth/approle/role/ci token_policies=ci token_ttl=15m secret_id_ttl=720h
vault read -field=role_id auth/approle/role/ci/role-id
vault write -f -field=secret_id auth/approle/role/ci/secret-id
```

Put the role ID and secret ID in Gitea as `VAULT_ROLE_ID` and `VAULT_SECRET_ID`, and **delete** `HARBOR_USER` and `HARBOR_PASSWORD`. (Those two IDs are your "secret zero": the one credential CI must hold to get all the others.) Install the Vault CLI on runner, and replace the Push step in `ci.yml`:

```yaml
      - name: Push
        if: github.event_name == 'push'
        env:
          VAULT_ADDR: https://vault.lab.internal:8200
        run: |
          export VAULT_TOKEN=$(vault write -field=token auth/approle/login \
            role_id='${{ secrets.VAULT_ROLE_ID }}' secret_id='${{ secrets.VAULT_SECRET_ID }}')
          vault kv get -field=password lab/harbor | \
            docker login harbor.lab.internal -u "$(vault kv get -field=username lab/harbor)" --password-stdin
          docker push $IMAGE:${{ github.sha }}
```

Stretch goals: the database secrets engine (Vault issues a short-lived Postgres user per job), the SSH secrets engine (signed SSH certs instead of `authorized_keys`), and auto-unseal using a fourth small Vault with the transit engine.

### Step 7: SOPS and age for secrets in Git

SOPS lets you commit encrypted files and decrypt them only where the key is. On admin:

```bash
sudo apt install -y age
# sops: download the linux.amd64 binary from https://github.com/getsops/sops/releases into /usr/local/bin/sops
mkdir -p ~/.config/sops/age && age-keygen -o ~/.config/sops/age/keys.txt
grep 'public key' ~/.config/sops/age/keys.txt
```

At the root of `homelab`, create `.sops.yaml`:

```yaml
creation_rules:
  - path_regex: secrets/.*\.yaml$
    age: <your age public key>
```

```bash
mkdir -p secrets && printf 'db_password: changeme\napi_key: abc123\n' > secrets/app.yaml
sops -e -i secrets/app.yaml
cat secrets/app.yaml          # keys readable, values encrypted
sops secrets/app.yaml         # edit in place, re-encrypted on save
git add .sops.yaml secrets/ && git commit -m "SOPS-encrypted secrets"
```

Give CI the private key through Vault: `vault kv put lab/sops key=@$HOME/.config/sops/age/keys.txt`. Then in a workflow step, `export SOPS_AGE_KEY=$(vault kv get -field=key lab/sops)` followed by `sops -d secrets/app.yaml`. Phase 5 adds Sealed Secrets and External Secrets Operator, the Kubernetes-native versions of the same idea.

### Step 8: Terraform from the pipeline

First, narrow Terraform's Proxmox rights. Create a custom role with only the privileges the [bpg provider docs](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) list, using `pveum role add TerraformProv -privs "<list>"`. Then swap it for `Administrator` with `pveum aclmod / -user terraform@pve -role TerraformProv`.

Create `.gitea/workflows/terraform.yml`:

```yaml
name: terraform
on:
  pull_request:
    paths: ['phase3/terraform/**']
  push:
    branches: [main]
    paths: ['phase3/terraform/**']

jobs:
  terraform:
    runs-on: lab
    defaults:
      run:
        working-directory: phase3/terraform
    env:
      VAULT_ADDR: https://vault.lab.internal:8200
    steps:
      - uses: actions/checkout@v4

      - name: Credentials from Vault
        run: |
          export VAULT_TOKEN=$(vault write -field=token auth/approle/login \
            role_id='${{ secrets.VAULT_ROLE_ID }}' secret_id='${{ secrets.VAULT_SECRET_ID }}')
          PVE=$(vault kv get -field=token lab/proxmox)
          AK=$(vault kv get -field=access_key lab/s3)
          SK=$(vault kv get -field=secret_key lab/s3)
          echo "::add-mask::$PVE"; echo "::add-mask::$SK"
          echo "TF_VAR_pve_api_token=$PVE" >> $GITHUB_ENV
          echo "AWS_ACCESS_KEY_ID=$AK" >> $GITHUB_ENV
          echo "AWS_SECRET_ACCESS_KEY=$SK" >> $GITHUB_ENV

      - run: terraform init -input=false
      - run: terraform fmt -check
      - run: terraform validate
      - run: terraform plan -input=false -out=tfplan
      - name: Apply
        if: github.event_name == 'push'
        run: terraform apply -input=false tfplan
```

The `~/.ssh/id_ed25519.pub` that `main.tf` reads must exist on runner too. Generate it there, or better, move the public key into a variable. Test the whole loop: open a pull request that adds `web3`, read the plan in the job log, merge, and watch it apply.

### Done when

- [ ] A merge to `main` builds, scans and pushes a tagged image to Harbor
- [ ] A vulnerable base image fails the pipeline
- [ ] `vault operator raft list-peers` shows 3 voters, and the cluster survives losing one node
- [ ] Gitea holds only the AppRole IDs; every other credential comes from Vault
- [ ] `secrets/app.yaml` is encrypted in Git and decrypts in CI
- [ ] A Terraform change goes from pull request to applied with no laptop involved
- [ ] You've run the same build in Jenkins and written down how the two compare

## Phase 5 runbook: Kubernetes and GitOps

By the end you have a kubeadm cluster with a 3-node HA control plane behind your Nginx LB, NFS storage, Argo CD deploying everything from Gitea, and pods reading secrets from Vault. Steps 3 and 4 are CKA exam drills. Code lives in `homelab/phase5/`.

Before you start, shut down your existing 3-node cluster to free its 12 GB. Keep its clean-state snapshot.

### Step 1: Add the cluster VMs to Terraform

Add these to the `vms` map: `cp1` (150, .50), `w1` (153, .53) and `w2` (154, .54), each with `cores = 2, memory = 4096, disk = 30`. Leave cp2 and cp3 for Step 5. In Unbound, add records for each node, plus the API name, which points at cp1 for now:

```
local-data: "k8s-api.lab.internal. A 192.168.1.50"
```

Pointing kubeadm at a name instead of an IP is what lets you go HA later without rebuilding. Run `terraform apply`, add a `[k8s]` group to the Ansible inventory, and run `site.yml`.

### Step 2: Install kubeadm and build the cluster

**On every node.** Turn these commands into an Ansible role `k8s_node` once they work by hand:

```bash
# kernel modules and sysctls
printf 'overlay\nbr_netfilter\n' | sudo tee /etc/modules-load.d/k8s.conf
sudo modprobe overlay && sudo modprobe br_netfilter
printf 'net.bridge.bridge-nf-call-iptables=1\nnet.bridge.bridge-nf-call-ip6tables=1\nnet.ipv4.ip_forward=1\n' \
  | sudo tee /etc/sysctl.d/k8s.conf
sudo sysctl --system

# containerd with the systemd cgroup driver
sudo apt install -y containerd nfs-common
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml >/dev/null
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml
sudo systemctl restart containerd

# Kubernetes packages: pick ONE minor below the newest at kubernetes.io/releases,
# so Step 4 can practice an upgrade
K8S=v1.XX
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/$K8S/deb/Release.key \
  | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/$K8S/deb/ /" \
  | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update && sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

Cloud images have no swap, so there's nothing to turn off. Check with `free -h`.

**On cp1:**

```bash
sudo kubeadm init --control-plane-endpoint k8s-api.lab.internal:6443 \
  --upload-certs --pod-network-cidr 10.244.0.0/16
mkdir -p ~/.kube && sudo cp /etc/kubernetes/admin.conf ~/.kube/config && sudo chown $(id -u):$(id -g) ~/.kube/config
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
```

Save the two `kubeadm join` commands it prints: one for control-plane nodes, one for workers. Run the worker one with `sudo` on w1 and w2. Copy `~/.kube/config` to the admin VM, then check:

```bash
kubectl get nodes -o wide          # all Ready
kubectl get pods -A                # everything Running
```

Join tokens expire after 24 hours. Make a new one with `kubeadm token create --print-join-command`.

### Step 3: CKA drills on a single control plane

Do these now, while there's one control-plane node; they're simpler and closer to the exam. Take a Proxmox snapshot of all three nodes first (`qm snapshot 150 pre-drills`, and the same for 153 and 154).

**etcd backup and restore** (on cp1):

```bash
sudo apt install -y etcd-client   # gives etcdctl; or exec into the etcd pod
kubectl create deployment canary --image=nginx
sudo ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /var/backups/etcd-snap.db
kubectl delete deployment canary
```

Now restore it:

```bash
sudo etcdutl snapshot restore /var/backups/etcd-snap.db --data-dir /var/lib/etcd-restore
# point etcd at the restored data:
sudo sed -i 's#path: /var/lib/etcd$#path: /var/lib/etcd-restore#' /etc/kubernetes/manifests/etcd.yaml
# wait 1 to 2 minutes for etcd and the API server to restart
kubectl get deployment canary      # it's back
```

If `etcdutl` isn't installed, `etcdctl snapshot restore` takes the same flags on older versions.

**Break and fix** (one at a time; roll back with `qm rollback` if you get stuck):

| Break it | What you see | Find it with |
| --- | --- | --- |
| On w1: `sudo mv /var/lib/kubelet/config.yaml /root/` then `sudo systemctl restart kubelet` | w1 goes `NotReady` | `systemctl status kubelet`, `journalctl -u kubelet -n 50` |
| On w1: `sudo systemctl stop containerd` | Pods on w1 fail | `crictl ps` errors, `kubectl describe node w1` |
| On cp1: change `--secure-port` or add a typo in `/etc/kubernetes/manifests/kube-apiserver.yaml` | `kubectl` refuses to connect | `sudo crictl ps -a \| grep apiserver`, `sudo crictl logs <id>`, `journalctl -u kubelet` |
| `kubectl -n kube-flannel delete ds kube-flannel-ds` | New pods stuck in `ContainerCreating` | `kubectl describe pod` shows a CNI error |
| `kubectl cordon w2`, then scale a deployment up | New pods only go to w1 | `kubectl get nodes`, `kubectl get pods -o wide` |

**Drain and upgrade one minor version.** Switch the apt repo on every node to the next minor (`K8S=v1.YY`), then:

```bash
# cp1
sudo apt-mark unhold kubeadm && sudo apt update && sudo apt install -y kubeadm && sudo apt-mark hold kubeadm
sudo kubeadm upgrade plan
sudo kubeadm upgrade apply v1.YY.Z
kubectl drain cp1 --ignore-daemonsets
sudo apt-mark unhold kubelet kubectl && sudo apt install -y kubelet kubectl && sudo apt-mark hold kubelet kubectl
sudo systemctl daemon-reload && sudo systemctl restart kubelet
kubectl uncordon cp1

# each worker: upgrade kubeadm as above, then
sudo kubeadm upgrade node
# from admin: kubectl drain w1 --ignore-daemonsets --delete-emptydir-data
# on w1: upgrade kubelet and kubectl, restart kubelet
# from admin: kubectl uncordon w1
```

`kubectl get nodes` should show the new version everywhere.

### Step 4: Swap Flannel for Cilium, and prove NetworkPolicy works

First, see the gap. Flannel doesn't enforce NetworkPolicy:

```bash
kubectl create ns demo
kubectl -n demo create deployment web --image=nginx
kubectl -n demo expose deployment web --port 80
kubectl -n demo run client --image=busybox --restart=Never -- sleep 3600
kubectl -n demo exec client -- wget -qO- -T 3 web    # works

cat <<'EOF' | kubectl apply -f -
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: demo
spec:
  podSelector: {}
  policyTypes: [Ingress]
EOF
kubectl -n demo exec client -- wget -qO- -T 3 web    # STILL works: Flannel ignores policy
```

Swapping a CNI in place is messy. You have Terraform, so rebuild instead:

1. Run `terraform destroy` on cp1, w1 and w2, then `apply`, and repeat Step 2 **without** the Flannel line.
2. Install the [Cilium CLI](https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/) on admin, then run `cilium install` and `cilium status --wait`.
3. Run the demo again. With `default-deny` applied, the `wget` now times out.
4. Allow only labelled clients:

    ```bash
    cat <<'EOF' | kubectl apply -f -
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-client
      namespace: demo
    spec:
      podSelector:
        matchLabels: { app: web }
      ingress:
        - from:
            - podSelector:
                matchLabels: { role: client }
          ports:
            - port: 80
    EOF
    kubectl -n demo label pod client role=client
    kubectl -n demo exec client -- wget -qO- -T 3 web    # works again
    ```

The rest of this guide assumes Cilium.

### Step 5: HA control plane behind the LB

Add `cp2` (151, .51) and `cp3` (152, .52) to Terraform and run Step 2's node prep on them. Then turn lb into a TCP load balancer for the API server. Install the module with `sudo apt install -y libnginx-mod-stream`, and add this at the **end** of `/etc/nginx/nginx.conf` (outside the `http` block):

```nginx
stream {
    upstream k8s_api {
        server 192.168.1.50:6443 max_fails=2 fail_timeout=10s;
        server 192.168.1.51:6443 max_fails=2 fail_timeout=10s;
        server 192.168.1.52:6443 max_fails=2 fail_timeout=10s;
    }
    server {
        listen 6443;
        proxy_pass k8s_api;
    }
}
```

Open 6443 on lb (in `130.fw` and `ufw`), reload Nginx, and change the Unbound record to `k8s-api.lab.internal. A 192.168.1.30`. On cp1, get a fresh certificate key and join command:

```bash
sudo kubeadm init phase upload-certs --upload-certs     # prints a certificate key
kubeadm token create --print-join-command
```

On cp2 and cp3, run the join command with `--control-plane --certificate-key <key>` added. Then test that it really is HA:

```bash
kubectl get nodes                       # 3 control-plane nodes
kubectl -n kube-system get pods -l component=etcd
# on the Proxmox host: qm stop 150   (cp1)
kubectl get nodes                       # still answers, via cp2 or cp3
# qm start 150
```

Put the stream config into your Ansible `lb` role.

### Step 6: Storage on the NAS

On the NAS VM, export `/export/k8s` to the k8s node IPs with `rw,no_root_squash`. Then, from admin:

```bash
curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm repo add csi-driver-nfs https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/master/charts
helm install csi-driver-nfs csi-driver-nfs/csi-driver-nfs -n kube-system
```

Create a default StorageClass:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: nfs.csi.k8s.io
parameters:
  server: <NAS_IP>
  share: /export/k8s
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions: [nfsvers=4.1]
```

Test it with a StatefulSet that writes to its volume:

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: writer
  namespace: demo
spec:
  serviceName: writer
  replicas: 2
  selector:
    matchLabels: { app: writer }
  template:
    metadata:
      labels: { app: writer }
    spec:
      containers:
        - name: writer
          image: busybox
          command: [sh, -c, 'while true; do date >> /data/log; sleep 10; done']
          volumeMounts:
            - { name: data, mountPath: /data }
  volumeClaimTemplates:
    - metadata: { name: data }
      spec:
        accessModes: [ReadWriteOnce]
        resources: { requests: { storage: 1Gi } }
```

Check with `kubectl -n demo get pvc` (Bound), then find which node runs `writer-0` and `qm stop` it. Watch what happens. The pod stays `Terminating`, because Kubernetes can't be sure the dead node has stopped writing. That's the lesson. Fix it the way the docs describe:

```bash
kubectl taint node <node> node.kubernetes.io/out-of-service=nodeshutdown:NoExecute
```

`writer-0` comes back on another node with its old log intact. Remove the taint once the node is back.

### Step 7: Argo CD and the app-of-apps

This is the last thing you install by hand. Everything after it goes through Git.

```bash
kubectl create namespace argocd
kubectl apply -n argocd --server-side --force-conflicts \
  -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl -n argocd rollout status deploy/argocd-server
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d; echo
kubectl -n argocd port-forward svc/argocd-server 8080:443 &

# argocd CLI: arkade get argocd (or download from the Argo CD releases page)
argocd login localhost:8080 --username admin --insecure
argocd cert add-tls gitea.lab.internal --from ~/lab-root.crt
argocd repo add https://gitea.lab.internal/jason/homelab.git --username jason --password <gitea access token>
```

Lay out the GitOps folder:

```
phase5/gitops/
  root.yaml              # the only thing you kubectl apply
  apps/                  # one Argo CD Application per component
    csi-driver-nfs.yaml
    storageclass.yaml
    traefik.yaml
    external-secrets.yaml
    demo.yaml
  manifests/
    storage/             # the StorageClass from Step 6
    demo/                # web deployment, service, NetworkPolicies, ExternalSecret
```

`root.yaml`:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: root
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://gitea.lab.internal/jason/homelab.git
    targetRevision: main
    path: phase5/gitops/apps
  destination:
    server: https://kubernetes.default.svc
    namespace: argocd
  syncPolicy:
    automated: { prune: true, selfHeal: true }
```

A Helm-chart app, `apps/external-secrets.yaml`. Pin `targetRevision` to the chart's current version:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: external-secrets
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://charts.external-secrets.io
    chart: external-secrets
    targetRevision: <chart version>
  destination:
    server: https://kubernetes.default.svc
    namespace: external-secrets
  syncPolicy:
    automated: { prune: true, selfHeal: true }
    syncOptions: [CreateNamespace=true]
```

A Git-folder app, like `apps/demo.yaml`, uses `path: phase5/gitops/manifests/demo` in place of `chart`. Write `csi-driver-nfs.yaml` the same way as external-secrets, so Argo CD adopts the release you installed by hand.

For ingress, write `apps/traefik.yaml` with `repoURL: https://traefik.github.io/charts` and `chart: traefik`. Add these Helm values under `source.helm.valuesObject`:

```yaml
service:
  type: NodePort
ports:
  web:
    nodePort: 30080
```

Then send `*.apps.lab.internal` from lb to the ingress:

1. In Unbound, add a wildcard: `local-zone: "apps.lab.internal." redirect` and `local-data: "apps.lab.internal. A 192.168.1.30"`.
2. Issue a wildcard cert: `step ca certificate '*.apps.lab.internal' apps.crt apps.key --not-after 2160h`.
3. Add an Nginx `server` on lb with `server_name *.apps.lab.internal;` and that cert. Give it `proxy_pass http://k8s_ingress;`, where `k8s_ingress` is an upstream of w1 and w2 on port 30080, and set `proxy_set_header Host $host;`.

Commit, then bootstrap with the only `kubectl apply` you'll need:

```bash
kubectl apply -f phase5/gitops/root.yaml
argocd app list           # everything Synced and Healthy
```

Test self-heal: `kubectl -n demo scale deployment web --replicas=5`, then watch Argo CD put it back to what Git says. Change replicas in Git, push, and watch it roll out.

### Step 8: Pods read secrets from Vault (External Secrets Operator)

In Vault (from admin), set up Kubernetes auth. Vault runs outside the cluster, so it uses each client's own token to check it with the API server:

```bash
kubectl config view --raw --minify -o jsonpath='{.clusters[0].cluster.certificate-authority-data}' | base64 -d > k8s-ca.crt
vault auth enable kubernetes
vault write auth/kubernetes/config \
  kubernetes_host=https://k8s-api.lab.internal:6443 kubernetes_ca_cert=@k8s-ca.crt

vault policy write eso - <<'EOF'
path "lab/data/apps/*" { capabilities = ["read"] }
EOF
vault write auth/kubernetes/role/eso \
  bound_service_account_names=vault-auth bound_service_account_namespaces=demo \
  policies=eso ttl=1h
vault kv put lab/apps/demo password='s3cret-v1'
```

In `manifests/demo/`, add the following. All of it syncs through Argo CD:

- A ServiceAccount `vault-auth` in `demo`.
- A ClusterRoleBinding giving that ServiceAccount the `system:auth-delegator` ClusterRole, so Vault can use its token for the review.
- A ConfigMap `lab-root-ca` in `external-secrets`, with your root cert under key `ca.crt`.
- This store and secret:

```yaml
apiVersion: external-secrets.io/v1
kind: ClusterSecretStore
metadata:
  name: vault
spec:
  provider:
    vault:
      server: https://vault.lab.internal:8200
      path: lab
      version: v2
      caProvider:
        type: ConfigMap
        name: lab-root-ca
        key: ca.crt
        namespace: external-secrets
      auth:
        kubernetes:
          mountPath: kubernetes
          role: eso
          serviceAccountRef:
            name: vault-auth
            namespace: demo
---
apiVersion: external-secrets.io/v1
kind: ExternalSecret
metadata:
  name: demo-db
  namespace: demo
spec:
  refreshInterval: 1m
  secretStoreRef:
    name: vault
    kind: ClusterSecretStore
  target:
    name: demo-db
  data:
    - secretKey: password
      remoteRef:
        key: apps/demo
        property: password
```

Older ESO releases use `apiVersion: external-secrets.io/v1beta1`. Check with `kubectl api-resources | grep external`. Then verify, rotate, and verify again:

```bash
kubectl -n demo get externalsecret demo-db          # SecretSynced
kubectl -n demo get secret demo-db -o jsonpath='{.data.password}' | base64 -d; echo
vault kv put lab/apps/demo password='s3cret-v2'      # wait about 1 minute
kubectl -n demo get secret demo-db -o jsonpath='{.data.password}' | base64 -d; echo
```

### Step 9: Flux on a throwaway cluster

To compare GitOps tools, clone one VM from template 9000 and install single-node k3s (`curl -sfL https://get.k3s.io | sh -`). Create an empty Gitea repo `flux-lab`, then:

```bash
flux bootstrap gitea --hostname=gitea.lab.internal --owner=jason \
  --repository=flux-lab --personal --token-auth --ca-file=lab-root.crt
```

Deploy the same demo app with a Flux `Kustomization`. Write down what each tool does better: UI, multi-tenancy, Helm handling, and how much runs in-cluster. Then destroy the VM.

### Step 10: The 30-minute rebuild

1. Turn Step 2 into Ansible: a `k8s_node` role, plus a `k8s.yml` playbook that runs `kubeadm init` on cp1, joins the other control planes and workers, and installs Cilium.
2. Write `phase5/rebuild.sh`: Terraform apply, wait for SSH, run `k8s.yml`, copy the kubeconfig, add the repo to Argo CD, and apply `root.yaml`.
3. Destroy all six k8s VMs and `time ./rebuild.sh`. Apps, storage and secrets should all come back on their own.
4. Book the CKA. Registration includes two [killer.sh](https://killer.sh) practice sessions; do one on this cluster.

### Done when

- [ ] You've restored etcd from a snapshot and found every Step 3 fault from its symptoms
- [ ] You've upgraded the cluster one minor version
- [ ] NetworkPolicy blocks traffic under Cilium (and you can explain why it didn't under Flannel)
- [ ] `kubectl` keeps working with cp1 powered off
- [ ] A StatefulSet keeps its data after its node dies
- [ ] Every add-on is an Argo CD Application in Git, and self-heal undoes manual changes
- [ ] A secret changed in Vault reaches the pod's Secret within a minute
- [ ] A full rebuild takes under 30 minutes
- [ ] You've passed a CKA practice exam

## Phase 6 runbook: Monitoring, logs and observability

By the end, metrics, logs and traces for the cluster, the VMs and the Proxmox host all land in Grafana, with alerts reaching your phone. Everything is installed as Argo CD Applications in `homelab/phase5/gitops/apps/`, which keeps them in one tree; the apps live in a `monitoring` or `observability` namespace.

### Step 1: Make room

This stack needs about 6 GB more than you have. Either add `w3` (155, .55) to Terraform and join it, or raise w1 and w2 to `memory = 8192` (Terraform resizes them in place; drain each one first). Then add `metrics-server` as an Argo CD app (chart `metrics-server` from `https://kubernetes-sigs.github.io/metrics-server/`, with `args: [--kubelet-insecure-tls]` in its values) so `kubectl top` works.

### Step 2: kube-prometheus-stack

Put Grafana's admin login in Vault, and let ESO create it as a Secret (same pattern as Phase 5 Step 8):

```bash
vault kv put lab/apps/grafana admin-user=admin admin-password="$(openssl rand -base64 18)"
```

Add an ExternalSecret `grafana-admin` in `monitoring` that maps both keys. Then `apps/kube-prometheus-stack.yaml`:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: kube-prometheus-stack
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://prometheus-community.github.io/helm-charts
    chart: kube-prometheus-stack
    targetRevision: <chart version>
    helm:
      valuesObject:
        grafana:
          admin:
            existingSecret: grafana-admin
            userKey: admin-user
            passwordKey: admin-password
          ingress:
            enabled: true
            ingressClassName: traefik
            hosts: [grafana.apps.lab.internal]
        prometheus:
          ingress:
            enabled: true
            ingressClassName: traefik
            hosts: [prometheus.apps.lab.internal]
          prometheusSpec:
            retention: 7d
            serviceMonitorSelectorNilUsesHelmValues: false
            podMonitorSelectorNilUsesHelmValues: false
            ruleSelectorNilUsesHelmValues: false
            probeSelectorNilUsesHelmValues: false
            storageSpec:
              volumeClaimTemplate:
                spec:
                  storageClassName: nfs
                  accessModes: [ReadWriteOnce]
                  resources: { requests: { storage: 10Gi } }
        alertmanager:
          ingress:
            enabled: true
            ingressClassName: traefik
            hosts: [alertmanager.apps.lab.internal]
  destination:
    server: https://kubernetes.default.svc
    namespace: monitoring
  syncPolicy:
    automated: { prune: true, selfHeal: true }
    syncOptions: [CreateNamespace=true, ServerSideApply=true]
```

`ServerSideApply=true` matters, because the chart's CRDs are too big for a normal apply. The four `...NilUsesHelmValues: false` lines let Prometheus pick up ServiceMonitors and rules from any namespace, not only ones labelled for this release. Prometheus on NFS is fine for a lab; in production you'd use local disks.

Open `https://prometheus.apps.lab.internal/targets`. Some targets will be **down**: kube-scheduler, kube-controller-manager, etcd and kube-proxy. kubeadm binds their metrics to `127.0.0.1`. Fixing it is good practice:

- On each control-plane node, edit `/etc/kubernetes/manifests/kube-scheduler.yaml` and `kube-controller-manager.yaml` to set `--bind-address=0.0.0.0`.
- In `etcd.yaml`, set `--listen-metrics-urls=http://0.0.0.0:2381`.
- For kube-proxy, run `kubectl -n kube-system edit cm kube-proxy`, set `metricsBindAddress: 0.0.0.0:10249`, then restart the kube-proxy pods.

Fix the kubeadm config too, so a rebuild keeps the changes.

### Step 3: Watch the VMs and the Proxmox host

**node_exporter everywhere.** Add the Prometheus Ansible collection and a role to `site.yml`:

```bash
ansible-galaxy collection install prometheus.prometheus
```

```yaml
- hosts: all
  become: true
  roles: [prometheus.prometheus.node_exporter]
```

On the Proxmox host itself, run `apt install prometheus-node-exporter`. Open port 9100 to the cluster nodes in each VM's Proxmox firewall file: `IN ACCEPT -source 192.168.1.48/28 -p tcp -dport 9100`.

**Proxmox metrics.** Create a second read-only token for the exporter: `pveum user token add automation@pve exporter --privsep 0`. Store it in Vault at `lab/apps/pve-exporter`. Then deploy [prometheus-pve-exporter](https://github.com/prometheus-pve/prometheus-pve-exporter) to `monitoring` as a Deployment and Service (`pve-exporter`, port 9221). Its config file `/etc/prometheus/pve.yml` comes from an ExternalSecret:

```yaml
default:
  user: automation@pve
  token_name: exporter
  token_value: <from Vault>
  verify_ssl: false
```

Then add scrape jobs to the kube-prometheus-stack values, under `prometheus.prometheusSpec.additionalScrapeConfigs`:

```yaml
- job_name: lab-vms
  static_configs:
    - targets:
        - pve.lab.internal:9100
        - lb.lab.internal:9100
        - web1.lab.internal:9100
        - web2.lab.internal:9100
        - runner.lab.internal:9100
        - harbor.lab.internal:9100
        - vault1.lab.internal:9100
        - vault2.lab.internal:9100
        - vault3.lab.internal:9100
- job_name: pve
  metrics_path: /pve
  params:
    module: [default]
    cluster: ['1']
    node: ['1']
  static_configs:
    - targets: [pve.lab.internal]
  relabel_configs:
    - source_labels: [__address__]
      target_label: __param_target
    - source_labels: [__param_target]
      target_label: instance
    - target_label: __address__
      replacement: pve-exporter.monitoring.svc:9221
```

The relabeling is the "exporter pattern": Prometheus scrapes the exporter, and the exporter queries the target you name.

### Step 4: An app worth watching, and PromQL drills

Replace the plain nginx demo with [podinfo](https://github.com/stefanprodan/podinfo). It has endpoints that return errors (`/status/500`) and slow responses (`/delay/2`), which is exactly what you need to see the golden signals. Deploy it in `demo` with an Ingress at `demo.apps.lab.internal`, and turn on Traefik's metrics ServiceMonitor in the Traefik values:

```yaml
metrics:
  prometheus:
    serviceMonitor:
      enabled: true
```

Generate traffic from admin, mixing good, slow and failing requests:

```bash
sudo apt install -y hey
hey -z 10m -c 10 https://demo.apps.lab.internal/ &
hey -z 10m -c 2 https://demo.apps.lab.internal/delay/1 &
hey -z 10m -c 1 https://demo.apps.lab.internal/status/500 &
```

Run each query in Prometheus, and say out loud what it means before you move on:

| Question | PromQL |
| --- | --- |
| What's down? | `up == 0` |
| CPU busy % per host | `100 * (1 - avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])))` |
| Memory available % | `100 * node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes` |
| Disk free % | `100 * node_filesystem_avail_bytes{fstype!~"tmpfs\|overlay"} / node_filesystem_size_bytes{fstype!~"tmpfs\|overlay"}` |
| Root disk full within 4 hours? | `predict_linear(node_filesystem_avail_bytes{mountpoint="/"}[1h], 4*3600) < 0` |
| rate against irate | Graph `rate(node_network_receive_bytes_total[5m])` and `irate(node_network_receive_bytes_total[5m])` together |
| Traffic (golden signal) | `sum by (service) (rate(traefik_service_requests_total[5m]))` |
| Errors (golden signal) | `sum by (service) (rate(traefik_service_requests_total{code=~"5.."}[5m])) / sum by (service) (rate(traefik_service_requests_total[5m]))` |
| Latency p95 (golden signal) | `histogram_quantile(0.95, sum by (le, service) (rate(traefik_service_request_duration_seconds_bucket[5m])))` |
| Saturation (golden signal) | `sum by (pod) (rate(container_cpu_usage_seconds_total{namespace="demo"}[5m]))` |
| Pods restarting | `increase(kube_pod_container_status_restarts_total[1h]) > 0` |
| CPU throttling | `rate(container_cpu_cfs_throttled_periods_total[5m]) / rate(container_cpu_cfs_periods_total[5m])` |

### Step 5: Dashboards as code

The chart's Grafana loads any ConfigMap labelled `grafana_dashboard: "1"`. For each dashboard:

1. Build it in the Grafana UI, or import a community one by ID: **1860** (Node Exporter Full) and **10347** (Proxmox via the PVE exporter) are good starting points.
2. Export it with Share > Export > *Export for sharing externally* off, and save the JSON to `manifests/monitoring/dashboards/`.
3. Wrap it in a ConfigMap with the label above. Use a Kustomize `configMapGenerator`, so the JSON stays a plain file.
4. Push, and let Argo CD sync it. Delete the dashboard in the UI and watch it come back.

Make three: **Host** (Proxmox host plus VMs), **Cluster** (nodes, pods, restarts, PVCs) and **App** (the four golden signals for `demo`).

### Step 6: Alerts that reach you

Use a free Discord (or Slack) channel webhook as your test channel. Store the URL in Vault, sync it with ESO into a Secret `alertmanager-discord` in `monitoring`, and add to the chart values:

```yaml
alertmanager:
  alertmanagerSpec:
    secrets: [alertmanager-discord]
  config:
    route:
      receiver: discord
      group_by: [alertname, instance]
      routes:
        - receiver: 'null'
          matchers: ['alertname = "Watchdog"']
    receivers:
      - name: 'null'
      - name: discord
        discord_configs:
          - webhook_url_file: /etc/alertmanager/secrets/alertmanager-discord/url
```

For cert checks, add the `prometheus-blackbox-exporter` chart (same Helm repo) and a `Probe` for each HTTPS endpoint. Then write your rules as a `PrometheusRule` in Git:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: lab-alerts
  namespace: monitoring
spec:
  groups:
    - name: lab
      rules:
        - alert: LabHostDown
          expr: up{job="lab-vms"} == 0
          for: 2m
          labels: { severity: critical }
          annotations:
            summary: "{{ $labels.instance }} has been down for 2 minutes"
        - alert: DiskAlmostFull
          expr: 100 * node_filesystem_avail_bytes{fstype!~"tmpfs|overlay"} / node_filesystem_size_bytes{fstype!~"tmpfs|overlay"} < 15
          for: 5m
          labels: { severity: warning }
          annotations:
            summary: "{{ $labels.instance }} {{ $labels.mountpoint }} is over 85% full"
        - alert: CertExpiringSoon
          expr: (probe_ssl_earliest_cert_expiry - time()) / 86400 < 14
          for: 10m
          labels: { severity: warning }
          annotations:
            summary: "Cert for {{ $labels.instance }} expires in under 14 days"
```

There's a catch to find: your ACME certs from step-ca last 24 hours, so a 14-day rule fires for them all the time. Split the rule. Use 14 days for the 90-day certs (Harbor, Vault, `*.apps`) and about 6 hours for the 24-hour ones, which also proves renewal is working.

Fire each alert on purpose:

1. `sudo systemctl stop prometheus-node-exporter` on web1, and wait 2 minutes.
2. `fallocate -l <size> /var/tmp/big.bin` on web2, until it's over 85% full.
3. Point a Probe at a site using a cert issued with `--not-after 3h`.

Check each one in the Alertmanager UI, then in Discord. Then clean up and watch the resolved messages arrive.

### Step 7: Logs with Loki and Alloy

`apps/loki.yaml`: chart `loki` from `https://grafana.github.io/helm-charts`, in single-binary mode. The chart's values change between major versions, so check them against the [Loki Helm docs](https://grafana.com/docs/loki/latest/setup/install/helm/install-monolithic/) for your chart version:

```yaml
deploymentMode: SingleBinary
loki:
  auth_enabled: false
  commonConfig:
    replication_factor: 1
  storage:
    type: filesystem
  schemaConfig:
    configs:
      - from: "2024-04-01"
        store: tsdb
        object_store: filesystem
        schema: v13
        index: { prefix: loki_index_, period: 24h }
singleBinary:
  replicas: 1
  persistence: { storageClass: nfs, size: 10Gi }
backend: { replicas: 0 }
read: { replicas: 0 }
write: { replicas: 0 }
chunksCache: { enabled: false }
resultsCache: { enabled: false }
```

`apps/alloy.yaml`: chart `alloy` from the same repo, run as a DaemonSet. It reads pod logs through the Kubernetes API, so it needs no host paths. Values:

```yaml
alloy:
  configMap:
    content: |
      discovery.kubernetes "pods" {
        role = "pod"
      }
      discovery.relabel "pods" {
        targets = discovery.kubernetes.pods.targets
        rule {
          source_labels = ["__meta_kubernetes_namespace"]
          target_label  = "namespace"
        }
        rule {
          source_labels = ["__meta_kubernetes_pod_name"]
          target_label  = "pod"
        }
        rule {
          source_labels = ["__meta_kubernetes_pod_container_name"]
          target_label  = "container"
        }
      }
      loki.source.kubernetes "pods" {
        targets    = discovery.relabel.pods.output
        forward_to = [loki.write.default.receiver]
      }
      loki.write "default" {
        endpoint {
          url = "http://loki-gateway.monitoring.svc/loki/api/v1/push"
        }
      }
```

**VM logs.** Give Loki's gateway an Ingress at `loki.apps.lab.internal`. Then install Alloy on every VM with Ansible, using the `grafana.grafana.alloy` role, and give it this config to ship the systemd journal:

```
loki.source.journal "system" {
  forward_to = [loki.write.default.receiver]
  labels     = { job = "journal", host = constants.hostname }
}
loki.write "default" {
  endpoint {
    url = "https://loki.apps.lab.internal/loki/api/v1/push"
  }
}
```

Add Loki to Grafana in the kube-prometheus-stack values:

```yaml
grafana:
  additionalDataSources:
    - name: Loki
      type: loki
      url: http://loki-gateway.monitoring.svc
```

Turn on Traefik's JSON access logs (`logs.access.enabled: true` and `logs.access.format: json` in its values). Then practice LogQL in Grafana's Explore view:

| Question | LogQL |
| --- | --- |
| Errors in the demo app | `{namespace="demo"} \|= "error"` |
| Log volume per pod | `sum by (pod) (rate({namespace="demo"}[5m]))` |
| Your Phase 1 timer on web1 | `{job="journal", host="web1"} \|= "diskreport"` |
| 5xx responses at the edge | `{namespace="traefik"} \| json \| DownstreamStatus >= 500` |
| Slow requests | `{namespace="traefik"} \| json \| Duration > 1000000000` |

Then the Phase 1 incident, from logs alone. On web1, run `stress-ng --vm 1 --vm-bytes 120% --timeout 120` so the kernel's OOM killer fires. Without SSHing in, find which host, when, and which process with `{job="journal"} |= "Out of memory"`.

### Step 8: Traces with OpenTelemetry and Jaeger

Deploy two things in an `observability` namespace through Argo CD:

- **Jaeger.** A Deployment of the all-in-one `jaegertracing/jaeger` image (v2), in-memory, plus a Service exposing 16686 (UI) and 4317 (OTLP gRPC). Add an Ingress at `jaeger.apps.lab.internal`.
- **OpenTelemetry Collector.** Chart `opentelemetry-collector` from `https://open-telemetry.github.io/opentelemetry-helm-charts`:

    ```yaml
    mode: deployment
    image:
      repository: otel/opentelemetry-collector-contrib
    config:
      receivers:
        otlp:
          protocols:
            grpc: { endpoint: 0.0.0.0:4317 }
            http: { endpoint: 0.0.0.0:4318 }
      exporters:
        otlp/jaeger:
          endpoint: jaeger.observability.svc:4317
          tls: { insecure: true }
      service:
        pipelines:
          traces:
            receivers: [otlp]
            processors: [batch]
            exporters: [otlp/jaeger]
    ```

Write a small service that calls podinfo, in `homelab/apps/orders/app.py`:

```python
import logging
import random
import time

import requests
from flask import Flask

logging.basicConfig(level=logging.INFO)
app = Flask(__name__)


@app.get("/order")
def order():
    time.sleep(random.uniform(0.01, 0.2))  # pretend work
    delay = random.choice([0, 0, 0, 1])     # sometimes slow
    upstream = requests.get(f"http://podinfo.demo.svc:9898/delay/{delay}", timeout=5)
    if random.random() < 0.05:
        logging.error("payment failed")
        return {"error": "payment failed"}, 500
    return {"status": "ok", "upstream": upstream.status_code}
```

Instrument it with no code changes. In its Dockerfile:

```dockerfile
RUN pip install flask requests opentelemetry-distro opentelemetry-exporter-otlp \
 && opentelemetry-bootstrap -a install
ENV OTEL_SERVICE_NAME=orders \
    OTEL_EXPORTER_OTLP_ENDPOINT=http://opentelemetry-collector.observability.svc:4318 \
    OTEL_PYTHON_LOGGING_AUTO_INSTRUMENTATION_ENABLED=true \
    OTEL_PYTHON_LOG_CORRELATION=true
CMD ["opentelemetry-instrument", "flask", "--app", "app", "run", "--host", "0.0.0.0", "--port", "8080"]
```

Check the Collector's Service name with `kubectl -n observability get svc`, and fix the endpoint if it differs. Build the image through your Phase 4 pipeline, push it to Harbor, and deploy it with Argo CD at `orders.apps.lab.internal`. Point `hey` at `/order`.

Then connect the three signals in Grafana:

1. Add a Jaeger data source (`http://jaeger.observability.svc:16686`).
2. On the Loki data source, add a **derived field** that matches `trace_id=(\w+)` and links to the Jaeger data source.
3. Walk it: the App dashboard shows a 5xx spike, Explore in Loki finds `payment failed`, the trace ID link opens the trace in Jaeger, and the span shows where the time went.

Optional: run single-node OpenSearch (or Elastic) with the same logs, and compare `kubectl top pod` for it against Loki. Swapping Jaeger for Grafana Tempo is another good comparison.

### Done when

- [ ] Every target on Prometheus's Targets page is up, including the control plane, the VMs and the Proxmox host
- [ ] You can write each PromQL query in the table from memory
- [ ] Three dashboards live in Git and come back if deleted
- [ ] All three alerts have fired on purpose and reached Discord, then resolved
- [ ] Pod logs and VM journals are both searchable in Loki
- [ ] You found the OOM kill from logs alone
- [ ] You can go from a metric spike to a log line to a trace span without SSHing anywhere

## Phase 7 runbook: Service mesh and design patterns

By the end, the `orders` app from Phase 6 runs inside a service mesh with mTLS and a canary, has published SLOs with burn-rate alerts, and has survived three game days, each with a postmortem in Gitea. Its data can be restored from backup.

### Step 1: Linkerd

The open-source Linkerd project now publishes **edge** releases; Buoyant ships the stable ones. Edge is fine for a lab. On admin:

```bash
curl --proto '=https' --tlsv1.2 -sSfL https://run.linkerd.io/install-edge | sh
export PATH=$PATH:$HOME/.linkerd2/bin
linkerd check --pre
linkerd install --crds | kubectl apply -f -
linkerd install | kubectl apply -f -
linkerd check
linkerd viz install | kubectl apply -f -
linkerd viz check
```

Once it works, move it into Argo CD with the `linkerd-crds` and `linkerd-control-plane` Helm charts. They need a trust anchor and an issuer cert, which you make with the step CLI you already know:

```bash
step certificate create root.linkerd.cluster.local ca.crt ca.key \
  --profile root-ca --no-password --insecure
step certificate create identity.linkerd.cluster.local issuer.crt issuer.key \
  --profile intermediate-ca --not-after 8760h --no-password --insecure \
  --ca ca.crt --ca-key ca.key
```

Store the issuer key in Vault, deliver it with ESO, and keep `ca.key` offline.

**Mesh the demo namespace.** Put the annotation in Git (on the `demo` Namespace manifest), then restart the workloads:

```yaml
metadata:
  annotations:
    linkerd.io/inject: enabled
```

```bash
kubectl -n demo rollout restart deploy
linkerd viz stat deploy -n demo           # success rate, RPS, latency per deployment
linkerd viz edges deploy -n demo          # SECURED = mTLS between every pair
linkerd viz tap deploy/orders -n demo     # live requests
```

You get golden metrics for every meshed service without touching app code. Compare them with your Phase 6 Traefik numbers.

### Step 2: Retries, timeouts and a canary

**Retries and timeouts.** Add these annotations to the `podinfo` Service in Git:

```yaml
metadata:
  annotations:
    retry.linkerd.io/http: 5xx
    retry.linkerd.io/limit: "2"
    timeout.linkerd.io/request: 2s
    balancer.linkerd.io/failure-accrual: consecutive
```

The last line is Linkerd's circuit breaker: after a run of failures, it stops sending to that pod for a while. Check the annotation names against the [Linkerd docs](https://linkerd.io/2-edge/reference/) for your version.

**Canary.** Run two podinfo Deployments behind their own Services: `podinfo-stable`, and `podinfo-canary` started with `--random-error` so some of its requests fail. Keep the original `podinfo` Service as the name callers use. Then split the traffic with an HTTPRoute:

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: podinfo-split
  namespace: demo
spec:
  parentRefs:
    - name: podinfo
      kind: Service
      group: ""
      port: 9898
  rules:
    - backendRefs:
        - name: podinfo-stable
          port: 9898
          weight: 90
        - name: podinfo-canary
          port: 9898
          weight: 10
```

The split applies to meshed callers, so watch it from `orders`: `linkerd viz stat deploy -n demo` shows the canary's success rate falling. Move the weights to 50/50, then 0/100 for the canary, all through Git.

Stretch, which leads into Capstone 2: install Flagger with its Linkerd provider and let it run that promotion on its own, rolling back when the success rate drops.

**Compare with Istio.** On a throwaway k3s VM with 8 GB, run `istioctl install --set profile=demo -y` and mesh the same demo. Compare `kubectl top pod -n istio-system` with `-n linkerd`, and count the steps each one took.

### Step 3: SLOs and burn-rate alerts with Sloth

First, make the orders error rate something you control. Change the failure line in `app.py` to `random.random() < float(os.getenv("ERROR_RATE", "0.002"))` (and add `import os`), then redeploy. At 0.2% failures the app is inside its budget; you'll raise it on purpose later.

Add Sloth as an Argo CD app: chart `sloth` from `https://slok.github.io/sloth`. Then write the SLOs as a resource in Git:

```yaml
apiVersion: sloth.slok.dev/v1
kind: PrometheusServiceLevel
metadata:
  name: orders
  namespace: monitoring
spec:
  service: orders
  labels:
    owner: jason
  slos:
    - name: availability
      objective: 99.5
      description: "99.5% of order requests succeed"
      sli:
        events:
          errorQuery: sum(rate(traefik_service_requests_total{service=~"demo-orders.*",code=~"5.."}[{{.window}}]))
          totalQuery: sum(rate(traefik_service_requests_total{service=~"demo-orders.*"}[{{.window}}]))
      alerting:
        name: OrdersAvailabilityBurn
        pageAlert:
          labels: { severity: critical }
        ticketAlert:
          labels: { severity: warning }
    - name: latency
      objective: 99
      description: "99% of order requests finish in under 300 ms"
      sli:
        events:
          errorQuery: >-
            sum(rate(traefik_service_request_duration_seconds_count{service=~"demo-orders.*"}[{{.window}}]))
            - sum(rate(traefik_service_request_duration_seconds_bucket{service=~"demo-orders.*",le="0.3"}[{{.window}}]))
          totalQuery: sum(rate(traefik_service_request_duration_seconds_count{service=~"demo-orders.*"}[{{.window}}]))
      alerting:
        name: OrdersLatencyBurn
        pageAlert:
          labels: { severity: critical }
        ticketAlert:
          labels: { severity: warning }
```

Check the exact `service` label with `traefik_service_requests_total` in Prometheus first, and adjust the regex. `0.3` works because it's one of Traefik's default histogram buckets.

Sloth turns each SLO into recording rules and multi-window burn-rate alerts. A fast burn (the whole month's budget gone in about 2 days) pages; a slow burn opens a ticket. Read the PrometheusRule it generates (`kubectl -n monitoring get prometheusrule`) until you can explain each window pair. Import the Sloth Grafana dashboards (IDs **14348** and **14643**) into Git the same way as in Phase 6.

**Test it.** Set `ERROR_RATE=0.1` (10% failures) and run `hey` against `/order`. Within minutes, the page alert should fire to Discord. Set it back and watch it resolve. Then work out how much of the month's error budget that test used.

### Step 4: Game days

Run one scenario per session. For each: write down what you expect, start a timer, break it, and note when you **detected** it (alert fired, or you noticed) and when you **recovered**. Take Proxmox snapshots first.

| Scenario | How to break it | Things to watch |
| --- | --- | --- |
| Lose a worker | `qm stop 153` on the host | Pod rescheduling, the StatefulSet behavior from Phase 5, SLO burn |
| Lose the NAS | Untick **Connected** on the NAS VM's network device in Proxmox | NFS-backed pods, Prometheus, Loki. What does your monitoring see when its own storage is gone? |
| Fill a control-plane disk | On cp1: `sudo fallocate -l <size> /var/fill.bin` until under 10% free | Kubelet disk-pressure taints, evictions, etcd health, which alert fires first |
| (Bonus) CA down | `systemctl stop step-ca` for 24 hours | Which 24-hour certs fail to renew, and whether your cert alert catches it first |

After each one, write a postmortem in `homelab/postmortems/YYYY-MM-DD-<name>.md`:

```markdown
# Postmortem: <title>

**Date:** · **Duration:** · **Severity:**

## Summary
Two sentences: what broke, what users saw.

## Impact
Requests failed, SLO budget used (from the Sloth dashboard).

## Timeline
| Time | Event |
| --- | --- |
| 19:02 | Worker w1 powered off |
| 19:04 | LabHostDown fired |

## Detection
How you found out, and time to detect.

## Root cause

## What went well / what didn't

## Action items
- [ ] <change>, owner, due date
```

Then do the action items. The NAS scenario almost always produces one about where your monitoring stores its data.

### Step 5: Design patterns on your own stack

**Health and resilience for `orders`:**

1. Add a `/healthz` endpoint, plus `readinessProbe` and `livenessProbe` that use it.
2. Run 3 replicas with `topologySpreadConstraints` across nodes, and add a PodDisruptionBudget (`minAvailable: 2`). Drain a node and confirm it never drops below 2.
3. Add a HorizontalPodAutoscaler on CPU (70%). Load it with `hey` and watch `kubectl get hpa -w`.

**Queue-based load leveling with NATS JetStream.** Add the `nats` chart (`https://nats-io.github.io/k8s/helm/charts/`) with JetStream enabled. Change `orders` to publish each order instead of doing the work inline, and add a `worker` Deployment that pulls at a steady pace:

```python
# in orders: publish and return right away
import json
import nats

nc = await nats.connect("nats://nats.messaging.svc:4222")
js = nc.jetstream()
await js.add_stream(name="ORDERS", subjects=["orders.*"])
await js.publish("orders.created", json.dumps(order).encode())

# in worker: pull in small batches and ack each one
sub = await js.pull_subscribe("orders.created", durable="worker")
while True:
    try:
        for msg in await sub.fetch(10, timeout=5):
            process(json.loads(msg.data))
            await msg.ack()
    except nats.errors.TimeoutError:
        pass
```

These are `async` snippets, so run them under `asyncio` (switch `orders` to an async framework, or keep one event loop per process). Send a burst 10 times bigger than the worker can handle. Requests stay fast while the queue grows and then drains. Graph queue depth in Grafana from the NATS exporter.

**Backup and restore with Velero.** On SeaweedFS, create a `velero` bucket, then write a credentials file and install Velero from admin:

```bash
cat > credentials-velero <<'EOF'
[default]
aws_access_key_id=<ACCESS_KEY>
aws_secret_access_key=<SECRET_KEY>
EOF

velero install \
  --provider aws \
  --plugins velero/velero-plugin-for-aws:<current version> \
  --bucket velero \
  --secret-file ./credentials-velero \
  --backup-location-config region=us-east-1,s3ForcePathStyle=true,s3Url=http://s3.lab.internal:8333,checksumAlgorithm="" \
  --use-node-agent --default-volumes-to-fs-backup
```

The empty `checksumAlgorithm` stops newer AWS SDKs from sending checksums that some S3-compatible stores reject. Then test a restore:

```bash
velero backup create demo-1 --include-namespaces demo --wait
# turn off auto-sync for the demo app in Argo CD first, then:
kubectl delete namespace demo
velero restore create --from-backup demo-1 --wait
kubectl -n demo exec writer-0 -- tail /data/log   # the StatefulSet's old log is back
velero schedule create nightly --schedule "0 3 * * *" --ttl 168h
```

The lesson to write down: Argo CD restores **configuration** from Git, but only a backup restores **data**. You need both.

### Step 6: Take it back to Azure

For each pattern, write the Azure service you'd use at work, and one thing the lab showed you that the managed service hides:

| Pattern | In the lab | Azure equivalent |
| --- | --- | --- |
| Load balancing and failover | Nginx LB | Application Gateway, Azure Load Balancer |
| mTLS, retries, canary | Linkerd | Istio add-on for AKS |
| SLOs and burn-rate alerts | Prometheus + Sloth | Azure Monitor managed Prometheus + alert rules |
| Logs | Loki | Log Analytics |
| Traces | OpenTelemetry + Jaeger | Application Insights (OpenTelemetry distro) |
| Secrets into pods | Vault + ESO | Key Vault + Secrets Store CSI driver, workload identity |
| Backup and restore | Velero | Azure Backup for AKS |
| Queue-based load leveling | NATS JetStream | Service Bus |
| GitOps | Argo CD | AKS GitOps (Flux extension) |
| Infrastructure as code | Terraform | Bicep |

This table, with your notes added, makes a good one-page write-up for the observability proposal at work.

### Done when

- [ ] `linkerd viz edges` shows every demo connection as SECURED
- [ ] You moved a canary from 10% to 100% through Git, and saw a bad canary in the metrics
- [ ] `orders` has two published SLOs, and the page alert fired during a test
- [ ] Three game days are done, with three postmortems in Gitea and their action items closed
- [ ] A deleted namespace came back with its data from a Velero backup
- [ ] The Azure mapping table is filled in from your own experience

# Sources

- [roadmap.sh DevOps roadmap](https://roadmap.sh/devops): page text and topic framing
- [kamranahmedse/developer-roadmap on GitHub](https://github.com/kamranahmedse/developer-roadmap): the 140 DevOps topic files and their linked resources, cloned 2026-11-05
- [bpg/proxmox Terraform provider](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) · [Proxmox VE API](https://pve.proxmox.com/wiki/Proxmox_VE_API) · [Google SRE book](https://sre.google/sre-book/table-of-contents/): added beyond the roadmap's own links

