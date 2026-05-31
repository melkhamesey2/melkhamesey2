# Public Portfolio Rules

This repository is a public-facing portfolio space. It is designed to show capability, architecture, and direction without exposing private implementation details.

---

## Purpose

The purpose of this portfolio is to present sanitized work around:

- Local AI systems
- GPU performance and workload stability
- AI media production pipelines
- Arabic dubbing and lip-sync workflows
- Automation and agent workflows
- Real-time analytics architecture
- Defensive security and technical investigation tooling

This is a showcase and documentation layer, not a dump of production code.

---

## Allowed Public Content

The following content is safe to publish:

- Architecture overviews
- Redacted case studies
- High-level workflow diagrams
- Toy examples
- Demo scripts with fake values
- Publicly reproducible notes
- Generic troubleshooting checklists
- Sanitized screenshots
- Non-sensitive benchmark summaries
- Documentation for public-facing repositories

---

## Forbidden Public Content

The following content must not be published:

- Production scripts
- Private prompts
- Exact model tuning recipes
- Exact VRAM/offloading recipes
- Private automation chains
- Client-specific workflows
- Real credentials or API keys
- Local machine paths
- Private datasets
- Trading strategy thresholds
- Real trading decision logic
- Proprietary configuration files
- Full internal operational runbooks

---

## Redaction Rules

Before publishing any file, remove or generalize:

- Usernames, emails, tokens, and secrets
- Absolute paths and machine-specific directories
- Exact environment values that expose proprietary tuning
- Private model names if tied to internal work
- Client identifiers
- Dataset names when not public
- Exact strategy thresholds or scoring formulas
- Screenshots containing private files, prompts, logs, or credentials

---

## GitHub Strategy

Public repositories should be used for:

- Trust-building
- Recruiter/client screening
- Architecture communication
- Demonstrating engineering maturity
- Showing system thinking

Public repositories should not be used for:

- Giving away full production methods
- Publishing competitive advantages
- Exposing sensitive automation
- Releasing client or trading logic

---

## Default Rule

When in doubt, publish the architecture and the result, not the private recipe.
