# BosaTAZ — Tools Build Handover

*A short, build-oriented summary. Reasoning lives in
bosataz-explainer.md — this document is what to build, not why.
Nothing described here is built yet.*

## Status

Design complete enough to build from. Hardware kit, feature set, and
constraints are settled. Not yet decided: which local relay
implementation to use, and final UI details beyond what's noted
below.

## Hardware, per node

- Raspberry Pi Zero 2 W — hotspot, local relay, UI server
- microSD card — TAZ Tools OS, checksum-verified before flashing,
  boots to RAM, removable after boot
- USB key — this session's data (presence, ledger, archive-in-
  progress); wiped or swapped between rehearsals
- Battery pack — sized against measured draw, not spec estimates
- Plastic enclosure only — metal measurably degrades the onboard
  antenna's range
- Multiple nodes form a true mesh (802.11s or B.A.T.M.A.N-adv), one
  SSID, seamless handoff — not independent islands

## Software stack

- Local Nostr relay — candidates are strfry, nostr-rs-relay, or
  khatru; not yet chosen. strfry's router mode is worth weighting if
  cross-node syncing (two TAZs meeting at a shared event) becomes
  relevant early.
- Client: browser-only, no app, no extension. Nostr keys generated
  and signed client-side, in-page, ephemeral per session. WebSocket
  to the local relay. WebRTC (via NCC) for voice, signaled locally,
  no external STUN/TURN.
- No DNS resolution beyond what's needed for the local address
  (e.g. `bosataz.local`) — must NOT resolve Apple/Google's
  captive-portal check URLs, or the whole no-portal design breaks.

## Features to build

1. **Presence board** — anyone joined to the hotspot is visible, no
   login, no identity.
2. **Ledger / chat** — named, signed promises, posted to the relay
   as standard (accumulating) events. Handshake emoji (🤝) as the
   visual marker for a posted promise.
3. **Program tab** — current-act state only. Built as a *replaceable*
   relay event, not an accumulating one — always exactly one current
   state, overwritten on each admin update. No timer, no countdown,
   anywhere, under any circumstance.
4. **Participate tab** — static WhatsApp QR code (image only, no
   live link — BosaTAZ has no internet access, a tappable link will
   fail). One line of text below it, verbatim:
   *"bring something you no longer want (L'Usato), bring something
   worth a little more if you'd like to try bartering (the
   Gallery), think of a promise you could offer someone by name
   (the board)."*
   No other explanatory text on this tab.
5. **Archive site** — static, retrospective, not live. Receives
   ledger entries and Remembrancer photographs, synced out to
   BosaNode on a manual, one-way, periodic push. Never pulls
   anything back down.

## Admin interface

- Reachable only via physical USB connection from a tablet/laptop
  to the node. Never exposed over the wifi hotspot.
- Functions needed: advance Program tab state (single tap, per act);
  assign per-node role in a multi-node mesh (presence/ledger, voice,
  or relay-only hop); monitor node health/battery.
- Default priority under load: presence + ledger protected first,
  voice shed first.

## Non-negotiable constraints (see bosataz-explainer.md for reasoning)

- No captive portal, ever — let the OS's native "no internet"
  detection do its job honestly.
- No accounts, no persistent identity, no reputation or history
  tied across sessions.
- No live clock or countdown anywhere in the UI.
- No landing page or "about" screen on any tab — every surface does
  something; explanation is reached only via the Participate tab's
  QR code, never shown by default.
- Nothing in the ledger should ever resemble a running balance or
  transaction total — see bosataz-fiscal.md; this isn't a UI
  preference, it's load-bearing for the zone's legal standing.

## Not yet decided

- Local relay implementation (strfry / nostr-rs-relay / khatru)
- Exact mesh backhaul configuration and real-world coverage testing
- Whether/how cross-node syncing works when two TAZs are
  co-located
- Final visual/UI treatment beyond the handshake emoji convention
