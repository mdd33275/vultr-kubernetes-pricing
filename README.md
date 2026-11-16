# Vultr Kubernetes Pricing: Is the Control Plane Free, What Does a 3-Node Cluster Cost, and Is HA Extra? (Full Plan Table and the Limits Nobody Quotes)

Vultr Kubernetes Engine's control plane costs **$0**. Your bill comes from worker nodes, load balancers and block storage. A one-node lab cluster starts at **$10/month** on a 2 GB Cloud Compute instance. A three-node cluster with 4 GB per node costs **$60/month** on Cloud Compute or **$72/month** on High Performance, and a basic load balancer adds **$10–12/month** on top.

What follows is the full worker-node price list, three worked monthly bills, the reason the $2.50 VPS can't join a cluster, and four limits that decide whether VKE fits your setup at all.

> **Quick pick.** Most small teams should run 3× `vc2-2c-4gb` at $20/month each plus one load balancer, roughly $70–72/month all in. Pick 3× `vhp-2c-4gb` at $24 each when pods are latency-sensitive or you've been burned by shared-CPU throttling. A learning cluster is 1× `vc2-1c-2gb` at $10.
> 👉 [Check current Vultr Cloud Compute pricing](https://www.vultr.com/pricing/?ref=9738262-9J)

## What VKE bills you for

Vultr manages the control plane, meaning the API server, etcd with encryption and backups, and cluster networking. Its cost documentation lists three billable items: worker nodes, Vultr Load Balancers and Block Storage volumes. There is no line item for the cluster itself.

Worker nodes are ordinary Cloud Compute instances, so the plan names and prices match what you'd pay for a VPS. VKE requires **at least 2 GB RAM per node**, which removes the cheapest tiers from consideration. Two costs arrive later: a load balancer at roughly $10–12/month for a basic one, created automatically when you deploy a Service of type `LoadBalancer`, and block storage at **$0.10/GB-month** if you attach volumes beyond the disk included with the node plan. Outbound transfer beyond the plan's allowance runs $0.01/GB, and the included allowance ranges from 512 GB to 8,192 GB depending on the plan.

## Every worker-node plan Vultr sells

### Cloud Compute (shared CPU)

| Plan | vCPU / RAM | Monthly | Order |
| --- | --- | --- | --- |
| `vc2-1c-0.5gb-v6` | 1 / 0.5 GB | $2.50 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-1c-0.5gb` | 1 / 0.5 GB | $3.50 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-1c-1gb` | 1 / 1 GB | $5.00 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-1c-2gb` | 1 / 2 GB | $10.00 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-2c-2gb` | 2 / 2 GB | $15.00 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-2c-4gb` | 2 / 4 GB | $20.00 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-4c-8gb` | 4 / 8 GB | $40.00 | [Deploy](https://bit.ly/VuLtr) |
| `vc2-6c-16gb` | 6 / 16 GB | $80.00 | [Deploy](https://bit.ly/VuLtr) |

The first three rows are below VKE's 2 GB minimum and cannot serve as worker nodes.

### High Frequency

| Plan | vCPU / RAM | Monthly | Order |
| --- | --- | --- | --- |
| `vhf-1c-1gb` | 1 / 1 GB | $6.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhf-1c-2gb` | 1 / 2 GB | $12.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhf-2c-2gb` | 2 / 2 GB | $18.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhf-2c-4gb` | 2 / 4 GB | $24.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhf-3c-8gb` | 3 / 8 GB | $48.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhf-4c-16gb` | 4 / 16 GB | $96.00 | [Deploy](https://bit.ly/VuLtr) |

### High Performance (AMD and Intel at the same price)

| Plan | vCPU / RAM | Monthly | Order |
| --- | --- | --- | --- |
| `vhp-1c-1gb-amd` / `-intel` | 1 / 1 GB | $6.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-1c-2gb-amd` / `-intel` | 1 / 2 GB | $12.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-2c-2gb-amd` / `-intel` | 2 / 2 GB | $18.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-2c-4gb-amd` / `-intel` | 2 / 4 GB | $24.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-4c-8gb-amd` / `-intel` | 4 / 8 GB | $48.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-4c-12gb-amd` / `-intel` | 4 / 12 GB | $72.00 | [Deploy](https://bit.ly/VuLtr) |
| `vhp-8c-16gb-amd` / `-intel` | 8 / 16 GB | $96.00 | [Deploy](https://bit.ly/VuLtr) |

### Optimized Cloud Compute

| Plan | vCPU / RAM | Monthly | Order |
| --- | --- | --- | --- |
| `voc-c-1c-2gb-25s-amd` | 1 / 2 GB | $28.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-g-1c-4gb-30s-amd` | 1 / 4 GB | $30.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-m-1c-8gb-50s-amd` | 1 / 8 GB | $40.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-2c-4gb-50s-amd` | 2 / 4 GB | $40.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-2c-4gb-75s-amd` | 2 / 4 GB | $45.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-g-2c-8gb-50s-amd` | 2 / 8 GB | $60.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-s-1c-8gb-150s-amd` | 1 / 8 GB | $75.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-m-2c-16gb-100s-amd` | 2 / 16 GB | $80.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-4c-8gb-75s-amd` | 4 / 8 GB | $80.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-4c-8gb-150s-amd` | 4 / 8 GB | $90.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-m-2c-16gb-200s-amd` | 2 / 16 GB | $100.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-g-4c-16gb-80s-amd` | 4 / 16 GB | $120.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-m-2c-16gb-400s-amd` | 2 / 16 GB | $125.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-s-2c-16gb-320s-amd` | 2 / 16 GB | $125.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-s-2c-16gb-480s-amd` | 2 / 16 GB | $155.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-8c-16gb-150s-amd` | 8 / 16 GB | $160.00 | [Deploy](https://bit.ly/VuLtr) |
| `voc-c-8c-16gb-300s-amd` | 8 / 16 GB | $180.00 | [Deploy](https://bit.ly/VuLtr) |

## How much does a cluster cost per month?

Three setups cover most of what people actually deploy.

| Setup | Nodes | Node cost | Load balancer | Monthly total |
| --- | --- | --- | --- | --- |
| Lab | 1× `vc2-1c-2gb` | $10 | none until you expose a service | $10 |
| Lab with a public service | 1× `vc2-1c-2gb` | $10 | $10–12 | $20–22 |
| Small production, Cloud Compute | 3× `vc2-2c-4gb` | $60 | $10–12 | $70–72 |
| Small production, High Performance | 3× `vhp-2c-4gb` | $72 | $10–12 | $82–84 |

Add block storage at $0.10/GB-month for any persistent volume you attach, and watch egress only if you push serious traffic: the `vc2-2c-4gb` plan includes 3,072 GB of transfer, with another 2,048 GB credited to the account, so a typical API or web workload lands at $0 in overage.

A single node is enough to learn on, but it also means every pod goes down when that node does. The production number worth remembering is three nodes, and odd counts matter for etcd quorum. Vultr's own HA guide takes a softer line and recommends at least two worker nodes to avoid downtime.

👉 [Start a lab cluster on the $10 2 GB plan](https://bit.ly/VuLtr)

## Why the $2.50 VPS can't be a worker node

The $2.50 and $3.50 plans carry 0.5 GB of RAM, and the $5 and $6 plans carry 1 GB. VKE's floor is 2 GB per node, so the cheapest plan that can actually join a cluster is **`vc2-1c-2gb` at $10/month**, with 55 GB of disk.

Note that $10 is lower than the $12 figure most VKE guides quote as the entry point. Both numbers are correct; they describe different instance families. The $12 buys a High Performance or High Frequency node with NVMe storage and a faster clock, while the $10 buys a Regular Cloud Compute node on shared CPU. The same split applies at the production tier: three 4 GB Cloud Compute nodes cost $60/month, three 4 GB High Performance nodes cost $72/month.

Which one to order depends on what runs inside. Vultr-focused setup guides recommend High Performance as the default for Kubernetes and warn that Regular Cloud Compute instances share CPU and can be throttled, which shows up as latency spikes under load rather than as an error message. For a lab, the $10 node is fine. For anything serving users, the extra $2 per node ($6/month across three nodes) buys storage and scheduling behavior that you won't have to debug later. High Frequency suits database-heavy pods, and Dedicated CPU plans are for workloads where any variance in CPU time breaks things.

## What VKE manages, and the four limits that decide the fit

VKE holds CNCF Kubernetes Conformance certification, which means it passes the upstream test suite and works with standard tooling. As of June 2026 it supported Kubernetes v1.36, v1.35 and v1.34, with Calico as the default CNI. Clusters support multiple node pools, a Cluster Autoscaler that scales each pool between a min and max based on pending pod requests, and node self-repair: delete a worker outside the dashboard and VKE rebuilds it to match the pool configuration. Provisioning takes 3–5 minutes, and a `type: LoadBalancer` Service gets its external IP within 1–2 minutes.

The limits matter more than the feature list, because each one can force a redesign after you've already deployed.

**No VPC 2.0.** VKE clusters attach only to Vultr's legacy VPC, and there's no published timeline for VPC 2.0 support. If the rest of your infrastructure already lives in a VPC 2.0 network, the cluster cannot join it.

**Worker upgrades are manual.** Vultr upgrades the control plane for you. Worker nodes are upgraded by you, from the Manage Upgrades tab on each node pool. Clusters that sit unpatched for months are the normal outcome of missing this.

**No bare metal workers.** Node pools accept virtual Cloud Compute instances only. Bare metal servers cannot join a VKE cluster.

**No bundled ingress controller.** A single service can use the `LoadBalancer` type and be done. Path routing, host routing and TLS termination across several services require installing NGINX Ingress Controller or Traefik yourself, plus cert-manager with Let's Encrypt for certificates. That's ordinary Kubernetes work, but it is work, and it's absent from most "control plane is free" write-ups.

### Is the HA control plane an extra charge?

High availability spreads the control plane across multiple nodes so the API stays reachable when one fails. Vultr's cost documentation doesn't list a separate HA line item, and one 2026 setup guide describes HA as optional at no extra charge. A third-party price tracker lists an HA control plane at $0.0548/hour, or $40/month, a figure identical to what DigitalOcean charges for DOKS high availability, which makes it suspect. Treat HA as unpriced until you see the checkout summary.

Decide at creation either way. Enabling HA on an existing cluster through Terraform destroys and recreates the cluster, including every worker node, so toggling it later means downtime.

👉 [Create a cluster and check the HA option at checkout](https://bit.ly/VuLtr)

## How VKE compares on price

|  | Vultr VKE | DigitalOcean DOKS | Hetzner + K3s (self-managed) |
| --- | --- | --- | --- |
| Control plane | Free | Free | Self-managed |
| HA control plane | Optional, no fee listed in Vultr's cost docs | +$40/month | You configure it |
| Cheapest usable worker | $10/month (2 GB) | ~$12/month (2 GB) | ~€5.49/month excl. VAT (2 vCPU / 4 GB) |
| Three 4 GB nodes | $60–72/month | ~$36–72/month | ~€16.50/month excl. VAT |
| Managed upgrades | Control plane yes, workers manual | Yes | No |
| Ingress included | No | No | Yes (Traefik) |
| CNI | Calico | Flannel | Flannel |
| Operational load | Low | Low | High |

The anchor for the whole comparison is AWS EKS, which bills about **$73/month** for the control plane before a single worker exists.

Between VKE and DOKS the node math is nearly identical. DigitalOcean's interface is more polished and its App Platform integration suits teams that want everything managed from one place. VKE makes more sense when you're already inside Vultr: same account, same invoice, same instance plans you know. Hetzner with K3s is far cheaper at roughly €16.50/month for three nodes, and you pay for it with a control plane you run yourself, no node self-repair, and manual certificate handling. That trade is reasonable for a team with DevOps capacity and unreasonable for a developer who wants to ship an application.

## Credits, free tier and one caution

New Vultr accounts can receive promotional credit of up to **$300 for 30 days**, subject to the terms of the current offer. Vultr has no permanent free tier and no free trial; every plan is paid, and the credit is time-limited, so a cluster that outlives the 30 days starts billing against your balance. Payment goes into a prepaid balance via card, PayPal, crypto or bank transfer.

One caution worth knowing before you deposit money: a system administrator reviewing Vultr on G2 reports opening an account, passing verification, depositing $100, and having the account banned within 24 hours without an explanation or a refund of the unused balance. That's a single user report, not a pattern, but it's the kind of thing that's easier to read about now than to discover with a production cluster attached. The same review page shows an overall rating of 4.3/5, with positive reviews citing setup speed and stable uptime.

👉 [Open a Vultr account and check the current credit offer](https://bit.ly/VuLtr)

## Which setup to order

Match the plan to what the cluster is for:

- **Learning Kubernetes, nothing public** → 1× `vc2-1c-2gb` at $10/month. Skip the load balancer until you actually expose a service.
- **A small production workload that must stay up** → 3× `vc2-2c-4gb` at $60/month plus one load balancer, about $70–72/month. Keep the node count odd.
- **Latency-sensitive pods, or a previous bad experience with CPU throttling** → 3× `vhp-2c-4gb` at $72/month plus the load balancer, $82–84/month.
- **Persistent data in the cluster** → add block storage at $0.10/GB-month and budget it separately from node cost.

Two things to confirm on the order page before you click deploy: whether the HA control plane shows a charge in your region, and whether your existing private network is legacy VPC or VPC 2.0, since VKE only attaches to the former. Both are cheap to check now and expensive to fix after the cluster exists.

👉 [Compare Vultr's worker-node prices before you deploy](https://www.vultr.com/pricing/?ref=9738262-9J)
