# Development Roadmap

This roadmap is intentionally staged so improvements can be completed gradually and the repository history can show clear skill development over time.

## How to use this roadmap

For each improvement:

1. Open or select the matching GitHub issue.
2. Create a feature branch.
3. Complete one focused improvement.
4. Test and document the change.
5. Commit with a clear message.
6. Open a pull request.
7. Merge after reviewing your own work.
8. Close the issue and update this roadmap.

Recommended branch pattern:

```text
feature/dependency-review-guide
feature/github-actions-audit
feature/repository-scanner
```

Recommended commit style:

```text
Add dependency supply-chain review guide
Add risky workflow permission checks
Add JSON output to repository scanner
```

## Phase 1 — Documentation foundation

- [x] Create the repository.
- [x] Add the main README.
- [x] Add the repository inspection checklist.
- [ ] Add `RED_FLAGS.md` with suspicious behaviors and code patterns.
- [ ] Add `DEPENDENCIES.md` covering package and supply-chain risks.
- [ ] Add `GITHUB_ACTIONS.md` covering workflow security.
- [ ] Add `DOCKER_SECURITY.md` covering container review.
- [ ] Add `TOOLS.md` with Linux, macOS, and Windows inspection commands.
- [ ] Add `ASSESSMENT_TEMPLATE.md` for reusable review reports.
- [ ] Add the Obsidian repository worked example.

### Skills demonstrated

- Security documentation
- Threat identification
- Technical writing
- Risk assessment
- Git and GitHub workflow

## Phase 2 — Improve usability

- [ ] Add a table of contents to each major guide.
- [ ] Add navigation links between documents.
- [ ] Add beginner, intermediate, and advanced review paths.
- [ ] Add a glossary of repository-security terminology.
- [ ] Add quick-reference cheat sheets for Linux, macOS, Windows, and Git.
- [ ] Add a standard risk-scoring model.

### Skills demonstrated

- Information architecture
- User-focused documentation
- Security methodology design
- Risk communication

## Phase 3 — Add real-world case studies

- [ ] Add a safe documentation-only repository example.
- [ ] Add a suspicious training repository example using harmless sample indicators.
- [ ] Add a dependency-confusion case study.
- [ ] Add a typosquatting case study.
- [ ] Add a GitHub Actions abuse case study.
- [ ] Add an XZ Utils supply-chain case study.
- [ ] Add a Codecov supply-chain case study.

### Skills demonstrated

- Incident analysis
- Supply-chain security knowledge
- Evidence-based reporting
- Mapping indicators to risk

## Phase 4 — Build the repository scanner

Create a Python command-line tool that performs safe static inspection without executing target code.

- [ ] Inventory files and extensions.
- [ ] Detect executable files.
- [ ] Detect package manifests and lock files.
- [ ] Detect GitHub Actions workflows.
- [ ] Detect Dockerfiles and Compose files.
- [ ] Search for risky command patterns.
- [ ] Detect encoded or unusually large strings.
- [ ] List external URLs and IP addresses.
- [ ] Generate a Markdown report.
- [ ] Add JSON output.
- [ ] Add command-line arguments and help text.
- [ ] Add error handling.
- [ ] Add unit tests.

### Safety boundary

The scanner should analyze files statically. It should not install dependencies, build projects, or execute repository code.

### Skills demonstrated

- Python
- Secure static analysis
- Regular expressions
- CLI design
- Report generation
- Testing

## Phase 5 — Add specialized security checks

- [ ] Add GitHub Actions permission analysis.
- [ ] Flag unpinned third-party actions.
- [ ] Detect dangerous workflow triggers.
- [ ] Detect privileged Docker settings.
- [ ] Detect Docker socket and host filesystem mounts.
- [ ] Detect suspicious install hooks.
- [ ] Detect Git and URL-based dependencies.
- [ ] Add optional Semgrep rules.
- [ ] Add optional YARA rules for suspicious files.

### Skills demonstrated

- CI/CD security
- Container security
- Detection engineering
- Secure code review

## Phase 6 — Add software supply-chain tooling

- [ ] Generate a Software Bill of Materials.
- [ ] Document dependency scanning with appropriate tools.
- [ ] Add package-name similarity checks.
- [ ] Add dependency freshness checks.
- [ ] Add release-signature and checksum guidance.
- [ ] Document SLSA and provenance concepts.
- [ ] Document secure package publishing practices.

### Skills demonstrated

- Software supply-chain security
- SBOM analysis
- Vulnerability management
- Provenance verification

## Phase 7 — Automation and continuous integration

- [ ] Add formatting and linting checks.
- [ ] Add unit tests to GitHub Actions.
- [ ] Add Markdown link checking.
- [ ] Add security scanning for this repository.
- [ ] Add release automation.
- [ ] Publish versioned releases.
- [ ] Add a changelog.

### Skills demonstrated

- DevSecOps
- CI/CD
- Test automation
- Release management

## Phase 8 — Portfolio presentation

- [ ] Add screenshots and sample reports.
- [ ] Add an architecture diagram.
- [ ] Add a demonstration GIF or short video.
- [ ] Add a project lessons-learned section.
- [ ] Add a limitations and future-research section.
- [ ] Add resume-ready project bullets.
- [ ] Publish a LinkedIn project post.

### Skills demonstrated

- Security communication
- Portfolio development
- Technical presentation
- Professional reflection

## Suggested development order

Complete work in this order:

1. Documentation modules
2. Assessment template and examples
3. Risk-scoring model
4. Basic Python scanner
5. Tests and report generation
6. Specialized workflow and container checks
7. Supply-chain tooling
8. CI/CD and polished portfolio presentation

## Progress journal

Add a short entry after each meaningful release:

```markdown
## YYYY-MM-DD — Version or milestone

### Completed
- What was added or improved

### Learned
- Technical concepts learned
- Problems solved

### Next step
- The next small, achievable improvement
```

Keeping this journal will help demonstrate not only the finished project, but also how your security knowledge, coding ability, and development process improved over time.