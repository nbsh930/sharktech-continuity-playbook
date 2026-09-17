# cloud business continuity: a practical playbook with RTO, RPO, backups and Sharktech pricing

Business continuity sounds like something that lives in a binder nobody opens until the day everything breaks. In practice, it's simpler than the binders suggest: know which systems keep your revenue flowing, decide in advance how long they're allowed to be down, then buy infrastructure and backups that actually meet those numbers.

This guide walks through the parts that matter — RTO, RPO, backups, DR sites — and uses Sharktech's current cloud lineup (with verified pricing) as a concrete example of what the infrastructure layer costs, so you can budget a continuity setup that fits your workload instead of guessing.

## What "cloud business continuity" actually covers

Business continuity is the umbrella term for keeping operations running during a disruption. Disaster recovery is the subset that deals with bringing IT systems back. The two get used interchangeably, but the distinction matters when you're writing a plan:

- **Business continuity** asks: which business functions stop costing us money if they go offline?
- **Disaster recovery** asks: how do we restore the servers, data, and network access those functions depend on?

Cloud hosting changes the economics of the second question. A generation ago, real disaster recovery meant a second server room in another city, replicated hardware, and a contract you paid for while hoping never to use it. Today, spinning up standby infrastructure in a data center 2,000 km away is a line item measured in tens of dollars per month.

Two metrics anchor every continuity plan, and it's worth getting them straight because everything else — hardware choice, backup frequency, budget — hangs off them:

- **RPO (Recovery Point Objective):** how much data you can afford to lose, measured in time. An RPO of 1 hour means backups must run at least hourly.
- **RTO (Recovery Time Objective):** how long you can afford to be down before the business damage becomes unacceptable.

A company blog can tolerate an RPO of 24 hours. An order-processing database usually can't. Write these two numbers down per system before you buy anything, because they'll tell you whether a $7.95/month VPS is enough or whether you need redundant infrastructure — not the other way around.

## The infrastructure layer: what keeps systems running in the first place

Continuity starts before the disaster. Hardware fails, disks die, networks get attacked — and the cheapest downtime is the downtime that never happens.

Sharktech runs an OpenStack-based cloud platform across five data centers: Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam. For continuity purposes, the relevant facts are these:

**High availability by default.** Resources in the cloud platform operate across multiple servers and storage nodes simultaneously, so a single node failure doesn't take your VMs down. The platform carries a 99.999% uptime guarantee, and VMs survive hardware failures without needing a manual reboot-and-pray session. Their Smart VPS line runs on triple-redundant Proxmox clusters with 40G interconnects and makes the same uptime guarantee.

**Built-in DDoS protection.** Every hosted service includes DDoS filtering at no extra cost, with attack traffic scrubbed at the network level before it reaches your machines. This matters for continuity more than people assume: an availability attack is a disaster too, and for a lot of online businesses it's a more likely one than a data center fire.

**Sane bandwidth pricing.** Inbound traffic is free, each cloud service includes 5,000GB of outbound, and overage runs at $0.002 per GB. Egress fees are one of the quiet ways providers lock you in — when moving your data out costs thousands, "business continuity" starts looking expensive. Low egress means the reverse: migrating, replicating, or simply leaving stays cheap.

**No lock-in.** You can download your disk images at any time, upload your own ISOs, and move workloads in or out via the portal or REST API. A continuity plan that depends on a provider you can't leave isn't really a plan.

If this is the kind of infrastructure you're evaluating, 👉 [check out Sharktech's full cloud lineup and current plans](https://bit.ly/SharKTech).

## Full plan comparison: what each Sharktech option costs

Here is every currently listed cloud-related plan on Sharktech's order pages, verified directly against their store. Prices are USD.

**Public Cloud (pay-as-you-go with a fixed resource allowance; overflow billed hourly)**

| Tier | CPU | RAM | SSD | NVMe | HDD | Bandwidth | Price (monthly) | Order |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Small | 4–16 vCPU | 8–32 GB | 300–2400 GB | 0–1200 GB | 0–4800 GB | 20 TB+ | from $39.00 | [Deploy Public Cloud Small](https://portal.sharktech.net/aff.php?aff=1611&pid=602) |
| Medium | 8–32 vCPU | 16–64 GB | 800–6400 GB | 0–3200 GB | 0–12800 GB | 20 TB+ | from $79.00 | [Deploy Public Cloud Medium](https://portal.sharktech.net/aff.php?aff=1611&pid=603) |
| Large | 32–128 vCPU | 64–256 GB | 1500–12000 GB | 0–6000 GB | 0–24000 GB | 20 TB+ | from $249.00 | [Deploy Public Cloud Large](https://portal.sharktech.net/aff.php?aff=1611&pid=604) |
| Enterprise | 64+ vCPU | 128+ GB | 5000+ GB | unlimited tiers | unlimited tiers | 20 TB+ | from $499.00 | [Deploy Public Cloud Enterprise](https://portal.sharktech.net/aff.php?aff=1611&pid=605) |

The tiers work as resource pools, not fixed VM sizes — a Small allocation can be split into several small VMs or run as one bigger one. Overflow rates: CPU $0.0025/core/hr, RAM $0.0035/GB/hr, SSD $0.00006/GB/hr, NVMe $0.00009/GB/hr, HDD $0.00002/GB/hr, extra IPv4 $1.50/month (the first is free).

**Dedicated Cloud (prepaid, fixed monthly resources — the predictable-bill variant of the same platform)**

| Plan | CPU | RAM | Storage options | Data transfer | Price (monthly) | Order |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Dedicated Cloud | 8–512 vCPU | 16–1024 GB | SSD / HDD / NVMe | 5–300 TB | from $86.23 | [Configure Dedicated Cloud](https://portal.sharktech.net/aff.php?aff=1611&gid=102) |  |

**Smart VPS (Proxmox-based, NVMe storage, 60Gbps DDoS protection included)**

| Plan | CPU | RAM | Storage | Bandwidth | Price | Order |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Smart VPS | 2–128 vCPU | 4–256 GB | 40 GB–2 TB NVMe | 4–304 TB | from $7.95/mo (quarterly −25%, semi-annual −35%, annual −50%) | [Order Smart VPS](https://portal.sharktech.net/aff.php?aff=1611&gid=126) |  |

**Backup and off-site storage — the pieces most continuity plans are missing**

| Service | What's included | Price (monthly) | Order |  |
| --- | --- | --- | --- | --- |
| Acronis Cloud Backup (Cyber Protect) | 200 GB cloud backup, ransomware protection, sync & share included | $4.00 base + $0.02/additional GB | [Add Acronis Cloud Backup](https://portal.sharktech.net/aff.php?aff=1611&pid=648) |  |
| S3 Object Storage | 1 TB storage + 1 TB bandwidth, full S3 API | $4.90/TB | [Add S3 Object Storage](https://portal.sharktech.net/aff.php?aff=1611&pid=643) |  |

A few honest notes on reading this table. The Public Cloud "starting from" prices assume the base resource commit for the cheapest location; the order form prices your exact configuration. The S3 figure is a flat per-TB rate with no minimum commitment, which is what makes it workable as a third backup copy. And the Acronis base tier is 200 GB — enough for a small business's critical files, not enough for a server image library; the $0.02/GB add-on scales it predictably.

## Public Cloud or Dedicated Cloud? Match the billing model to your continuity posture

Both run on the same infrastructure; the difference is purely financial, but it affects how you plan.

**Public Cloud** includes a fixed resource commit and lets you burst beyond it, billed hourly. If your DR site only spins up during an incident, you pay for idle commit most of the time and full resources only when the standby is actually running — which is the classic "pilot light" DR pattern. Sharktech's own example: a Large plan ($287.18 for 32 cores/64GB/1500GB SSD) running six oversized VMs around the clock adds up to $396.62/month with overflow; run those VMs at 50% duty cycle and the overflow bill drops proportionally.

**Dedicated Cloud** is a fixed prepaid allocation. Same resources, same bill, every month. If you need a permanent warm standby that runs 24/7, predictable is better than flexible — you don't want your DR budget to depend on an incident lasting three days instead of one.

Rule of thumb: bursty or standby workloads → Public Cloud. Always-on production or DR nodes → Dedicated Cloud. Unsure? 👉 [Compare both billing models on Sharktech's cloud page](https://portal.sharktech.net/aff.php?aff=1611&gid=99).

## Building the plan: a five-step walkthrough

Here's the actual sequence, with the Sharktech options mapped onto each step. This is the part the binder version of business continuity never gets to.

### 1. Inventory and rank your systems

List what runs your business, then sort into three buckets: revenue-critical (order processing, customer-facing apps), important (internal tools, email), and nice-to-have. Only the first bucket needs aggressive RTO/RPO numbers. The others can ride out a day.

### 2. Set RTO and RPO per bucket

- Revenue-critical: RTO minutes to a few hours, RPO minutes to an hour → live redundant infrastructure, near-continuous backup.
- Important: RTO hours to a day, RPO 4–24 hours → regular backups plus a documented restore procedure.
- Nice-to-have: RTO days, RPO days → periodic backup, restore when someone gets to it.

### 3. Pick the tier that matches

For a typical small-business critical workload — a web app plus database — Public Cloud Small or Medium covers it with headroom to burst. A Smart VPS at $7.95/month handles the "important" tier fine, especially at the annual rate where the same plan runs $3.98/month. For a full warm standby that mirrors production, price it as Dedicated Cloud and check whether the predictable bill beats burst pricing at your duty cycle.

### 4. Put backups where the plan says

This is where the RPO number earns its keep. The Acronis Cyber Protect service handles scheduled backups of files and systems (Windows, Linux, macOS, physical or virtual) with deduplication and ransomware detection built in, starting at $4/month for 200 GB. For larger datasets and archives, S3 object storage at $4.90/TB gives you an off-site, API-accessible copy that any backup tool speaking S3 can target — which is nearly all of them.

Follow the 3-2-1 rule: three copies of the data, on two different media, with one copy off-site. A cloud VM plus Acronis backup plus S3 archive satisfies this neatly without buying a single tape.

### 5. Test the restore

The step everyone skips. A backup that has never been restored is a hypothesis. Schedule it: restore a VM from image, download an object from S3, verify the Acronis recovery console actually reaches your machine. Sharktech's portal supports downloading disk images on demand, so test-restores cost nothing beyond the bandwidth — which, again, is free inbound and $0.002/GB outbound.

## Don't skip the exit strategy

A continuity plan has to survive the failure of any single vendor — including the one hosting it. Sharktech's no-lock-in posture (image downloads, open APIs, no proprietary formats) makes this easier than most, but the principle applies everywhere you deploy: your plan should include, in writing, how you would move your workloads and data to another provider, and roughly what it would cost in egress and effort.

If your current provider makes that question hard to answer, that's worth knowing before the incident, not during it.

## Common questions, answered directly

**Can a small business afford real business continuity?** With cloud pricing at these levels, yes. A complete setup for a small business — one cloud VM, Acronis backup, S3 off-site copy — lands somewhere between $50 and $130/month depending on size. The question isn't affordability anymore; it's whether you've spent an afternoon writing down your RTO and RPO.

**What's the difference between backup and disaster recovery?** Backup gets your data back; DR gets your systems running again. You need both. A backup without a restore procedure is data archaeology; a DR site without fresh backups is a very fast way to launch an empty server.

**How often should the plan be tested?** Restore tests quarterly for critical systems, annually for the full plan. Mark it on the calendar like a bill — it doesn't happen otherwise.

**Which tier do I actually need?** Most teams overestimate. Start with the smallest tier that fits your critical workload, use the burst capability to absorb spikes, and upgrade when the monthly bill says you've outgrown the commit. Downgrades are available on both cloud products, so the cost of starting small is near zero.

For sizing help, Sharktech offers a free consultation with their engineers — 👉 [book a free cloud consultation to size your continuity setup](https://bit.ly/SharKTech).
