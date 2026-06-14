<!-- SPDX-License-Identifier: CC-BY-4.0 -->
# openexam-demo-course

The course-side repo of the OpenExam end-to-end demo. Contains:

- [`midterm.oex`](midterm.oex) — buildable `.oex` source that imports questions from `openexam-demo-library` via `<import>` and declares its own inline questions. No participants list in the frontmatter; supply one at build time via `--participants roster.csv`.
- [`warmup.oex`](warmup.oex) — a small standalone `.oex` that shows what you can do without any imports: three inline questions plus a heading personalised via the built-in `student` and `date` globals.
- [`defaults.yaml`](defaults.yaml) — department-shared build defaults (seed, totalPoints, params). Pass via `--defaults defaults.yaml`.
- [`roster.csv`](roster.csv) — the participants list (`id,name[,seed]`). Pass via `--participants roster.csv`.

The companion repo is [`openexam-demo-library`](../library/), which holds the shared question bank.

## Trying it

If you've run [`../setup.sh`](../setup.sh), both repos are materialised under `$XDG_STATE_HOME/openexam-demo/` (default `~/.local/state/openexam-demo`). From there:

```bash
cd ~/.local/state/openexam-demo/local/openexam-demo-course
openexam validate midterm.oex
openexam preview  midterm.oex > /tmp/midterm.html
openexam build    midterm.oex --out-dir out \
                              --defaults defaults.yaml \
                              --participants roster.csv
openexam grade    out ~/devel/openexam/demo/responses.json
```

(`openexam` here is whichever alias you set up — see [`../../BUILDING.md` §5](../../BUILDING.md#5-make-openexam-available-everywhere).)

## License

Apache-2.0 — see the workspace root LICENSE.
