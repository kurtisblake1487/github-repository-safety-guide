# GitHub Repository Safety Guide

A practical playbook for evaluating whether an unfamiliar GitHub repository is reasonably safe to clone, open, install, build, or run.

> No review can guarantee that a repository is completely safe. This project supports a documented, risk-based decision.

## Start here

1. Use the [inspection checklist](CHECKLIST.md).
2. Review [common red flags](RED_FLAGS.md).
3. Inspect [dependencies and supply-chain risk](DEPENDENCIES.md).
4. Audit [GitHub Actions workflows](GITHUB_ACTIONS.md).
5. Review [Docker and container risks](DOCKER_SECURITY.md).
6. Use the commands in [TOOLS.md].
7. Record findings with the [assessment template](ASSESSMENT_TEMPLATE.md).
8. See the worked [Obsidian repository assessment](EXAMPLES/obsidian-starter-templates.md).

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