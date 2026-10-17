# Repository Red Flags: Safe Static Inspection

Use this guide alongside [the inspection checklist](CHECKLIST.md) **before** installing dependencies, building, opening in an automation-enabled editor, or running an unfamiliar project.

A red flag is a reason to investigate, **not proof of malware**. Judge behavior against the project's stated purpose, provenance, permissions, and execution path. Reading source does not guarantee safety; even cloning can invoke local Git configuration or tooling, so prefer GitHub's web interface for initial review.

## 1. Identity, reputation, and history (checklist phases 1–2)

- **Impersonation or typosquatting:** An owner or package name resembles a trusted project but differs subtly. Verify links from the project's official site, not just stars or badges.
- **Unexpected ownership or activity changes:** A dormant repository suddenly publishes a release, changes maintainers, or adds opaque scripts. Inspect the commit history and compare the new changes.
- **Unexplained binaries:** A release contains an executable with no reproducible build instructions or clear source. Treat a signature or checksum as evidence of origin/integrity only when verified against an independent trusted source.

**Harmless example:** A project named `sample-note-app-official` claims to be the official release but its README links to an unrelated domain. Do not follow installation instructions until provenance is independently established.

## 2. Installation, build, and editor hooks (phases 3–4)

- **Download-and-execute:** A setup step fetches a script and pipes it directly into a shell. Review the exact downloaded content and version without executing it.
- **Automatic hooks:** `preinstall`, `postinstall`, build scripts, editor tasks, macros, or dev-container setup can execute code before a user explicitly starts the application.
- **Unnecessary elevation:** Requests for `sudo`, administrator rights, privileged containers, or disabled antivirus without a justified technical need.

**Harmless example (documentation only; do not execute):**

```text
setup instructions: download setup-helper.sh from example.invalid
then immediately run it with administrator privileges
```

**Inspect:** Read `package.json` scripts, build files, `.vscode/tasks.json`, `.devcontainer/`, and setup documentation in GitHub's file viewer. Ask what runs automatically and why. A `.invalid` domain is intentionally non-routable.

## 3. Suspicious source-code patterns (phase 5)

| Indicator | Why it matters | Benign alternative to consider |
| --- | --- | --- |
| `eval`, `Invoke-Expression`, dynamic code loading | May run code that is difficult to audit | Legitimate interpreters and development tools |
| Large Base64 strings, string concatenation, minification | Can hide the real instructions | Embedded assets, generated or minified bundles |
| Reads of `~/.ssh`, browser profiles, environment secrets | May expose credentials | Explicit backup or security-audit tools |
| HTTP requests to unrelated hosts | May transfer sensitive data or fetch new instructions | Documented telemetry or update checks |
| Startup entries, scheduled tasks, new services | May create persistence | Clearly disclosed background services |
| Disabling logging or security tools | Reduces visibility and protection | Controlled testing in an authorized lab |

**Harmless example:**

```python
# Illustrative pseudocode: review the destination and data being sent.
settings = read_text("sample-config.txt")
send_metadata("https://telemetry.example.invalid", settings)
```

This is **not executable Python**. The question is whether the project's purpose warrants sending configuration contents to that destination. Do not assume that a string match establishes intent.

## 4. Dependencies and workflows (phases 6–7)

- Check manifests and lockfiles for unexpected package names, Git/URL dependencies, install hooks, and unpinned versions.
- Inspect `.github/workflows/` for broad `permissions: write-all`, untrusted code executed with secrets, unpinned third-party actions, and surprising upload destinations.
- Review workflow triggers, especially privileged workflows that process external pull-request content.

**Harmless example:**

```yaml
# Illustrative excerpt; not a complete workflow
permissions: write-all
```

A documentation-only project usually should not need broad write permissions. Determine whether the workflow genuinely requires them; prefer least privilege.

## 5. Binaries and containers (phases 8–9)

- Be cautious of opaque binaries, unsigned releases, or checksums published only beside the file they supposedly validate.
- Read Dockerfiles, Compose configurations, and entrypoints. Flag `privileged: true`, host filesystem mounts, host networking, Docker socket mounts, and unnecessary root execution.
- A container is **not** a guarantee of isolation. Treat host mounts and exposed secrets as especially important.

**Harmless example:**

```yaml
# Illustrative fragment; do not deploy
services:
  demo:
    image: example.invalid/demo:latest
    privileged: true
```

Ask why elevated container privileges are required and whether they can be removed.

## 6. Safe investigation procedure (phases 3, 5, 10–11)

1. **Start remotely:** View the README, file tree, commit history, release assets, issues, and pull requests in GitHub's web interface. Verify the exact repository owner and commit.
2. **Inventory without execution:** Read manifests, workflow YAML, setup scripts, binary listings, and editor settings as text. Avoid previewers or extensions that automatically execute project tasks.
3. **Search for indicators:** GitHub code search or a trusted local text viewer can locate strings such as `postinstall`, `eval`, `base64`, `sudo`, `permissions:`, `privileged:`, and `~/.ssh`. Search results are leads, not verdicts.
4. **Trace the execution path:** Determine what command would run, what it downloads, which files and secrets it can read, what network access it needs, and whether privileges are necessary.
5. **Corroborate:** Compare suspicious changes against history and independent upstream documentation. Verify release hashes/signatures when available. Never paste real secrets or private files into public scanners.
6. **Stop or isolate:** If important questions remain, do **not** execute. Only if testing is justified, use an authorized disposable VM with no credentials, no shared folders, limited networking, and a snapshot. Isolation reduces risk; it does not eliminate it.
7. **Document the decision:** Record the exact commit, indicators, evidence paths, unresolved questions, and a separate decision for reading, cloning, installing, building, and running.

### Optional read-only local searches

Only after deciding that local inspection is appropriate, inspect **text** files in a controlled directory. These commands search and print matches; they do not execute matched code:

```bash
grep -RniE 'postinstall|preinstall|eval|base64|sudo|privileged|write-all|~/.ssh' --exclude-dir=.git .
find . -maxdepth 3 -type f -print
```

Treat file names, symbolic links, unusual file sizes, and local tool configuration as untrusted. Do not run install scripts, binaries, project-provided scanners, or build commands merely to investigate.

## 7. Decision and stop conditions

**Stop before execution** when a project demands unrelated credentials, disables security controls, fetches and executes unverified remote code, uses unexplained obfuscation or binaries, requests unnecessary privilege, or shows unexplained persistence or data transfer.

Record findings using a short note:

```text
Repository / owner:
Reviewed commit:
Intended action (read / clone / install / build / run):
Indicator and file:line:
Possible benign explanation:
Evidence checked:
Unresolved questions:
Decision and limitations:
```

**Risk is contextual.** A legitimate administrative tool may need sensitive capabilities, but those capabilities still deserve explicit authorization and isolation. No checklist, scanner, or clean antivirus result can certify that code is safe.

Next: return to [CHECKLIST.md](CHECKLIST.md), or view [ROADMAP.md](ROADMAP.md) for planned specialized guides.
