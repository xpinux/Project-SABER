# NPM Supply-Chain / Malicious Package Hunting

## Description
Hunting queries to detect suspicious npm package installs and network connections related to recent npm supply-chain compromises (e.g., installs that fetch packages or artifacts from unusual URLs, typosquatted domains, Git repositories, or direct tarballs).  
Use both network and process telemetry.

Key goals:
- Detect outbound connections to suspicious domains (e.g. webhook.site, known typosquats) or unknown hosting endpoints used by malicious packages.
- Detect npm installs that pull packages directly from remote URLs (HTTP[S], git, SSH, tarball) a common vector in supply-chain abuse.
- You may also find webhook related events in your enviroment.

## Log Source
- **DeviceNetworkEvents** — network outbound and URL telemetry  
- **DeviceProcessEvents** — process command lines (npm, npx) and parent process context

## MITRE ATT&CK Mapping
- **T1195 – Supply Chain Compromise** (malicious packages, dependency confusion)  
- **T1071 – Application Layer Protocol** (suspicious HTTP/HTTPS callbacks / C2-style callbacks during install)  
- **T1204.002 – User Execution: Malicious File** (if user-run installs execute malicious payloads)

## Configuration
- **Recommended time window for initial hunt:** 30 days  
- **Severity (investigation priority):** Medium to High (depending on correlation with other alerts)

## Recommendations & Tuning
- **Whitelist** known developer hosts (internal registries, CI/CD runners) to reduce false positives.  
- Use **both queries** together: a process-level hit (npm installing from URL) + network-level hit to the same domain/IP = higher confidence.  
- **Simulate/test**: Run the queries over historical data (Simulate / ad-hoc) and review results to tune:
  - Time window (e.g., 7/30/90 days)  
  - Command patterns (npm variants to include)  
  - Additional delivery indicators (.tgz, git@, git+, raw GitHub URLs)  
- Consider adding lookups for **known-good registries** (registry.npmjs.org, internal registries) and exclude them.

## False Positives
- Developer machines running legitimate `npm install` with direct git URLs or internal registries.  
- CI/CD jobs that fetch from external artifact stores.  
- Use host or account exclusion lists for build servers, developer workstations, and known automation accounts.

---
