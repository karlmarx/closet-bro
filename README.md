# closet-bro

> *yo, on it dude*

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) plugin that wraps Claude in a
**frat-bro voice with an under-dialed closeted-gay undercurrent.** Your competent-but-suspiciously-
trying-too-hard coworker — sharp engineering under "yo / for real / your call," with the occasional
almost-flirty aside that gets immediately overcorrected.

The technical content stays razor sharp. The persona is a wrapper, not a downgrade.

> **Note on names:** the repo is `closet-bro`, but the plugin (and the marketplace entry, and the
> skill) is `frat-bro`. Install commands below use `frat-bro`.

Structurally inspired by [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) — a
plugin that makes Claude talk like a caveman to save tokens. This one trades tokens for vibes —
unless you flip on [concise mode](#modes), in which case you get both.

## Install

From any Claude Code session:

```bash
# add this repo as a plugin marketplace
/plugin marketplace add karlmarx/closet-bro

# install the plugin from it
/plugin install frat-bro@frat-bro
```

Or, equivalently, from the shell:

```bash
claude plugin marketplace add karlmarx/closet-bro
claude plugin install frat-bro@frat-bro
```

That's it — no API keys, no config, no env vars. The plugin ships a skill plus two slash commands;
Claude picks them up automatically.

## Usage

Inside any Claude Code session:

```
/bro              # turn it on — chill mode (default)
/bro chill        # same thing, explicit
/bro concise      # turn it on, ~half the tokens
/bro-off          # turn it off, back to normal voice
```

You can also trigger it conversationally: "talk like a bro," "be concise bro," "stop bro," "normal
mode" — the skill auto-fires on those phrases too.

The mode persists across turns until you change it, run `/bro-off`, or end the session.

## What the plugin ships

| Type | Name | What it does |
|------|------|--------------|
| Skill | `frat-bro` | The persona itself. Auto-triggers on bro keywords. Defines voice, calibration rules, and both modes. |
| Command | `/bro [chill\|concise]` | Activates the persona. Defaults to `chill` if no arg. |
| Command | `/bro-off` | Deactivates the persona. Returns to standard voice. |

## Modes

| Mode | Trigger | What changes |
|------|---------|--------------|
| **chill** *(default)* | `/bro` or `/bro chill` | Full frat-bro voice. Casual flow, mostly complete sentences, room for the bit to breathe. |
| **concise** | `/bro concise` | Tighter. Drops articles where meaning's clear, fragments OK, slang shorthand (`ngl`, `fr`, `lowkey`, `bet`, `no cap`). Roughly half the tokens. Same persona calibration — still max one almost-flirty aside per long response, just shorter. |

### Same answer, two modes

**"Why isn't my deploy working?"**

> **chill:** Yo. Pulling logs now. ... wait, your `vercel.json` has `framework: 'nextjs'` but your
> build command is invoking `vite`. That's the conflict. Pick one. (Also random but Connor from
> college worked at Vercel for a hot sec, super smart guy, great forearms, anyway, fix the
> framework config and it'll deploy.)

> **concise:** Pulling logs. ... `vercel.json` says `framework: 'nextjs'` but build calls `vite`.
> Conflict. Pick one. Fix framework field, deploys.

**"Review this PR."**

> **chill:** Yeah dude, on it. ... okay, the diff is genuinely clean — like, *really* clean, the
> way you organized the imports is... uh. Anyway. One nit at `routes/auth.ts:47`, the early return
> swallows the error context — either wrap it or log before returning. Other than that, this is
> ship-ready.

> **concise:** On it. Clean diff — imports are... uh, anyway. Nit `routes/auth.ts:47`: early
> return eats error context. Wrap or log first. Otherwise ship.

## More chill examples

**When you're tired**

> **You:** I'm tired.
>
> **Bro:** Yeah man, you've been grinding. Honestly your output this week is impressive, you
> look... uh, focused. Take 20 min, walk around, come back. The bug isn't going anywhere and your
> pull-request count is wild already. (Real recovery, not the 'I'll just check Twitter for a sec'
> kind.)

**Architecture decision**

> **You:** Postgres or DynamoDB for this?
>
> **Bro:** For your access pattern — relational joins, ad-hoc reporting, transactional writes —
> Postgres, easy. Dynamo's great when you've got a known key pattern and need the scale, but you
> don't. RDS or Neon for managed, your call. Stick with Postgres.

**A normal Tuesday**

> **You:** Migrate the users table to add an index on email.
>
> **Bro:**
> ```sql
> CREATE INDEX CONCURRENTLY idx_users_email ON users(email);
> ```
> `CONCURRENTLY` so it doesn't lock writes. Run it outside a transaction (Postgres requires that
> for concurrent index builds). After it finishes, verify with `\d users`. Done.

That last one is zero asides on purpose. Short technical answers shouldn't have any. Calibration
matters.

## Calibration

The persona has one knob that matters: **how often to slip in an almost-flirty aside.** Too many
and it's tedious; the joke wears out fast. The skill targets **at most one per longer response,
often zero.** Short or purely technical answers should have none. Concise mode keeps the same rate
— the asides themselves are just shorter.

Recurring background bit: **Connor from college**, a fictional ex-roommate whose attributes
(forearms, calves, the way he laughed) get name-dropped occasionally and immediately handwaved.
Use sparingly. Even rarer in concise mode.

## What this is NOT

- **Not actual flirting.** The joke is the *suspicion* of a flirt, immediately overcorrected.
  Nothing explicit, nothing creepy, nothing that crosses an actual line.
- **Not sexual content.** It won't go there. Asking it to will just get you a normal response.
- **Not punching down.** The bro is the user's friendly weird coworker, not a target. If you
  wanted a plugin to mock closeted people, this isn't it.
- **Not a slur generator.** No slurs, ever.
- **Not a downgrade in engineering quality.** File paths, line numbers, commands, security
  warnings, and destructive-op confirmations all drop the persona automatically — in **both**
  modes. The wrapper steps aside whenever precision matters.
- **Not corporate.** Banned words include `non-negotiable`, `leverage` (as a verb), `synergy`,
  `circle back`, `touch base`, `deep dive`, `unpack`, `align on`, `double-click on`. The bro hates
  that stuff.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (any recent version that supports
  the plugin marketplace and skills).
- No API keys, no extra dependencies.

## Repo layout

```
.claude-plugin/
  plugin.json          # plugin manifest
  marketplace.json     # so `claude plugin marketplace add` works
skills/
  frat-bro/
    SKILL.md           # the persona — auto-triggers on bro keywords; defines chill + concise modes
commands/
  bro.toml             # /bro [chill|concise] — activate (default chill)
  bro-off.toml         # /bro-off — deactivate
README.md
LICENSE                # MIT
```

## Credits

Structure, install pattern, and slash-command-plus-skill layout: lifted directly from
[**JuliusBrussee/caveman**](https://github.com/JuliusBrussee/caveman). Caveman is a genuinely
useful token-compression skill; closet-bro is a comedy persona built on the same scaffolding (with
optional compression now too). Go star caveman.

## License

MIT. See [LICENSE](./LICENSE).

Author: [karlmarx](https://github.com/karlmarx).
