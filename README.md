# Iron Root

Iron Root is a concept for a modern on-prem operations platform focused on Windows and Linux estates that still need local control, local execution, and strong abstraction over the underlying infrastructure.

The product direction is not finalized. The current intent is to build a cloud-linked but customer-controlled platform that:

- gives each customer a private Iron Root appliance running in their environment
- keeps execution, credentials, workflows, and infrastructure control inside that private environment
- uses a central company-managed hub for licensing, subscription tracking, module distribution, release metadata, and fleet visibility
- abstracts infrastructure details so customers work through Iron Root instead of native hypervisor, package, or automation tooling

## Product Direction

Iron Root is aimed at organizations that still run meaningful on-prem workloads and want automation without rebuilding their operating model around a public cloud control plane.

The rough product shape today is:

- a central management hub operated by Iron Root for licensing, module catalog, release distribution, and cross-customer telemetry
- a customer-owned private appliance that exposes the customer portal, API, workflow engine, controller services, and execution runtime
- controller and engine services that are container or function driven, can scale horizontally, and can be updated by shipping new platform versions
- agentless automation against Windows and Linux over PSRP, WinRM, and SSH
- support for image lifecycle, patching, software deployment, workflow orchestration, and infrastructure abstraction
- a modular feature model so new capabilities can be delivered as licensed add-ons

## Design Principles

- Customer environments stay in control of execution. The central hub links to a customer appliance, but does not directly control that environment.
- The private appliance should prefer outbound federation to the hub rather than inbound control paths.
- Hypervisors are implementation details, not the product center. Hyper-V matters as a useful target, but the platform should treat it as one adapter among several.
- The product should feel like a single operations surface even when the underlying work spans workflows, packages, patches, images, and runtime execution.
- APIs and PowerShell-based CLI management are first-class interfaces, not afterthoughts.

## Functional Areas

- Platform federation: appliance registration, licensing, entitlement sync, release sync, and health reporting
- Workflow and orchestration: conditional execution, approvals, retries, branching, and job coordination
- Systems management: agentless automation for Windows and Linux administration
- Image lifecycle: create, update, publish, and retire system images and templates
- Patch and package management: operating system patching plus Chocolatey, NuGet, and Winget-style software repository functions
- Infrastructure abstraction: run workloads on Hyper-V and other future platforms without exposing customers to native tool complexity
- Extensibility: installable modules that expand product capability as licensed features

## Current Architecture Sketch

The current working architecture diagram lives in [iron-root-hybrid-architecture.mmd](/Users/art/.openclaw/workspace/projects/ironroot/iron-root-hybrid-architecture.mmd). It should be treated as a concept sketch for IRON-2, not a frozen design.

## Team Workflow

Iron Root development should use `dev` as the shared integration branch.

- Create each work branch from `dev`
- Name branches by Jira ticket and purpose, not by person
- Do all work for that Jira ticket in that branch
- Merge finished ticket branches back into `dev`
- Promote `dev` into `main` only when the integrated work is ready for release

The workflow diagram lives in [team-development-workflow.mmd](/Users/art/.openclaw/workspace/projects/ironroot/team-development-workflow.mmd).
