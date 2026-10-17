# GitHub Repository Safety Guide

A practical playbook for evaluating whether an unfamiliar GitHub repository is reasonably safe to clone, open, install, build, or run.

> No review can guarantee that a repository is completely safe. This project supports a documented, risk-based decision.

## Start here — available guides

1. Use the [inspection checklist](CHECKLIST.md).
2. Review [common red flags and safe investigation methods](RED_FLAGS.md).
3. Track planned work in the [development roadmap](ROADMAP.md).
4. See the [learning log](LEARNING_LOG.md) for project progress.

## Planned documentation (not yet published)

These Phase 1 resources are **not available yet**; follow [ROADMAP.md](ROADMAP.md) for progress:

- `DEPENDENCIES.md` — dependency and supply-chain review
- `GITHUB_ACTIONS.md` — workflow security
- `DOCKER_SECURITY.md` — container review
- `TOOLS.md` — inspection commands
- `ASSESSMENT_TEMPLATE.md` — reusable assessment report
- `EXAMPLES/obsidian-starter-templates.md` — worked example

## Understand the risk levels

These actions are not equally risky:

1. Viewing a repository on GitHub
2. Cloning it
3. Opening it in an editor or application
4. Installing dependencies
5. Building the project
6. Running its code
7. Running it as administrator or root

Cloning normally copies files. Installing, building, opening with automatic tasks, or running code creates much greater risk.

## Quick decision rule

### Lower risk

- Markdown documentation
- Curated resource lists
- Plain-text templates
- Static websites
- Small projects with readable source
- No install scripts or binaries

### Medium risk

- Numerous dependencies
- Build scripts
- Containers
- Editor automation
- Browser extensions
- Community plugins
- Network access
- Unsigned release files

### Higher risk

- Obfuscated code
- Credential tools
- Cryptocurrency software
- Cheats or cracks
- Malware samples
- Unknown offensive-security tools
- Reverse-shell functionality
- Root or administrator requirements
- Antivirus-disabling instructions
- Unexplained binaries

## Core principle

Do not ask only, “Is this repository safe?” Ask:

- What code will execute?
- What permissions will it receive?
- What data can it access?
- What network connections can it make?
- Can I test it safely in isolation?

## Disclaimer

This is an educational security-review guide, not a guarantee, certification, or substitute for professional malware analysis.