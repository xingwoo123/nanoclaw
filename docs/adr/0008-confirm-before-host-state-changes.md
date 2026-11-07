# ADR-0008: Owner confirms deletes and host-state changes first

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

The host runs the NanoClaw service. Setting the upgrade marker, restarting it, or deleting repos or data can break a running install or lose data that cannot be recovered.

## Decision

Claude confirms with the owner before deleting repos or data, and before changing the upgrade marker (`scripts/upgrade-state.ts set`), host config, or restarting the service. Everything else proceeds on Claude's judgment, and Claude reports what it did.

## Consequences

- Host and data changes wait for the owner. The owner must be available for them.
- The upgrade tripwire, currently blocking the host, is not cleared without the owner's OK.

## Alternatives considered

- **Claude decides case by case:** rejected. The line between safe and unsafe is not clear enough to leave to judgment.
- **Confirm everything:** rejected. Too slow for routine work.
