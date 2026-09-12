# The Slow Theatre Handbook

## Slow Theatre has no company and no building

There is no Slow Theatre company. There is no Slow Theatre building. There is no
box office, no artistic director, no season programme, no application to join.

Slow Theatre runs on **Nodes**.

A Node is a group of people, in one place, who perform the acts, keep their own
record, and decide for themselves how far to take it. That's all a Node is.
Nothing is rented, nothing is owned, nothing is incorporated. A Node can be
three friends and a pickup truck. It has existed, elsewhere, before this
Handbook was written, and it will go on existing wherever this Handbook is
read next.

A theatre company needs a building because a building is where permission
lives — where the box office decides who gets in, where the season decides
when something happens, where the company decides who performs. Remove the
building and you remove all three gatekeepers at once. What's left is a
place, some people, and a recurrence. That's enough.

---

## What a Node keeps

Every Node keeps three things, and only three:

1. **The protocol** — the acts, the roles, the constraints (place, exchange,
   recurrence, silence). This can be translated and adapted locally, but its
   spine stays recognisable as Slow Theatre.
2. **A remembrancer-log** — a dated record of every performance: where, when,
   a photo of that day's blackboard, a line from whoever wrote it. This is the
   Node's own history, in its own hand.
3. **Its own name for itself.** A Node is known by the people who run it and
   the town it runs in — never by a brand, a sign, or a logo. Slow Theatre
   doesn't advertise. It recurs, and the recurrence is what people recognise.

Everything else — which acts get performed, how often, in what language, with
what local legal footnotes — is the Node's own decision. Nobody grants a Node
permission to exist. A Node exists the moment people perform.

---

## BosaNode: now and later

**BosaNode is the name for the Slow Theatre community based in Bosa** — the
people bringing this philosophy to life locally, starting with La Prova.
Right now, that's exactly what it is: a small, informal group of friends and
early readers, reviewing these core documents (currently shared via a
website built from this same working repository) and giving feedback before
anything is settled. There's no separate public repository yet, no
Discussions board, no WhatsApp group tied to any of this.

That infrastructure is planned, not built — the next stage, once the
documents themselves are settled enough to be worth building around. When it
happens, it looks like this:

- A new, separate public repository, split from the private working repo
  these documents are drafted in now.
- A Discussions board on that repository, scoped to Bosa and La Prova
  specifically.
- A WhatsApp group — the first informal layer a curious visitor would
  actually reach, eventually via BosaTAZ's Participate tab, once BosaTAZ
  itself is built.

This is the same discipline already applied everywhere else in this
project — prove the smaller thing first, build the infrastructure once
there's something real to build it around. BosaTAZ waits on a working
rehearsal. A formal ZAT event waits on ordinary rehearsals proving
themselves. This repository split waits on these documents earning that
next step.

---

## How a Node starts: forking

Once a Node's public repository exists, this is how a *new* Node joins —
described here as the general mechanism, since it's how any future Node,
including a fully set-up BosaNode, works.

"Repository" just means a folder of documents with a history attached —
every change, ever made, kept and dated.

**Forking** means taking your own complete copy of that folder, under your
own name, that you can freely change — while GitHub keeps a visible thread
back to where your copy came from. Nobody needs to approve it. There's no
form to fill in, no waiting period, no committee deciding if your town
qualifies. You press "Fork," and you now have your own Slow Theatre archive:

```
/protocol/          — the acts, as received. Yours to translate and adapt.
/scripts/            — La Prova, and whatever else your Node performs.
/roles/              — Remembrancer, Il Trasformatore, La Sarta, Il Commerciante, aspetta-tori, and others.
/remembrancer-log/   — empty when you fork it. This is what your Node fills in.
/local/              — your own adaptations: translations, local law, local names.
```

Forking a document library is the whole founding ceremony. There isn't
another one. A Node's first act of joining Slow Theatre and its first act of
performing Slow Theatre are, in this sense, the same act.

---

## What stays visible, without anyone keeping a register

This describes how things work once a Node's repository is public and other
Nodes exist to fork it — not the current state, where BosaNode has no public
repository yet.

Nobody administers a list of Nodes. Nobody needs to. GitHub itself keeps a
running, public record of every fork of the origin repository — this is a
built-in feature of the platform, not something anyone has to maintain. Visit
the origin repository and its network of forks is simply there: every Node
that has ever started, visible, in the order it joined, with no gatekeeper
having approved a single one of them.

This is the difference worth naming plainly: other movements that grow this
way keep a central database of their local groups, reviewed and registered by
a head office. Slow Theatre doesn't have a head office. The fork network is
the database, and it wrote itself.

---

## GitHub Discussions: where Nodes talk to each other

**Planned, not yet built.** Once BosaNode's own public repository exists, it
will have a **Discussions** board — a public noticeboard, readable by
anyone, no account needed to read it, only a free GitHub account needed to
post.

Unlike the generic, cross-Node categories a shared protocol-only origin
might eventually host, BosaNode's Discussions are meant to be scoped
geographically and by performance: about Bosa and La Prova specifically, not
Slow Theatre in the abstract. A future second Node's own repo would have its
own Discussions, scoped to their own place and their own performance, never
merged with Bosa's — the same way bosataz-boundaries.md is explicitly Bosa's
own worked example rather than a universal claim.

This won't replace a Node's own private logistics — a WhatsApp group, a
phone call, whoever's actually deciding when the truck goes out. Discussions
would be the layer above that: the place where anyone curious enough to have
been pointed here can read more, and, eventually, take part.

The plan includes a pinned onboarding thread explaining why and how: what a
GitHub account is, why posting requires one when reading doesn't, and how to
set one up. Reading Discussions would cost nothing. Posting in them would be
the first genuinely persistent, named commitment anywhere in this whole
system — see bosataz-boundaries.md's identity boundary for the fuller
reasoning on why that crossing is treated differently from everything
upstream of it.

Planned categories, each doing a different job:

- **Announcements** — dates, locations, and changes as BosaNode itself
  develops.
- **Show and Tell** — what happened at the last rehearsal, linking
  remembrancer-log entries. This is where the archive would get a living
  front door, instead of just being a folder of dated files nobody outside
  the Node ever opens.
- **Protocol Proposals** — suggestions for the shared protocol itself, raised
  here first before becoming an actual proposed change (a "pull request" —
  a formal suggestion to alter the shared documents).
- **Q&A** — practical questions, answered by whoever's already done it.

No one will be required to participate in Discussions to take part in La
Prova itself. Someone who never posts a word is exactly as real a
participant as one who posts every week. Discussions is meant to be an
offer, not an obligation — the same as everything else in this Handbook.

---

## Changing the protocol

Any Node can propose a change to the shared protocol — a new act, a clearer
translation, a better legal footnote for their own country. They raise it in
Protocol Proposals, and if there's real interest, it becomes a pull request
against the origin's `/protocol/`.

If it's accepted, it becomes part of what future Nodes fork. It does **not**
become part of any existing Node's own copy automatically — each Node decides
for itself whether to pull the change into their own fork, on their own
timeline, or not at all. Nothing is pushed. Nothing is synchronised. A
Node that never updates is not behind; it is simply still performing the
version it started with, which was always a complete and legitimate version
of Slow Theatre.

---

## What this Handbook is not

This Handbook is not a licence, a contract, or a membership agreement. Nobody
signs it. Nobody enforces it. It exists to be read once, by someone standing
in a town somewhere, wondering whether they could do this too — and to answer,
plainly: yes, and here is exactly how.

Fork it. Perform it. Keep your own record. That's all a Node has ever been.
