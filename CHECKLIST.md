# Repository Inspection Checklist

Use this checklist before cloning, opening, installing, building, or running an unfamiliar repository.

## Phase 1 — Identify the project

- [ ] Confirm the exact owner and repository name.
- [ ] Confirm the repository is linked from the official project website.
- [ ] Read the project description and README.
- [ ] Identify what the repository claims to do.
- [ ] Decide whether you only need to read it, clone it, build it, or run it.

## Phase 2 — Review reputation and history

- [ ] Inspect the owner's account history.
- [ ] Review recent commits and contributors.
- [ ] Check whether maintainers changed recently.
- [ ] Review open and closed issues for security concerns.
- [ ] Review recent pull requests.
- [ ] Check whether the repository is archived or abandoned.
- [ ] Note whether activity suddenly changed after a long inactive period.

## Phase 3 — Inventory the files

```bash
git clone --no-checkout https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY
git ls-tree -r --name-only HEAD
```

After a normal clone, use:

```bash
find . -maxdepth 3 -type f | sort
find . -type f -perm -111 -print
```

- [ ] Identify scripts, binaries, manifests, workflows, submodules, and editor settings.
- [ ] Check hidden directories such as `.github`, `.vscode`, `.devcontainer`, and application-specific configuration folders.

## Phase 4 — Inspect installation and execution paths

- [ ] Read every install, setup, bootstrap, build, and start script.
- [ ] Look for commands requiring `sudo`, administrator, root, or privileged containers.
- [ ] Identify code that downloads and immediately executes remote content.
- [ ] Identify automatic install hooks such as npm `preinstall` or `postinstall`.
- [ ] Check whether opening the project can trigger editor tasks, plugins, macros, or extensions.

## Phase 5 — Search for suspicious patterns

```bash
grep -RniE \
'curl|wget|eval|sudo|chmod|chown|nc |netcat|base64|crontab|launchctl|systemctl|Invoke-Expression|DownloadString|EncodedCommand' \
--exclude-dir=.git .
```

- [ ] Investigate encoded or obfuscated content.
- [ ] Investigate unexplained external domains and IP addresses.
- [ ] Investigate access to browser data, SSH keys, wallets, cloud credentials, or password stores.
- [ ] Investigate persistence mechanisms, scheduled tasks, services, or startup entries.
- [ ] Investigate reverse shells, process injection, or security-control disabling.

## Phase 6 — Review dependencies

- [ ] Identify every package manifest and lock file.
- [ ] Confirm package names are spelled correctly.
- [ ] Check whether versions are pinned.
- [ ] Look for Git-based or URL-based dependencies.
- [ ] Review install hooks and build scripts.
- [ ] Check for abandoned or newly created packages.
- [ ] Scan dependencies with appropriate tools before execution.

## Phase 7 — Review GitHub Actions

- [ ] Inspect all files under `.github/workflows/`.
- [ ] Review workflow triggers.
- [ ] Review permissions.
- [ ] Identify secret access.
- [ ] Identify third-party actions and whether they are pinned.
- [ ] Look for untrusted pull-request code running with write access or secrets.
- [ ] Review artifact upload and external network destinations.

## Phase 8 — Review binaries and releases

- [ ] Identify all executable or compiled files.
- [ ] Confirm source code exists.
- [ ] Compare hashes with official releases.
- [ ] Check signatures when available.
- [ ] Scan suspicious binaries using multiple tools.
- [ ] Do not assume a clean scan proves safety.

## Phase 9 — Review containers and virtual environments

- [ ] Inspect `Dockerfile`, Compose files, and entrypoints.
- [ ] Avoid `--privileged`, host networking, root filesystem mounts, and Docker socket mounts.
- [ ] Check whether the image runs as root.
- [ ] Check base-image age and provenance.
- [ ] Restrict secrets, mounts, capabilities, and network access.

## Phase 10 — Protect your environment

- [ ] Use a disposable VM or isolated test machine for uncertain projects.
- [ ] Remove SSH keys, cloud credentials, tokens, wallets, and password-manager access.
- [ ] Disable shared folders and clipboard if risk is elevated.
- [ ] Take a snapshot before testing.
- [ ] Monitor processes, files, and network traffic while running.

## Phase 11 — Record the decision

- [ ] State the commit or release assessed.
- [ ] Document positive indicators.
- [ ] Document warning signs.
- [ ] Assign a risk rating.
- [ ] State whether it is safe to inspect, clone, or run.
- [ ] State the limitations of the review.

## Stop conditions

Do not run the repository when it:

- asks you to disable security controls;
- requests unrelated credentials or secrets;
- contains unexplained obfuscation or binaries;
- downloads and executes remote code without verification;
- requires unnecessary administrator or root access;
- contains suspicious persistence or exfiltration behavior;
- cannot be understood well enough to explain what will execute.