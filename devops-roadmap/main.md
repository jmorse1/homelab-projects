# DevOps Roadmap Homelab Study Guide

Nov 5, 2026 · @Jason Morse

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

&#91;embedded content: target lab layout · one Proxmox host, 4 tiers\]

Argo CD in the cluster pulls its manifests from Gitea. DNS and the internal CA serve every box.

**Resource budget.** Your 3 nodes at 2 CPU / 4 GB each are enough for Phases 1 to 5. Phase 6 (Prometheus, Loki, Grafana) and Phase 7 (a service mesh) need more. Before then, raise workers to 8 GB or add a fourth node from the golden image. Plan on about 10 to 12 GB more for the platform VMs: Harbor about 4 GB, Vault about 1 GB per node, a 2 GB CI runner, a 1 GB load balancer. The LXCs need under 512 MB each.

**Snapshot rules.** Take a named snapshot before each phase (for example `pre-phase3`) and before any exercise marked "break". Keep your clean-state cluster snapshot untouched as the reset point.

**Open question:** how much CPU, RAM and disk does the Proxmox host have? That decides whether Phases 6 and 7 fit at the same time or need to take turns.

## Modules

Seven phases, in roadmap order. Each one leaves something running that the next phase builds on.

Step-by-step commands for each phase are in Runbooks.

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

## Sources

- [roadmap.sh DevOps roadmap](https://roadmap.sh/devops): page text and topic framing
- [kamranahmedse/developer-roadmap on GitHub](https://github.com/kamranahmedse/developer-roadmap): the 140 DevOps topic files and their linked resources, cloned 2026-11-05
- [bpg/proxmox Terraform provider](https://registry.terraform.io/providers/bpg/proxmox/latest/docs) · [Proxmox VE API](https://pve.proxmox.com/wiki/Proxmox_VE_API) · [Google SRE book](https://sre.google/sre-book/table-of-contents/): added beyond the roadmap's own links

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
