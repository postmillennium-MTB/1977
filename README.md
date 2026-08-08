# Grateful Dead 1977 — Setlist Atlas

A single-file, zero-dependency HTML tool documenting every show the Grateful Dead played in 1977 — full setlists, a venue/song search, song-frequency stats, and a handful of hand-rolled SVG charts.

**File:** `gd77-setlist-atlas.html` — open it directly in a browser, or embed it via iframe like the other PMR tools. No build step, no external libraries, no fonts loaded from a CDN.

---

## What's inside

| Tab | What it does |
|---|---|
| **Shows** | All 60 shows, chronological, grouped into 5 tour legs. Tap a date to expand the full setlist, which also links out to a date-filtered archive.org search for that night's recordings. |
| **Search** | Toggle between searching venues/cities/states and searching songs. Song mode highlights the match and shows how many of the 60 shows it appeared at. |
| **Stats** | Headline numbers (most-played song, unique songs, longest/shortest setlist, etc.), a song search box, and a full sortable ranking table of every song played. |
| **Graphics** | Seven charts: most-played songs (bar), shows by state (bar), shows by state (pie, top 5 + "Other"), set 1/set 2/encore split (pie), shows by region (pie), setlist length across the year (scatter), and songs per set across the year (scatter, toggled between Set One / Set Two / Encore). |
| **Quiz** | Multiple-choice trivia generated live from the `SHOWS` data — "how many times was X played?" and "which song was played more, X or Y?" — so it can't drift out of sync as shows are added. |

---

## Data & sourcing

Every show's setlist was compiled from a Jerry Stratton–lineage database (the same research lineage that became DeadBase, mirrored at `cs.cmu.edu/~mleone/gdead/` and `cs.cmu.edu/~gdead/`), then cross-checked wherever possible against:

- archive.org show pages and box-set descriptions
- dead.net's official show archive
- Grateful Dead box-set liner notes (Dick's Picks, Dave's Picks, and standalone archival releases)
- Wikipedia entries for specific releases and shows

Most shows were confirmed against **two or more independent sources**. Where sources disagreed or a set break wasn't explicitly labeled, that show carries a `flag` field, and a note is shown right in the expanded setlist rather than being silently guessed.

### One correction worth knowing
*Sunshine Daydream*, the famous outdoor show at Veneta, Oregon, is often misfiled into 1977 — it's actually **August 27, 1972**. It's deliberately excluded from this dataset.

### Shows with an inferred set break or encore (4)
- **Oct 28, 1977** (Kansas City) — encore inferred as the closing song; source didn't mark an explicit break.
- **Nov 1, 1977** (Detroit) — set break placed at a documented tuning pause, not an explicit "Set 1 / Set 2" label.
- **Nov 6, 1977** (Binghamton) — no encore is documented in the sources used; the show may simply not have had one.
- **Dec 30, 1977** (Winterland) — the Set 2 / encore boundary is inferred from typical show shape.

### Shows with no encore documented (7)
Apr 22 (Philadelphia), Apr 26 (Passaic), May 4 (Palladium), May 19 (Atlanta), Oct 1 (Portland), Oct 11 (Norman), Nov 6 (Binghamton). These may genuinely have ended without an encore rather than being missing data.

---

## Officially released shows

Where a show in this dataset was released as part of an official Grateful Dead / Rhino archival series, that's noted in its `notes` field and summarized here. This list reflects only what's been verified and tagged so far — it isn't necessarily exhaustive of every 1977 show that's seen an official release.

| Date(s) | Venue | Release |
|---|---|---|
| May 8 | Cornell (Barton Hall) | Added to the Library of Congress National Recording Registry, 2011 |
| May 19 & 21 | Atlanta / Lakeland | Dick's Picks Vol. 29 |
| May 22 | Hollywood, FL | Dick's Picks Vol. 3 |
| May 25 | Richmond (The Mosque) | Dave's Picks Vol. 1 |
| May 28 | Hartford | *To Terrapin: Hartford '77* |
| Jun 7–9 | Winterland | *Winterland June 1977: The Complete Recordings* |
| Oct 1–2 | Portland | Dave's Picks Vol. 45 |
| Nov 5 | Rochester | Dick's Picks Vol. 34 |
| Nov 6 | Binghamton | Dave's Picks Vol. 25 |
| Dec 29 | Winterland | Dick's Picks Vol. 10 |

---

## How to add or correct a show

The `SHOWS` array and a `SHOW_TEMPLATE` object with full instructions live at the top of the `<script>` block, right above the data. In short:

1. Copy `SHOW_TEMPLATE`, fill in date / venue / city / state.
2. List songs in performance order. Use `{t:"Song Title", seg:true}` instead of a plain string for any song that segues into the next one (renders as "Song Title >").
3. **Reuse existing spelling** for repeated songs — search the file first (e.g. always "Playing in the Band", never "Playin' in the Band") or the Stats tab will count it as a separate song.
4. If you're not sure exactly where a set break or encore falls, add a `flag` string rather than guessing silently.

Everything else — the Search tab, Stats tab, and all six charts — is computed from the `SHOWS` array at load time, so adding a show automatically flows through everywhere. Nothing else needs to be touched.

---

## Design notes

Since this is Grateful Dead content rather than mountain biking, it uses its own theme instead of the PMR trail palette: deep indigo background, marigold and dusty-rose poster-ink accents, a cream "paper" surface for expanded setlists, system-font serif/mono/sans pairing (no web fonts), and ticket-stub-style tabs with a CSS-only perforated edge as the one signature flourish. All charts are hand-rolled inline SVG — no charting library.

Three color schemes are available from the buttons at the top, named after the band's keyboardists in the order they held the chair: **Godchaux** (the default — Keith Godchaux was actually on keys for this '77 tour), **Mydland** (1979–1990), and **Welnick** (1990–1995).
