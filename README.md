# OpenVibe.Realtime

> Browser delivery plane for events: authorised WS/SSE topics with cursors, resume and presence.

**Status:** placeholder — planning only, no runnable code yet.  
**Domain:** `realtime.openvibe.network`  
**Plan:** OpenVibe End-to-End Realignment & Implementation Plan, revision 3 (20 Sep 2026), §2 and §6.2.  
**License:** AGPL-3.0 (same as every OpenVibe service).

## Purpose

Reserved for the Realtime runtime if it is operationally useful to split it out of OpenVibe.Events. Until that decision is made, the Realtime gateway is a separately deployable runtime inside OpenVibe.Events; this repository holds the decision record and nothing else.

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

## Decision pending

ADR-005 (Realtime Topics and Cursor/Resume Model) decides whether this becomes its own service. Do not add code here before that ADR.

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
