# ADR-0010: Claude uses its own GitHub identity, ShinChanWooBot

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Claude needs to clone, push, and open PRs. Using the owner's personal account would make every automated action look personal and would give Claude the owner's full access.

## Decision

Claude uses the `ShinChanWooBot` GitHub account, authenticated over SSH with `~/.ssh/id_ed25519_nanoclaw` for git, and with `gh` for the API. The old OpenClaw key was deleted on the owner's instruction.

## Consequences

- Actions are attributed to `ShinChanWooBot`, and the owner can revoke that account separately.
- The account must be given access to each repo it works in. Access to the fork is confirmed by the successful push.
- The `gh` token is stored in plain text by `gh` on this machine.

## Alternatives considered

- **Owner's personal account:** rejected. Mixes automated and personal activity.
- **A fine-grained token only:** not chosen for now. SSH is already set up and works for git.
