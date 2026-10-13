# The Garden

> *In The Garden, narrative is not told, read, or played — it is bred.*

**The Garden** is a single-file interactive web game about inheritance, memory,
and the stories families keep. Two flowers are planted in a dark garden. Every
bloom carries a genome — some of it you can see (stem, petals, height), and six
story-genes you can hear when you ask: what she **keeps**, **loves**,
**regrets**, **hopes for**, **fears**, and **hums**.

You cross flowers, plant their children, and watch a saga no one wrote emerge
across generations: names drift (Fern → Ferndil → Ferndilwen), a regret can
become a new regret, and rarely a gene jumps loci entirely — *a fear becomes a
humming*. Flowers age, pair for life, and die; when the last keeper of a
story-gene withers, that line of text leaves the garden with them, and the
Chronicle says so.

No dependencies. No build step. No assets. One file.

---

## Run it

Download the HTML file and open it in any modern browser. That's the whole
installation. (If your browser is strict about `localStorage` on `file://`
URLs, serve it locally instead: `python3 -m http.server`, then visit
`http://localhost:8000/garden.html`.)

| Flag | Effect |
|---|---|
| `?fast` | 10× time — a full life in ~40 seconds, for exploring generations quickly |
| `?reset` | start a fresh garden on load (stays active while in the URL) |
| `?kiosk=1` / `?kiosk=0` | force kiosk mode on/off (auto-detects touch devices) |

Flags combine freely: `garden.html?reset&fast`

---

## How to play

There are no menus and no tutorial. Everything is taught by light and gesture:

| Gesture | What happens |
|---|---|
| **Tap a bloom** | Read its story: generation, parentage, six story-genes, condition |
| **Drag one bloom to another** | The *pollination stroke* — cross them |
| **Tap a floating seed** | Take it in hand |
| **Hold the soil** (~1.2s) | Plant the seed — life only comes from life |
| **Drag toward a relative** | The ring turns blue — *same blood* — and a caution asks you twice |
| **Tap the stone** (bottom-left) | Read the Chronicle, the garden's auto-written saga |
| **Hold the spiral seed** (bottom-right, 2.5s) | The garden dims under your hand… then night falls, and everything begins again |

### The laws of the garden

- **Marriage:** the first cross pairs two flowers for life — a golden thread
  rests on the soil between them, and neither crosses with anyone else again.
  Widows do not remarry.
- **Wildflowers** sprout on their own, independent of the player. Crossing with
  one brings new blood: children grow visibly stronger. New blood is a gift,
  never a punishment.
- **Kin warnings:** crossing family is allowed, but only if you ask twice.
  The first attempt is refused with a caution; an identical second attempt is
  honoured — and chronicled as *one blood, twice chosen*.
- **Age:** sprout → bloom → elder (crossable, but stranger children) →
  wither. Petals shed one by one and drift upward; a pale hull remains.
- **Death is real.** If a withered flower was the last holder of its KEEPS
  allele, the Chronicle records it: *"Rowan withered, and the bone flute went
  with her."*
- **The quiet:** if the founded line ends, the garden records the ending and
  goes on — wildflowers arrive, and something grows wild.
- **The blue ones** bloom rarely. *"No one asks for the blue ones. The garden
  grows them when something must be remembered."*

---

## The systems

**Genome.** Eight visible loci (height, stem hue, lean, leaf form/count, petal
count/hue/form) render the body; six story loci, each a pool of ten authored
alleles, render the card. Identity is seeded: the same plant is the same person
on every visit, forever.

**Inheritance & mutation.** Children take each gene 50/50 from either parent,
with a small mutation rate (raised by elder parents). Mutations are of two
kinds: a *shift* (a new allele from the pool) and the rarer *transplant* — an
allele that jumps loci, so a fear can become a humming. Names drift too, so
lineage is legible by ear.

**Names.** Children derive names from their parents with morphological drift
(suffixes, blends), so a family line sounds like one: Fern, Ferna, Fernash.

**The Chronicle.** The game writes its own saga — pairings, births, mutations,
deaths, endings — in a small stone in the soil. Deaths are checked against the
whole living population: if the deceased was the last keeper of their KEEPS
allele, that fragment is recorded as lost to the line.

**Sound.** Life is breath: a deep inhale at planting and crossing, an exhale at
death. Every bloom hums the note of its HUMS gene (a soft pentatonic scale, so
the garden stays consonant); hold your attention on a flower and you hear who
it is. A crossing sounds the parents' dyad, then each child chimes its
inherited hum. A death plays the flower's note one last time, fading.

**Continuity.** Everything persists — genomes, stories, ages, pairings, seeds,
the Chronicle, even the seed in your hand. The garden lives while you're away;
return after a day and you may find deaths chronicled in your absence, petals
ghosting where they stood. If the line ended while you were gone, the quiet is
waiting, and the wind is already bringing wildflowers.

---

## Technical notes

- **One self-contained HTML file** — Canvas 2D rendering, seeded procedural
  generation, Web Audio synthesis, localStorage persistence. No dependencies,
  no frameworks, no images, no audio files, no build.
- **Seeded identity:** `mulberry32` PRNG. A plant's genome, story and name are
  deterministic from its seed.
- **Audio:** all sounds synthesized at runtime (filtered noise for breaths,
  sine oscillators for hums and chimes). Browsers require a user gesture
  before audio, so the garden is silent until your first touch.
- **Persistence:** saved under the localStorage key `the_garden_v1` (every
  ~2s when dirty, plus on exit/hide). Ages are stored in wall-clock time, so
  the garden ages in real time between visits. To wipe a save manually:
  `localStorage.removeItem('the_garden_v1')` — or hold the Seed of Return.
- **Adaptive:** touch devices automatically get larger hit targets and looser
  gesture thresholds; a CPU-load governor simplifies rendering quietly if the
  machine struggles.
- Tested in current Chrome, Firefox, Edge, and Safari. Desktop and tablet.

---

## Design notes

The piece is built on generative art's central bargain — the artist authors
the *conditions* (the allele pools, the laws), and the audience performs one
instantiation of a possibility-space that is comfortably past a billion
distinct sagas. The story text is 100% hand-written fragments; the *assembly*
is genetic. The author's hand is in the gene pool, never the offspring.

The reset button follows the game's own law rather than UI convention:
nothing in this garden happens without a held moment of attention — including
its ending. The dimming while you hold is the confirmation.

### References

Written as part of a practice-based research course, drawing on:

- Jason Bailey, *"Why Love Generative Art?"* (Artnome, 2018) — controlled
  randomness, the gene-pool as authorship
- Qi Li, *"Data visualization as creative art practice"* (*Visual Communication*
  17(3), 2018) — aesthetics over utility; Norman's visceral / behavioural /
  reflective levels
- *"Interactive Art Installations: 6 Inspiring Examples"* (Interactive &
  Immersive HQ, 2024) — real-time generation over playback; emergence from
  local rules; presence as input

### Practice lineage

*The Garden* is the fifth work in an ongoing series exploring what creates
what:

- ***Don't Look Back*** — sound creates the world
- ***Smoke*** — time creates the self
- ***The Unbroken Line*** — the drawing creates both
- ***The Fading Wall*** — light creates memory
- ***The Garden*** — inheritance creates story

---

## License

The code and story text of this repository are released under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) —
share and adapt freely with attribution, not for commercial use. (Swap this
for MIT if you prefer code-only licensing; see below.)
