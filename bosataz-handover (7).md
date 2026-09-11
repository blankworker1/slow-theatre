# BosaTAZ — Build Handover

*A short, build-oriented summary. Reasoning lives in
bosataz-explainer.md — this document is what to build, not why.
Nothing described here is built yet.*

## Status

Design complete enough to build from. Hardware kit, feature set, and
constraints are settled. See "Not yet decided" below for the current
full list of open items — check there rather than here, since that
list is the one kept current as decisions land.

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

**Every node carries identical signage — no exceptions, nothing
beyond this.** Two QR codes (join hotspot, open local address) and
three words, in Italian only — matching every other painted or
spoken text in the physical layer (the lavagna's heading, the toast,
the example promise), none of which has ever appeared in English on
site:

*"Senza segnale? Spostati!"*

That's the entire sign. No label, no heading, no English, nothing
further. No node should look different from another; a visitor near
any node gets the same awareness and access as one standing at the
truck.

## Software stack

- Local Nostr relay — candidates are strfry, nostr-rs-relay, or
  khatru; not yet chosen. strfry's router mode is worth weighting if
  cross-node syncing (two TAZs meeting at a shared event) becomes
  relevant early.
- Client: browser-only, no app, no extension. Nostr keys generated
  and signed client-side, in-page, ephemeral per session. WebSocket
  to the local relay for presence, ledger, and Program-tab state.
  No voice/audio relay — text only.
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

## Security

- **The air-gap already removes the largest category of risk** —
  no route from the wider internet, so nobody outside wifi range
  can ever reach the node, regardless of what software
  vulnerabilities might exist on it.
- **The open, passwordless hotspot means "who can reach the
  server" and "who can join the zone" are the same question** —
  this is required by the design, not a gap, but it does mean
  anyone nearby is on the same network as the relay.
- **Relay spam/flood from an open network is a real, deliberately
  accepted tradeoff.** No accounts, no gatekeeper on posting — a
  light per-connection rate limit at the relay level is worth
  adding to blunt a deliberate flood without compromising the
  openness a real visitor would ever notice.
- **Traffic on the open network is unencrypted** (no realistic
  HTTPS on a purely local, offline network). Low-stakes given what's
  actually sent: no passwords exist to leak, no persistent accounts.
  Hard requirement: private signing keys must never leave the
  browser tab — only signed public events go over the wire.
- **Minimal running services** — only the relay's websocket and the
  UI's HTTP should be listening. No other open ports or default
  services.
- **Patching is manual, via the same SD-card ceremony already
  planned for provenance** — no auto-update path exists since
  there's no internet to pull from. Build this into the same
  between-rehearsal rhythm as the data-card reset, not as separate
  maintenance.
- **Physical theft/tampering of remote node boxes is a real but
  low-stakes risk** — unlike SeedSigner/Seed Hammer, a BosaTAZ node
  holds no keys, no funds, nothing of value beyond one session's
  ordinary presence and ledger data. Reasonable physical robustness
  is enough; no tamper-evidence ceremony warranted.
- **No login exists on the wifi side, so there's nothing to "hack
  into" in the conventional sense — the real risks are more
  specific:**
  - *Fake admin impersonation.* Anyone can post relay events,
    including a fake "current act" update. Mitigation is
    architectural, not a login system: pin the Program tab's
    display to one fixed, known public key baked into every client.
    A forged event from any other key is simply ignored by honest
    clients, regardless of what the relay stores.
  - *Content injection via the ledger.* Since anyone's posted text
    gets displayed to every other visitor, all user-submitted
    content must be rendered strictly as plain text, never as
    executable markup — a hard requirement, not an assumption.
  - *Exploits against the relay/server software itself.* Mitigated
    by choosing mature, field-tested relay implementations (the
    strfry/nostr-rs-relay/khatru shortlist) over anything custom,
    running both the relay and UI server as a low-privilege user
    rather than root, and keeping the UI server to simple static
    file serving with no dynamic server-side processing.
  - The RAM-boot design is a backstop here too: even a successful
    exploit doesn't persist past that session's power cycle.
- **Mesh backhaul (node-to-node traffic) is authenticated
  separately from the client-facing hotspot**, using 802.11s
  mesh-SAE with a shared secret baked into the standard TAZ Tools OS
  image — every correctly-flashed node has it automatically, no
  separate distribution step. This is invisible to clients: phones
  never touch the backhaul, so roaming speed, the open SSID, and the
  no-captive-portal behavior are all unaffected. Tradeoff worth
  knowing: one shared secret across every deployment means a
  physically compromised node's key affects all BosaTAZ instances
  built from that image, not just the one node — acceptable given
  the backhaul only carries the same low-stakes presence/ledger
  traffic already covered above, but a deliberate choice rather than
  the only option. A unique per-deployment key would contain any
  breach to one Node, at the cost of a real setup step the shared
  key avoids.
- **A spoofed "BosaTAZ" network (evil twin) — relevant at ZAT/
  festival scale, not the current small-rehearsal stage.** Open
  SSIDs have no cryptographic binding to specific hardware; anyone
  can broadcast a network with the same name. The real damage
  ceiling is low — no passwords or funds exist to steal, and the
  pinned admin key already protects content on the *real* network —
  but a fake node could serve a malicious Participate-tab QR code in
  place of the real WhatsApp group, redirecting trust rather than
  stealing anything directly. No clean technical fix exists without
  reintroducing the account/credential infrastructure this project
  has deliberately refused; the real answer is human, not software.
  - **Zone Security Agent** — a role for ZAT/festival scale: connects
    to every node on the mesh in turn, at setup and periodically
    through the event, and confirms each is genuinely serving
    BosaTAZ's own content rather than something impersonating it.
  - **Locating a rogue device is fox hunting, not guesswork** —
    signal triangulation, the same basic method radio hobbyists use
    to track down a hidden transmitter. Simplest version: any
    ordinary wifi-analyzer phone app shows live signal strength,
    strengthening on approach — often enough on its own. More
    precise: a directional (Yagi) antenna with an open-source tool
    like Kismet, rotating for signal-by-direction rather than just
    position. Standard practice in wireless security work, not
    exotic — just requires a person actively doing it, not a system
    watching passively in the background.

## Admin interface

- Reachable only via physical USB connection from a tablet/laptop
  to the node. Never exposed over the wifi hotspot — but physical
  connection alone is not sufficient either. The admin web app
  itself requires a PIN/password before showing any controls;
  connecting the cable gets you to a login screen, nothing more.
- The USB connection must be scoped narrowly — a single-purpose
  interface (USB-serial or USB-network gadget) serving only the
  admin app on a fixed local address, not a general host connection
  that would let someone bypass the PIN gate and reach a shell or
  the filesystem directly. The PIN only means something if this is
  built correctly.
- Functions needed: advance Program tab state (single tap, per act);
  assign per-node role in a multi-node mesh (presence/ledger, or
  relay-only hop); monitor node health/battery.
- Default priority under load: presence and ledger protected first.

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
