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

**Two kinds of node, same internals, different form factor.** In a
single-server setup, the truck itself is the node. In a mesh, the
truck remains one node, and additional nodes are remote, movable,
self-contained repeater units placed around the site — same
Pi/card/key/battery kit, packaged for standing on their own away
from the truck.

**Remote node enclosure — "lamp post," not literally a lamp post.**
Above crowd head height, for coverage reasons (see capacity/coverage
discussion) — but explicitly *not permanent*. These pack up and
move with everything else each rehearsal; "lamp post" describes the
look and function (ordinary street furniture, easy to walk past
without noticing), not a fixture left standing between events —
that distinction matters directly for the abitualità protection in
bosataz-fiscal.md. Final physical form not yet decided — a
freestanding A-frame (sign/ladder style), with the sealed box
mounted inside the top triangle, is one candidate.

**Every node carries identical signage — no exceptions.** The same
two QR codes (join hotspot, open local address) and the same "Not
working? Move and try again" line, printed on every remote node the
same way they're already at the truck. No node should look
different from another; a visitor near any node gets the same
awareness and access as one standing at the truck.

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

## Physical signage (off-network, not software)

The two QR codes and the "move and try again" line — see Hardware,
per node above for the full signage spec and enclosure notes. This
is functional troubleshooting text, not narrative explanation, and
it's the one piece of the whole system that has to exist off the
network, for someone who isn't on it yet.

## Not yet decided

- Local relay implementation (strfry / nostr-rs-relay / khatru)
- Exact mesh backhaul configuration and real-world coverage testing
- Whether/how cross-node syncing works when two TAZs are
  co-located
- Final visual/UI treatment beyond the handshake emoji convention
- Remote node enclosure's final physical form (A-frame candidate
  proposed, not settled)

## Future capability, scoped but not built: per-act audio guide

Structure only, content genuinely undecided: a per-act audio clip,
multilingual, triggered individually by each listener (not a
synced broadcast — no crowd-timing problem to solve, since each
person's playback is independent of everyone else's). Uses the same
act-state mechanism the Program tab already listens for.

**Hard rule, same as for any broadcast-style audio:** never
essential to following what's happening, and — more strictly than
"atmosphere only" — no narrator, no scripted explanatory lines
either, even ones redundant with something already visible. What
actually goes in this slot, if anything, is an open question.

**Explicitly out of scope for BosaTAZ's own hardware:** this slot
has been floated as a placeholder for individual AI interaction at
some future point. That capability cannot run on this
infrastructure — real inference needs a real network call, which
breaks the no-internet-ever principle this whole build depends on.
If it's ever built, it belongs to a separate, connected system
reserved for larger ZAT-scale events, not an upgrade path for the
air-gapped Pi Zero node. Also worth deciding deliberately, whenever
that's built: whether it may only answer factual questions, or
whether it's allowed to interpret meaning — the latter risks
becoming exactly the single interpretive authority the rest of this
design (no scribe, no Witness role, distributed witnessing) has
been built to avoid.
