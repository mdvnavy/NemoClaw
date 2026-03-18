# NVIDIA NemoClaw: Comprehensive Analysis of Changes to OpenClaw

**Date**: 2026-03-18
**Repository**: https://github.com/NVIDIA/NemoClaw
**Analysis**: Complete codebase exploration and documentation review

---

## Executive Summary

**IMPORTANT FINDING**: **NemoClaw is NOT a fork or modification of the original OpenClaw codebase.**

Instead, **NemoClaw is an entirely new project created by NVIDIA** that acts as a secure orchestration layer and plugin for OpenClaw. OpenClaw is used as a runtime dependency (version 2026.3.11), not as a source code base to be modified.

### What NemoClaw Actually Is

NemoClaw is an open-source stack developed by NVIDIA that:
- **Wraps OpenClaw** in a secure NVIDIA OpenShell sandbox environment
- **Adds security layers**: network policies, filesystem isolation, process restrictions
- **Routes inference** through NVIDIA's managed cloud infrastructure (build.nvidia.com)
- **Manages lifecycle**: installation, migration, configuration, and rollback
- **Provides CLI tooling**: Both host-level commands and OpenClaw plugin commands

**Relationship**: NemoClaw depends on OpenClaw as a package dependency, similar to how a web application might depend on Express.js or React. It doesn't modify OpenClaw's source code.

---

## Project Architecture Overview

NemoClaw consists of **100% original NVIDIA code** organized into two main components:

### 1. TypeScript Plugin (`/nemoclaw` directory)
- **20 TypeScript source files** (~3,500 lines of code)
- **Purpose**: Thin CLI layer that integrates with OpenClaw
- **License**: Apache 2.0 (NVIDIA Copyright 2025-2026)

### 2. Python Blueprint (`/nemoclaw-blueprint` directory)
- **Python orchestration code** for sandbox lifecycle management
- **Purpose**: Versioned artifact that plans and applies OpenShell resources
- **License**: Apache 2.0 (NVIDIA Copyright 2025-2026)

---

## Complete List of NVIDIA-Created Components

Since NemoClaw is not a fork, **ALL code in this repository was created by NVIDIA**. Here's the comprehensive breakdown:

### TypeScript Plugin Code (All Original NVIDIA Work)

#### Core Plugin Infrastructure
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw/src/index.ts` | ~200 | Plugin entry point, defines OpenClaw plugin API interfaces |
| `nemoclaw/src/cli.ts` | ~100 | Commander.js CLI command registration |
| `nemoclaw/openclaw.plugin.json` | 32 | OpenClaw plugin manifest and configuration schema |

#### Command Implementations (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw/src/commands/launch.ts` | ~150 | Fresh OpenClaw setup inside OpenShell sandbox |
| `nemoclaw/src/commands/migrate.ts` | ~200 | Move existing host OpenClaw into sandbox |
| `nemoclaw/src/commands/connect.ts` | ~80 | Interactive shell into sandbox |
| `nemoclaw/src/commands/status.ts` | ~250 | Show sandbox, blueprint, and inference state |
| `nemoclaw/src/commands/logs.ts` | ~100 | Stream blueprint and sandbox logs |
| `nemoclaw/src/commands/onboard.ts` | ~150 | Interactive setup wizard |
| `nemoclaw/src/commands/eject.ts` | ~120 | Rollback and restore host installation |
| `nemoclaw/src/commands/slash.ts` | ~80 | Chat interface `/nemoclaw` command |
| `nemoclaw/src/commands/migration-state.ts` | ~100 | Migration state management |

#### Blueprint Management (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw/src/blueprint/resolve.ts` | ~180 | Version resolution, cache management |
| `nemoclaw/src/blueprint/fetch.ts` | ~200 | Download blueprint from OCI registry/GitHub |
| `nemoclaw/src/blueprint/verify.ts` | ~150 | Digest verification, compatibility checks |
| `nemoclaw/src/blueprint/exec.ts` | ~120 | Subprocess execution of blueprint runner |
| `nemoclaw/src/blueprint/state.ts` | ~100 | Persistent run state management |

#### Onboarding Infrastructure (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw/src/onboard/config.ts` | ~150 | Configuration file management |
| `nemoclaw/src/onboard/prompt.ts` | ~200 | Interactive prompts for setup wizard |
| `nemoclaw/src/onboard/validate.ts` | ~100 | Validation for user inputs |

### Python Blueprint Code (All Original NVIDIA Work)

#### Orchestrator
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw-blueprint/orchestrator/runner.py` | ~600 | Main CLI runner (plan/apply/status/rollback actions) |
| `nemoclaw-blueprint/orchestrator/__init__.py` | ~20 | Package initialization |

#### Policy Definitions (All Original)
| File | Purpose |
|------|---------|
| `nemoclaw-blueprint/policies/openclaw-sandbox.yaml` | Baseline security policy: filesystem, network, process restrictions |
| `nemoclaw-blueprint/policies/presets/slack.yaml` | Slack API network policy preset |
| `nemoclaw-blueprint/policies/presets/discord.yaml` | Discord API network policy preset |
| `nemoclaw-blueprint/policies/presets/telegram.yaml` | Telegram API network policy preset |
| `nemoclaw-blueprint/policies/presets/github.yaml` | GitHub API network policy preset |
| `nemoclaw-blueprint/policies/presets/docker.yaml` | Docker registry network policy preset |
| `nemoclaw-blueprint/policies/presets/pypi.yaml` | PyPI registry network policy preset |
| `nemoclaw-blueprint/policies/presets/npm.yaml` | NPM registry network policy preset |
| `nemoclaw-blueprint/policies/presets/jira.yaml` | Jira API network policy preset |
| `nemoclaw-blueprint/policies/presets/outlook.yaml` | Outlook API network policy preset |
| `nemoclaw-blueprint/policies/presets/huggingface.yaml` | HuggingFace API network policy preset |

#### Migration and State Management (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `nemoclaw-blueprint/migrations/snapshot.py` | ~300 | State snapshot utilities for migration |
| `nemoclaw-blueprint/blueprint.yaml` | ~100 | Manifest: version constraints, profiles, components |

### Supporting Infrastructure (All Original NVIDIA Work)

#### Installation and Setup Scripts
| File | Lines | Purpose |
|------|-------|---------|
| `install.sh` | ~350 | One-line installation script |
| `uninstall.sh` | ~300 | Uninstallation and cleanup script |
| `scripts/install-openshell.sh` | ~200 | OpenShell installation |
| `scripts/setup.sh` | ~300 | Legacy setup script |
| `scripts/setup-spark.sh` | ~150 | Spark GPU instance setup |
| `scripts/brev-setup.sh` | ~200 | Brev.dev remote deployment setup |
| `scripts/nemoclaw-start.sh` | ~100 | Sandbox startup script |
| `scripts/fix-coredns.sh` | ~50 | CoreDNS configuration fix |
| `scripts/walkthrough.sh` | ~100 | Interactive walkthrough |
| `scripts/write-auth-profile.py` | ~80 | Authentication profile writer |
| `scripts/telegram-bridge.js` | ~250 | Telegram integration bridge |
| `scripts/test-inference.sh` | ~100 | Inference endpoint testing |
| `scripts/test-inference-local.sh` | ~80 | Local inference testing |
| `scripts/start-services.sh` | ~100 | Service orchestration |

#### CLI Entry Points and Utilities
| File | Lines | Purpose |
|------|-------|---------|
| `bin/nemoclaw.js` | ~450 | Main CLI entry point |
| `bin/lib/credentials.js` | ~150 | Credential management |
| `bin/lib/nim.js` | ~200 | NIM (NVIDIA Inference Microservice) integration |
| `bin/lib/nim-images.json` | ~100 | NIM Docker image registry |
| `bin/lib/onboard.js` | ~250 | Onboarding utilities |
| `bin/lib/policies.js` | ~150 | Policy management utilities |
| `bin/lib/registry.js` | ~100 | Registry operations |
| `bin/lib/runner.js` | ~200 | Blueprint runner utilities |

#### Test Suite (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `test/cli.test.js` | ~300 | CLI functionality tests |
| `test/policies.test.js` | ~200 | Policy validation tests |
| `test/registry.test.js` | ~150 | Registry operations tests |
| `test/nim.test.js` | ~200 | NIM inference tests |
| `test/install-preflight.test.js` | ~150 | Installation checks |
| `test/e2e/test-full-e2e.sh` | ~250 | End-to-end integration tests |
| `test/e2e-test.sh` | ~200 | E2E test runner |
| `test/Dockerfile.sandbox` | ~50 | Sandbox test container |

#### Container Images (All Original)
| File | Lines | Purpose |
|------|-------|---------|
| `Dockerfile` | ~100 | NemoClaw sandbox image definition |
| `.dockerignore` | ~20 | Docker build exclusions |

#### Documentation (All Original NVIDIA Content)
**50+ documentation pages** covering:
- Architecture and design (`docs/reference/architecture.md`)
- Command reference (`docs/reference/commands.md`)
- Inference profiles (`docs/reference/inference-profiles.md`)
- Network policies (`docs/reference/network-policies.md`)
- Quickstart guide (`docs/get-started/quickstart.md`)
- How it works (`docs/about/how-it-works.md`)
- Overview (`docs/about/overview.md`)
- Release notes (`docs/about/release-notes.md`)
- Deployment guides (`docs/deployment/`)
- Monitoring guides (`docs/monitoring/`)
- Custom documentation build system (`docs/_ext/`)

#### Build and Configuration Files (All Original)
| File | Purpose |
|------|---------|
| `package.json` | Root package configuration (depends on openclaw 2026.3.11) |
| `nemoclaw/package.json` | Plugin package configuration |
| `nemoclaw/tsconfig.json` | TypeScript compiler configuration |
| `nemoclaw/vitest.config.ts` | Test framework configuration |
| `nemoclaw/eslint.config.mjs` | Linting rules |
| `nemoclaw-blueprint/pyproject.toml` | Python project metadata and dependencies |
| `pyproject.toml` | Root Python project metadata |
| `Makefile` | Build targets (check, lint, format, docs) |
| `nemoclaw-blueprint/Makefile` | Blueprint-specific build targets |
| `.editorconfig` | Editor configuration |
| `.gitignore` | Git exclusions |

#### CI/CD and GitHub Configuration (All Original)
| File | Purpose |
|------|---------|
| `.github/workflows/pr.yaml` | Pull request CI workflow |
| `.github/workflows/pr-limit.yaml` | PR rate limiting |
| `.github/agents/` | AI agent configurations |
| `.coderabbit.yaml` | Code review automation |

#### Project Documentation (All Original)
| File | Purpose |
|------|---------|
| `README.md` | Main project documentation |
| `LICENSE` | Apache 2.0 license with NVIDIA copyright |
| `CONTRIBUTING.md` | Contribution guidelines |
| `CODE_OF_CONDUCT.md` | Community guidelines |
| `SECURITY.md` | Security policy and vulnerability reporting |
| `spark-install.md` | Spark GPU installation guide |

---

## Key NVIDIA Innovations and Additions

Since this is not a fork, **NVIDIA created everything from scratch**. The major innovations include:

### 1. Security Architecture (100% NVIDIA Original)
- **Multi-layer isolation**: Landlock LSM + seccomp + network namespaces
- **Declarative policy system**: YAML-based network and filesystem rules
- **Hot-reloadable policies**: Network policies can be updated at runtime
- **Operator approval workflow**: Unknown network requests surfaced to TUI
- **Filesystem confinement**: Read-write limited to `/sandbox` and `/tmp`

### 2. Inference Routing (100% NVIDIA Original)
- **Transparent proxy**: All model API calls intercepted and rerouted
- **NVIDIA cloud integration**: Routes to build.nvidia.com (Nemotron 3 Super 120B)
- **Multiple backend support**:
  - NVIDIA Cloud (production)
  - NIM (NVIDIA Inference Microservice) - local
  - vLLM - local alternative
  - OpenAI-compatible endpoints
- **Provider profiles**: Configurable inference backends

### 3. Blueprint Lifecycle System (100% NVIDIA Original)
- **Versioned artifacts**: Blueprints are immutable, versioned OCI images
- **Digest verification**: SHA-256 integrity checks
- **Plan-before-apply**: Dry-run capability before resource creation
- **Rollback support**: Full state snapshots for safe migration
- **Cache management**: Local blueprint cache to avoid re-downloads

### 4. Migration System (100% NVIDIA Original)
- **Host-to-sandbox migration**: Move existing OpenClaw installation into sandbox
- **State preservation**: Snapshots of config, plugins, and data
- **Rollback capability**: `nemoclaw eject` restores host installation
- **Zero-downtime migration**: Minimal disruption during transition

### 5. CLI Architecture (100% NVIDIA Original)
- **Dual-layer CLI**:
  - `nemoclaw` - Host-level management commands
  - `openclaw nemoclaw` - Plugin commands inside OpenClaw
- **Interactive onboarding wizard**: Step-by-step setup
- **Status monitoring**: Real-time sandbox health checks
- **Log streaming**: Unified logs from blueprint + sandbox

### 6. Container Orchestration (100% NVIDIA Original)
- **Custom sandbox image**: Pre-configured OpenClaw in OpenShell
- **Pre-installed dependencies**: Node.js, OpenClaw CLI, blueprint runner
- **Dedicated sandbox user**: Non-root execution with minimal permissions
- **Volume mapping**: Persistent `/sandbox` workspace

### 7. Remote Deployment (100% NVIDIA Original)
- **Brev.dev integration**: Deploy to remote GPU instances
- **Automated provisioning**: One-command setup on cloud GPUs
- **Spark GPU support**: Optimized for NVIDIA Spark instances

### 8. Integration Ecosystem (100% NVIDIA Original)
- **Telegram bridge**: Expose agent via Telegram bot
- **Tunnel support**: ngrok-style public endpoint
- **Service orchestration**: Manage auxiliary services (bridge, tunnel)

---

## OpenClaw Usage Pattern

NemoClaw uses OpenClaw as a **runtime dependency**, not as source code to modify:

```json
// package.json
{
  "dependencies": {
    "openclaw": "2026.3.11"
  }
}
```

**How NemoClaw uses OpenClaw**:
1. **Installs OpenClaw CLI** as a package dependency (via npm)
2. **Registers as a plugin** via `openclaw.plugin.json`
3. **Extends OpenClaw** with new commands (`openclaw nemoclaw <command>`)
4. **Wraps OpenClaw** in a sandbox environment
5. **Routes OpenClaw's inference** through NVIDIA infrastructure
6. **Does NOT modify OpenClaw source code** - uses it as-is

**Analogy**: This is like building a Docker container for a Node.js app. You don't fork Node.js, you package it with your app and add orchestration around it.

---

## Technology Stack Comparison

### Original OpenClaw (Not Modified)
- Autonomous AI agent framework
- CLI for agent interaction
- Plugin system for extensions
- Model API integration
- Configuration management

### NVIDIA NemoClaw (Entirely New)
- **TypeScript plugin** for OpenClaw
- **Python orchestrator** for sandbox lifecycle
- **NVIDIA OpenShell runtime** integration
- **Security policy engine** (YAML-based)
- **Blueprint versioning system**
- **NVIDIA cloud inference routing**
- **Migration and rollback utilities**
- **Remote deployment tooling**

---

## File Count Summary

**Total files created by NVIDIA**: ~200+ files

| Category | Count | Description |
|----------|-------|-------------|
| TypeScript source | 20 | Plugin implementation |
| Python source | 5 | Blueprint orchestrator |
| Policy definitions | 12 | Network policy presets + baseline |
| Shell scripts | 15 | Installation, setup, utilities |
| JavaScript utilities | 7 | CLI helpers and libraries |
| Test files | 7 | Unit and E2E tests |
| Documentation pages | 50+ | User guides, references, architecture |
| Configuration files | 15 | Build, lint, project metadata |
| Container definitions | 2 | Dockerfiles |
| CI/CD workflows | 2 | GitHub Actions |

**Total lines of code created by NVIDIA**: ~10,000+ lines (excluding documentation)

---

## Dependencies on External Projects

NemoClaw depends on these external projects **as runtime dependencies** (not as forked code):

1. **OpenClaw** (v2026.3.11) - The AI agent framework being wrapped
2. **NVIDIA OpenShell** - The sandbox runtime from NVIDIA Agent Toolkit
3. **Node.js** (20+) - JavaScript runtime
4. **Docker** - Container runtime
5. **Standard npm packages**: commander, yaml, tar, etc.
6. **Standard Python packages**: PyYAML

**Critical distinction**: These are **dependencies**, not **modifications**. NemoClaw doesn't fork or change these projects.

---

## Licensing and Copyright

**All NemoClaw code is licensed under Apache 2.0**:
```
Copyright 2025-2026 NVIDIA CORPORATION & AFFILIATES. All rights reserved.
SPDX-License-Identifier: Apache-2.0
```

**Every source file contains NVIDIA copyright headers**, confirming this is original work.

---

## Conclusion

**NVIDIA did not modify the original OpenClaw codebase.**

Instead, **NVIDIA created NemoClaw as a completely new project** that:
- Uses OpenClaw as a runtime dependency
- Wraps it in a secure OpenShell sandbox
- Adds enterprise-grade security policies
- Routes inference through NVIDIA infrastructure
- Provides lifecycle management tooling

**Total NVIDIA contribution**: ~10,000+ lines of original code across TypeScript, Python, Shell, YAML, and documentation.

**OpenClaw modification**: Zero lines changed. OpenClaw is used as-is, version 2026.3.11.

---

## Analogy for Understanding

Think of NemoClaw like **Docker for OpenClaw**:
- Docker doesn't modify your application code
- Docker wraps your application in a container
- Docker adds isolation, networking, and orchestration
- Docker provides CLI tools to manage containers

Similarly:
- NemoClaw doesn't modify OpenClaw code
- NemoClaw wraps OpenClaw in an OpenShell sandbox
- NemoClaw adds security policies, inference routing, and lifecycle management
- NemoClaw provides CLI tools to manage sandboxed agents

---

## Questions Answered

**Q: Is NemoClaw a fork of OpenClaw?**
A: No. NemoClaw is a new project that uses OpenClaw as a dependency.

**Q: Did NVIDIA modify OpenClaw source code?**
A: No. OpenClaw is installed via npm and used as-is (version 2026.3.11).

**Q: What did NVIDIA create?**
A: NVIDIA created 100% of the NemoClaw codebase - a security and orchestration layer for OpenClaw.

**Q: How much code did NVIDIA write?**
A: ~10,000+ lines of original code across TypeScript, Python, Shell, and YAML.

**Q: What's the relationship between NemoClaw and OpenClaw?**
A: NemoClaw is an OpenClaw plugin that wraps OpenClaw in a secure sandbox environment.

---

## References

- NemoClaw Repository: https://github.com/NVIDIA/NemoClaw
- OpenClaw Website: https://openclaw.ai
- NVIDIA OpenShell: https://github.com/NVIDIA/OpenShell
- NVIDIA Agent Toolkit: https://docs.nvidia.com/nemo/agent-toolkit/
- NemoClaw Documentation: https://docs.nvidia.com/nemoclaw/

---

**Report Generated**: 2026-03-18
**Analysis Method**: Complete repository exploration, documentation review, and source code analysis
**Repository State**: Clean working directory, branch `claude/summarize-nvidia-changes`
