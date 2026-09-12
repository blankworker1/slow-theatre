# Chain Barter

## The original: One Red Paperclip

In July 2005, a Montreal writer named Kyle MacDonald posted a single red
paperclip online — on his own blog and in Craigslist's barter section —
offering to trade it for anything "bigger or better." He promised to travel
to whoever took him up on it.

Someone in Vancouver traded him a fish-shaped pen. He traded the pen for a
hand-sculpted doorknob in Seattle. The doorknob became a camp stove, the
stove a generator, the generator an "instant party kit," and from there a
snowmobile, a snowmobile trip, a truck, a recording contract, a year's free
rent on a Phoenix condo, an afternoon with Alice Cooper, a KISS snow globe,
and finally a role in a film — which the small town of Kipling,
Saskatchewan traded him for a two-storey farmhouse. The final trade closed
on July 12, 2006, exactly one year to the day after the first one.
Fourteen trades, one year, and no money changed hands at any point.

Two things made it work, worth naming because they matter directly to the
version below. First, every trade was public — documented as it happened,
so a stranger halfway across a continent had some way to trust that a
person showing up with a paperclip's worth of trades behind him was
serious. Second, nobody owned the outcome in advance. MacDonald didn't know
it would end in a house any more than the person who traded him a fish pen
did — the value only ever became visible one trade at a time, after the
fact, never priced or planned ahead of itself.

Kipling later put up a giant paperclip sculpture, and the house itself
became a café. None of that publicity was bought or arranged. It happened
because the chain was worth following.

## Why it fits here, and where it genuinely diverges

The original is a real demonstration of something Currency and Character
argues in the abstract: that pricing and trust can both exist without
money, given enough time and enough public witnessing to stand in for
what a price tag would otherwise do. That's the part worth borrowing whole.

But La Prova's version changes the one thing that mattered most in the
original story, and it's worth being precise about the difference rather
than treating this as a straight homage. In the original, ownership
genuinely transferred at every step — MacDonald fully owned the paperclip,
then fully owned the pen, then the doorknob, and so on; each trader gave up
something they owned outright for something else they'd then own outright.
Chain Barter, as built for La Prova, removes that entirely. Nobody ever
owns the object at any point in its life, beginning to end. It's held in
common by the Node from the moment it first appears, and every trade after
that moves *custody*, not property. This isn't a small variation — it's the
same mechanism the original used, aimed at a different outcome: not one
person's escalating personal windfall, but a single object the whole
community keeps stewarding together, indefinitely.

## How it actually runs

- A first Donatore places an object on its own permanent plinth, separate
  from the Gallery's ordinary pedestals — the one thing on display that's
  always there and never turns over week to week.
- The Remembrancer records its form.
- Any Barterer may trade something for it, any number of times, for as
  long as that rehearsal's barter window is open. Each trade is recorded
  the same way.
- The chain freezes the moment the Remembrancer's bell ends Act Three.
  Whoever holds the object at that instant becomes **Il Custode** — not
  chosen, not applied for, just whoever happened to be holding it.
- Before the closing photograph, the Remembrancer chalks one further line
  naming the custodian and the object, kept visibly separate from the
  day's ordinary promises.
- Il Custode's only job is to bring it to the next rehearsal and place it
  back on the plinth — no ceremony, just continuity — where it opens to
  trading again.

Full role description: `roles/il-custode.md`. Digital record: the
BosaTAZ Chain tab, an append-only, local, never-reset history of the
object's whole life — the one surface in the entire digital layer built
to keep accumulating rather than clear between rehearsals.

## The benefactor move, and what "breaking the chain" actually means

Nothing stops someone trading something of real, disproportionate value
into the chain — an ounce of gold for a whittled spoon — and nothing
should. The objective here was always longevity, not appreciation: a chain
that only ever climbed would just be quietly re-importing the original
story's accumulation logic, the exact thing this version was built to
avoid. A chain that can spike and just as easily deflate back down again
is proof the reframing actually held.

Worth naming precisely what this move is, though, since it isn't really a
barter at all. Someone handing over something of real value for something
modest is Act One's gift logic, delivered through Act Two's mechanism — the
benefactor gains nothing and expects nothing back, same as any Donatore.
The actual barter decision, and the real pressure, falls on whoever trades
next: match the new value, or become, in the crowd's eyes, the one who
traded it back down.

That perception is exactly what it is — a perception, never a verdict. The
Remembrancer's record stays flatly factual: what was traded for what, by
whom, on what date. It never characterises a trade as a rise or a fall.
Whether onlookers read a downward swing as the chain being humbled back to
earth, or as someone quietly cashing in the community's own generosity, is
left entirely to whoever's watching — and that ambiguity is arguably the
most interesting thing the object can produce, since it's the one moment
its story and its worth visibly pull apart. A chain that survives a swing
like that and keeps moving afterward says something a steadily climbing
one never could: that the value was never really the point.

One caveat worth holding onto, since it connects straight back to Currency
and Character's third layer. A visible, generous swap like this risks
becoming exactly the kind of recognition-seeking gesture that document
warns about, dressed up as generosity. Nothing wrong with it happening
occasionally, unplanned. Something would go wrong if it became an expected
or repeated way for someone to be seen as generous — the same discipline
RESERVATO depends on to stay a rehearsal tool rather than the table's
default. This only stays healthy as a rare, spontaneous event, never a
designed feature anyone is nudged toward using.

A small but worth-stating nuance follows from all of this: collective
ownership belongs to whichever object currently occupies the chain's
role, not to any specific physical thing permanently. The moment an
object is traded out of the plinth, it leaves that role entirely and
becomes the trader's own outright property — no custody, no obligation,
nothing carried over from having once been the chain object. Someone who
trades their gold for the previous item doesn't inherit any collective
claim over what they now hold; it's simply theirs, the same as anything
won in an ordinary Act Two barter. Only what's currently on the plinth is
held in common. Every object the chain has ever shed along the way
belongs, fully and unconditionally, to whoever it was traded to.

## What's deliberately different from the source, summarised

- **Ownership → custody.** The original was a chain of private property,
  traded away in full each time. This is a chain of collective ownership,
  held in trust one interval at a time.
- **Open-ended time → the rehearsal's own rhythm.** MacDonald traded
  whenever the next offer came in, over the open timeline of the internet.
  Here, trading is bound to the performance itself — live only during a
  rehearsal, frozen by the same bell that closes Act Three every time.
- **A personal blog → a local, cumulative tab.** The original's
  documentation was continuous and public the moment it happened. BosaTAZ's
  Chain tab is deliberately not that — it accumulates locally, on the
  Node's own hardware, syncing outward only later and only in the same
  slow, periodic rhythm everything else in this project runs on.

What's kept whole from the original, and worth ending on: nobody has to
believe in this for it to work. It just has to keep moving, and be worth
watching do so.
