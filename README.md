# OpenVibe.Realtime

> Browser delivery plane for events: authorised WS/SSE topics with cursors, resume and presence.

**Status:** closed by [ADR-005](https://github.com/OpenVibers/OpenVibe.Contracts/blob/main/docs/adr/ADR-005-realtime.md) (2026-09-22): browser realtime runs inside [OpenVibe.Events](https://github.com/OpenVibers/OpenVibe.Events) (`/realtime/stream`, SSE with cursor resume). This repository stays as the decision record and is reopened only if measured load needs an independently scaled delivery process.  
**Domain:** `realtime.openvibe.network`  
**Plan:** OpenVibe End-to-End Realignment & Implementation Plan, revision 3 (20 Sep 2026), §2 and §6.2.  
**License:** AGPL-3.0 (same as every OpenVibe service).

## Purpose

Reserved for the Realtime runtime if it ever becomes operationally useful to split it out of OpenVibe.Events. ADR-005 decided against a split for now: the Realtime gateway runs inside OpenVibe.Events (deployed, `https://events.openvibe.network/realtime/stream`), and this repository holds the decision record and nothing else.

## Owns

- (when split) topic delivery, cursor/resume, presence, fanout transport

## Does not own

- durable event storage (Events)
- media/game transport packets

## Planned surfaces

- WS/SSE gateway

## Data (authority tables / families)

- none of its own (checkpoints live in Events)

## Capabilities and events

- `realtime.subscribe`

Events: `delivery of authorised projections of Events topics`

## Depends on

- OpenVibe.Events
- OpenVibe.Network

## Acceptance (must be true before "done")

- reconnect from a known cursor yields the complete authorised sequence
- a guessed private topic yields no data

## Bootstrap / extraction source

Extract from product-specific fanout patterns (Live's WebSocket layers) once Events exists.

## Decision

ADR-005 (Realtime Topics and Cursor/Resume Model, accepted 2026-09-22) keeps realtime inside OpenVibe.Events. Do not add code here unless a new ADR reopens the split on measured load.

Not done yet: `realtime.openvibe.network` still shows an OpenVibe.Sites placeholder that advertises this product, and this GitHub repository is not archived (Host compatibility register C-82).

## Launch rule

This repository does not make the product real, and the domain keeps its placeholder page on
[OpenVibers/OpenVibe.Sites](https://github.com/OpenVibers/OpenVibe.Sites) until all of the
following exist here (plan §12.12):

1. an owning runtime with health/readiness endpoints and observability;
2. canonical identity/auth integration (OpenVibe.Network subjects, scoped service principals);
3. server-rendered or static public routes that are useful without JavaScript;
4. real persistence and end-to-end workflows;
5. capability and event registration against `OpenVibe.Contracts`;
6. a migration/seed strategy, a security/threat review, and sitemap/robots/feed behaviour;
7. acceptance tests proving the advertised functionality.

The launch release removes the domain from `OpenVibe.Sites/sites.json`, switches routing and
registers maturity in the ecosystem registry atomically. A placeholder is never counted as an
implemented service.

---

Part of the [OpenVibe network](https://openvibe.network). Built in the open by [OpenVibers](https://github.com/OpenVibers).
