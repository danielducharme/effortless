# effortless handoff

## Branch and PRs
- `main` on danielducharme/effortless (a fork of HeyCubit/effortless, kept for Daniel Ducharme's organization). Work goes
  through PRs to `main`. `upstream` is HeyCubit's repo: pull from it only on purpose, and never push to it.
- Commit as yourself (Daniel Ducharme). Nothing here publishes to HeyCubit's installers.
- Two channels. Users install from the `stable` branch (marketplace `ref: stable`, update card reads `public.json`
  from danielducharme/effortless). The dev channel `effortless@effortless-dev` is the plugin from `main`, entries in
  `dev-releases.json`.
- `tools/release.sh --files <paths> -- "<subject>"`: tests, patch bump, commit, push, installs dev here. Never `--all`
  (other chats' changes sit in the tree). Reaches no user.
- `tools/publish.sh "<what's new>" "<detail>"`: minor bump, writes releases.json and public.json, pushes main, moves
  `stable`. Every user of this fork gets an update card. Only on Daniel's word.
- Public: 1.72.0 on HeyCubit's channel; this fork's `stable` does not exist until the first publish.

## Links
- No website and no report worker for this fork. What's new links to `public.json` on `stable`, Share copies the repo
  URL, Report bug opens a new issue on danielducharme/effortless with the version in the body.
- `site/` and `report-worker/` are HeyCubit's and still name them; `tools/site.sh` is unused here.

## Half done
- Updated card redesign (1.48.4, public in 1.49.0): seen only in the render rig. The card is drawn by the code already
  running in that chat, so it first appears on the update after 1.49.0, in a chat running 1.49.0+.
- Haiku handoff recommendation, Compact beside Handoff (hidden under 80 cells), alert default 80%: public, unseen in the
  real app. Isac's dev config still has `swampAt: 60`.
- `effortless@effortless-panel` (1.45.9, agent-panel chat) is disabled in ~/.claude/settings.json, dev enabled. That
  chat has flipped it back before. Offered to uninstall the panel copy: no answer.
- An inline effortless copy has its own store without setup (`~/.claude/plugins/store/effortless_inline-*.json`).
- `tools/release.sh` has another chat's uncommitted edit; `docs/marketing/` untracked. Leave both.

## Next
1. In a fresh (non-remote) chat on the public version: check the band, Compact, Handoff advice, Settings.
2. Watch the first real report that arrives through the form; check the title, body and labels look right.
3. Optional: ruleset blocking force pushes on `stable` (offered, no answer).
4. Terminal: the update card shows no animation while updating (desktop has one); add a moving state there.

## Only Daniel
- Publishing to users, anything that force-pushes, anything with a login or a secret.

## Decided, do not redo
- Deciding glow: rise, hold at full, fade 450 ms from the verdict, drawn as 150 ms pieces placed by clock. The app
  redraws the band every ~100-120 ms and sometimes re-shows an older copy ~0.6 s later; animations must survive a
  restart. Isac: "WORKS" on 1.36.18. Notes in ai-setup memory `mod_band_styling.md`.
- The judge line is off by default (`hide: reason`).
- Theme is one hue rotation, not a second colour set. Hot/Compact bands stay orange-red in both themes.
- No `clipPath` in band Svgs; controls over art need an empty absolute child; Svg needs alt text and a sized box.
- Split view: effortless only shows in the left pane (a Claude Code limitation); the site says so.

## Pointers
- Code `hooks/register.tsx` (bands, settings, judge), `hooks/theme.ts`, `hooks/agents.tsx`, `hooks/progress.tsx`.
- Tests: `CLAUDE_CODE_ENABLE_FUNCTION_HOOKS=1 claude plugin test .` (`tests/effortless.test.ts`), 167 pass.
- Rig `tools/render-band/` (README); `--options theme=orange` renders the orange band.
- Render log `~/.claude/effortless-render-<chat>.log`. Agent panel plan `docs/agent-panel/`.
- Site checks: Jev manifests live in the session scratchpad, not the repo. The footer has no passing Jev check: its only
  click is a footer link that jumps to `#how`, which trips the story's clipped-control findings.
