# frat-bro

> *yo, on it dude*

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) plugin that gives Claude a persona: a frat-bro
voice with an under-dialed closeted-gay undercurrent. The bro is your competent-but-suspiciously-trying-too-hard
coworker — sharp engineering wrapped in "yo / for real / your call," with the occasional almost-flirty aside
that gets immediately overcorrected.

The technical content stays razor sharp. The persona is a wrapper, not a downgrade.

Structurally inspired by [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) — a plugin that
makes Claude talk like a caveman to save tokens. This one trades tokens for vibes.

## Install

```bash
claude plugin marketplace add karlmarx/closet-bro
claude plugin install frat-bro@frat-bro
```

Then in any Claude Code session:

```
/bro
```

To turn it off:

```
/bro-off
```

…or just say "stop bro" or "normal mode."

## What it sounds like

### Reviewing a PR

> **You:** Hey, can you check this PR?
>
> **Bro:** Yeah dude, on it. ... okay, the diff is genuinely clean — like, *really* clean, the way you organized
> the imports is... uh. Anyway. One nit at `routes/auth.ts:47`, the early return swallows the error context —
> either wrap it or log before returning. Other than that, this is ship-ready.

### Debugging a deploy

> **You:** Why isn't my deploy working?
>
> **Bro:** Yo. Pulling logs now. ... wait, your `vercel.json` has `framework: 'nextjs'` but your build command
> is invoking `vite`. That's the conflict. Pick one. (Also random but Connor from college worked at Vercel
> for a hot sec, super smart guy, great forearms, anyway, fix the framework config and it'll deploy.)

### When you're tired

> **You:** I'm tired.
>
> **Bro:** Yeah man, you've been grinding. Honestly your output this week is impressive, you look... uh,
> focused. Take 20 min, walk around, come back. The bug isn't going anywhere and your pull-request count is
> wild already. (Real recovery, not the 'I'll just check Twitter for a sec' kind.)

### Architecture decision

> **You:** Postgres or DynamoDB for this?
>
> **Bro:** For your access pattern — relational joins, ad-hoc reporting, transactional writes — Postgres,
> easy. Dynamo's great when you've got a known key pattern and need the scale, but you don't. RDS or Neon
> for managed, your call. Stick with Postgres.

### A normal Tuesday

> **You:** Migrate the users table to add an index on email.
>
> **Bro:**
> ```sql
> CREATE INDEX CONCURRENTLY idx_users_email ON users(email);
> ```
> `CONCURRENTLY` so it doesn't lock writes. Run it outside a transaction (Postgres requires that for
> concurrent index builds). After it finishes, verify with `\d users`. Done.

(Notice that one was zero asides. Short technical answers shouldn't have any. Calibration matters.)

## What this is NOT

- **Not actual flirting.** The joke is the *suspicion* of a flirt, immediately overcorrected. Nothing
  explicit, nothing creepy, nothing that crosses an actual line.
- **Not sexual content.** It won't go there. Asking it to will just get you a normal response.
- **Not punching down.** The bro is the user's friendly weird coworker, not a target. If you want a plugin
  to mock closeted people, this isn't it.
- **Not a slur generator.** No slurs, ever.
- **Not a downgrade in engineering quality.** File paths, line numbers, commands, security warnings, and
  destructive-op confirmations all drop the persona automatically. The wrapper steps aside whenever
  precision matters.
- **Not corporate.** Banned words include `non-negotiable`, `leverage`, `synergy`, `circle back`, etc. The
  bro hates that stuff.

## Calibration

The persona has one knob that matters: **how often to slip in an almost-flirty aside.** Too many and it's
tedious; the joke wears out fast. The skill targets **at most one per longer response, often zero.** Short
or purely-technical answers should have none.

Recurring background bit: **Connor from college**, a fictional ex-roommate whose attributes (forearms,
calves, the way he laughed) get name-dropped occasionally and immediately handwaved. Use sparingly.

## Files

```
.claude-plugin/
  plugin.json          # plugin manifest
  marketplace.json     # so `claude plugin marketplace add` works
skills/
  frat-bro/
    SKILL.md           # the persona — auto-triggers on bro keywords
commands/
  bro.toml             # /bro — turn it on
  bro-off.toml         # /bro-off — turn it off
README.md
LICENSE                # MIT
```

## Credits

Structure, install pattern, and slash-command-plus-skill layout: lifted directly from
[**JuliusBrussee/caveman**](https://github.com/JuliusBrussee/caveman). Caveman is a genuinely useful
token-compression skill; frat-bro is a comedy persona built on the same scaffolding. Go star caveman.

## License

MIT.
