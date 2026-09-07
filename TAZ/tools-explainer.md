# TAZ Tools

*The digital layer of Slow Theatre*

## What this is

TAZ Tools is a software suite that turns a truck into a temporary, air-gapped digital zone — a Temporary Autonomous Zone in the sense Hakim Bey used the term: a pocket of autonomy that appears, does its work, and dissolves, rather than one that tries to become permanent or defended territory.

**BosaTAZ** is the first deployed instance: one server, running the full TAZ Tools suite, physically installed in the truck for the first rehearsals in Bosa.

Each town or community that takes up Slow Theatre gets two matching digital presences, named the same way: **(location)Node** — its permanent, public GitHub fork — and **(location)TAZ** — its own running instance of TAZ Tools. Bosa is first on both counts: BosaNode is the origin repo's first fork, and BosaTAZ is the first TAZ Tools instance, named for the place the truck operates in, not for any single performance.

## The core idea

Slow Theatre has a physical economy that needs no external gatekeeper — barter, conducted openly, witnessed or anonymous depending on the tier, requiring no bank, contract, or market to validate it. TAZ Tools is that same argument applied to a digital layer, instead of an object.

A conventional digital record — a server on the internet, a chat app, a cloud archive — is legible to the state and to platforms by default: every transaction passes through a wire that someone else controls, logs, and can be compelled to hand over. TAZ Tools removes the wire. There is no connection to the wider internet at any point. The zone isn't hidden from outside observation — it's structurally not adjacent to anything that could observe it.

This mirrors the distinction at the heart of barter's own legal standing: permuta was never illegal or secret, it simply never needed anyone's permission. TAZ Tools extends that same posture to the record of what happens inside the zone.

In the first Slow Theatre performance, La Prova Act 3 was originally conceived simply as the tier for what gift (Act 1) and barter (Act 2) couldn't hold cleanly — a promise rather than an object, and by nature an illegible one, since a promise has no settled form until it's kept. 
A promise is valid the instant it's signed and posted — nothing further is required of the promisor for it to count as witnessed. What happens after that is a different party's concern entirely: the promisee is the only one with a stake in whether the promise is actually kept, and with no scribe, no arbiter, and no dedicated Witness role standing behind it, they're also the only one positioned to carry that weight. The layers of witnessing exist for exactly this asymmetry — not to compel anyone, but to give the promisee something to point to, socially, if a promise goes unkept: a signed note, a timestamp, a chalked board, a photograph, a public archive.

Reputation was always barter's actual enforcement mechanism, long before permuta had a name in law. TAZ Tools just gives the promisee a far better trail to invoke it with.

## Physical design

- **The server** lives inside the truck.
  
- **The hotspot** is open and unencrypted — anyone in range can join, no password, no account. It is never connected to the internet.

- **There is no captive portal, landing page, or explanation.** The network's presence is its only announcement, the same way the truck's arrival announces the performance without anyone saying so. The SSID is simply "BosaTAZ" — if you know what it means, you connect; if you don't, it's just another network name.

- **The zone's perimeter is the hotspot's range.** Not a piazza, not a comune, not any administrative boundary — whoever is connected is in the zone; whoever isn't, isn't. The boundary is binary and testable rather than rhetorical.

- **The zone is invisible as a prop**, in the same sense the truck itself is a prop, a set piece, and the centerpiece of the performance all at once. It carries no separate branding or explanation beyond what the performance already provides.

## What the suite contains, and what each part maps to

| TAZ Tools component | Function | Physical Slow Theatre equivalent |
|---|---|---|
| Local presence board | Anyone who joins the hotspot is visible as present — no login, no identity required | The spuntino table: anonymous, untracked, no pairing |
| Local relay + ledger/chat | Named, witnessed promises get a signed, timestamped note | The Act 3 lavagna: OFFERTE E FAVORI, witnessed not priced |
| Static archive site | An accumulating record, written and read in a retrospective register, not a live feed | The Remembrancer's bound annual volume |
| WebRTC audio (via NCC) | Peer-to-peer voice over the local relay, no external signaling service | — |

The presence board and relay run entirely on infrastructure already built for NCC (Nostr Comms for Communities), reconfigured to point at a relay running locally on the truck's server rather than any public Nostr relay, with WebRTC signaling also kept local rather than routed through an outside STUN/TURN service.

**The offer's path, head to archive:**

1. **Head → phone.** The offer is typed into BosaTAZ, named and signed, posted to the local relay. This is the moment it becomes valid — everything after this is publicity and record, not validation.
2.  **Phone → USB key.** The same relay event lands directly in the session's local archive, stored on a USB key, independent of whether it's ever chalked.
3. **Phone → blackboard.** The Remembrancer sees it on the feed and chalks it onto the chalk board as part of Act 3 — a slower, physical, public confirmation for anyone without a device in hand.
4. **Blackboard → photo.** The chalk board is photographed — a different artifact from the relay note, not a duplicate of it: the note is the precise signed record, the photo is evidence of the performance of it.
5. **Photo → USB key.** The photo enters the same local archive as the note, on the same device, before anything leaves the truck.
6. **USB key → Node GitHub.** Both artifacts travel out together on the next periodic push, so the public archive carries the precise record and the textured, human one side by side.

A promise that's typed and signed but never chalked — because the Remembrancer hasn't reached it, or the session ends first — is still fully valid and still reaches the Node GitHub. The chalk-and-photo step enriches the record; it doesn't gate it.

## Relationship to the GitHub layer

Slow Theatre's public digital presence is a separate thing: each town's fork of the origin repo — its **Node** — its own permanent, forkable, internet-reachable archive, the layer aimed at a global audience, part of the growth strategy alongside the annual festival. Bosa's is BosaNode.

A town's **TAZ** is not that layer, and the two are named in parallel precisely so they're never confused for one another:

- **BosaNode** is public, permanent, and reachable by anyone with an internet connection.
- **BosaTAZ** is private in the sense that it only exists in radio range, complete and self-sufficient with no dependency on the wider internet to function, and closer in character to the Remembrancer's bound volume than to a public repo.

The sync between them is **one-way and deliberate**, never automatic and never two-directional. Content only ever leaves the truck outward, carried out by hand and pushed from BosaTAZ to BosaNode as a periodic archive update — the truck never pulls anything back down. This is not a live mirror; it's a record of what happened locally, broadcast outward once it's ready to be permanent, the same relationship the bound annual volume has to the loose daily pages it was copied from.

Every future community that adopts Slow Theatre follows the same pattern: a **(location)Node** on GitHub, and a **(location)TAZ** running in whatever truck or vehicle carries their own performances — Bosa's are simply first.

## Technical architecture

**Hardware kit, per node:**

- A Raspberry Pi Zero 2 W — runs the hotspot, the local relay, and the UI server.
- A microSD card carrying the TAZ Tools OS — verified against a published checksum before flashing, the same discipline already used for SeedSigner's own software provenance. Boots to RAM; the card can be pulled after boot to demonstrate nothing further is being read from or written to it, mirroring the member-witnessed statelessness demonstration already used in the btckeys ceremony.
- A USB key for the session's data — presence activity, the local ledger, the archive-in-progress. Not stateless: it holds this rehearsal's record for as long as the zone is open, then gets wiped or swapped before the next one, and carried out afterward for the one-way push to the town's Node. Using a USB port rather than a second SD card for this avoids the SD slot's unreliable hot-swap behaviour.
- A battery power pack, sized against real measured draw for a full rehearsal rather than spec-sheet estimates.
- Enclosure in plastic, not metal — the Zero 2 W's onboard antenna is a sensitive etched PCB trace, and a metal case measurably degrades its range.

**Coverage.** A single node's realistic open-air range is well short of its theoretical ceiling (~90–100m line of sight with no interference) once bodies, structures, and ordinary 2.4GHz noise are accounted for — closer to a piazza-sized footprint than a whole field. This is the practical reason for multiple nodes rather than one stronger one.

**Mesh design.** Multiple Zeros form a true wireless mesh (802.11s or B.A.T.M.A.N-adv, the same approach used by community networks like Freifunk and guifi.net) rather than independent islands — all broadcasting the same "BosaTAZ" name, with seamless handoff as someone moves across the site. This is a physical enactment of the same no-single-point argument the rest of the project makes: no one node is the zone.

**Per-node role assignment.** Because each Zero has a single radio shared between serving clients and mesh backhaul, roles are configurable per node from an admin interface rather than every node attempting every function — for example, one node dedicated to presence and ledger, another carrying WebRTC voice, a third acting as a pure relay hop with no client-facing service. Default priority under strain: presence and ledger are protected first, voice is shed first, since the ledger is the zone's actual economic function and voice is a carried-over convenience.

**Admin access.** The admin interface is reachable only by a physical USB cable connection from a tablet or laptop directly to a node — never over the wifi hotspot itself. This keeps operational control physically gated to whoever is standing at the hardware, consistent with the zone's participant-facing side staying anonymous, frictionless, and free of any privileged point of access.

## Design principles

1. **No scribe.** No third party — state, platform, or ISP — sits between two people making a promise inside the zone.
2. **Offline-first, not offline-until-convenient.** The air gap is structural, not a temporary state that resolves the moment signal is available.
3. **Presence, not permission.** Joining the network requires nothing — no account, no password, no explanation. The same ethos as the open gifting floor in Act 1.
4. **Temporary by design.** The zone exists for as long as the truck is parked and the server is on. It does not try to persist, defend territory, or become an institution — matching La Prova's own refusal of a hard curtain.
5. **One-way legibility.** What happens inside the zone is witnessed locally in real time; what reaches the outside world is a settled, immutable record, never a live feed.
6. **Witnessing is distributed, not delegated.** A promise is confirmed by the relay signature, the timestamp, live visibility on the network, the Remembrancer's chalk act, the aspetta-tori at Act 3, the photograph, and the archive — seven independent, overlapping layers, none of them load-bearing alone.

No single Witness role is needed, for the same reason no single mesh node is the zone and no wifi-reachable point controls the admin interface: a designated point of confirmation would be exactly the kind of bottleneck the rest of the design avoids.

## Interface notes for future build

- The digital equivalent of the chalk-and-blackboard act — a promise appearing on the local relay — should use a handshake symbol (🤝) as its visual marker in the UI.

## Open questions

- 
