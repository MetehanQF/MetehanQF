# Metehan Öztürk

I run a small two-node home lab and build the software it needs. These
repositories are the parts of it that turned out to be worth extracting —
generalised, stripped of anything that names my house, and documented well
enough that someone else could actually run them.

They are not tutorials or dotfiles. Each one exists because something broke, or
because a job was too repetitive to keep doing by hand, and the fix was worth
designing properly.

---

## Featured projects

### ⚡ [MetehanTech Status](https://github.com/MetehanQF/metehantech-status)

A self-hosted control centre for a two-node home lab. Health metrics, alerting
through a single delivery path, verified backups, and a resilience harness whose
job is to **try to break the backups** — corrupt an archive, truncate a dump,
inject a symlink, and confirm the validator refuses to call any of it good.

Built around one discipline: *an unknown is never healthy.* A missing reading
renders `UNKNOWN`, never a comfortable green.

`Python` · `Flask` · `SQLite` · `systemd` · 231 tests

---

### 🏠 [MetehanTech Homelab](https://github.com/MetehanQF/metehantech-homelab)

The infrastructure underneath it: **redundant AdGuard DNS** with parity and
failover tooling, **Mosquitto MQTT**, and **Home Assistant** — reproducible from
Compose files and scripts, with the incident write-ups that produced each design
decision.

A single resolver is a single point of failure for every device in the house.
This is the answer to that, plus the tooling to prove the two resolvers actually
agree.

`Docker Compose` · `AdGuard Home` · `MQTT` · `Python`

---

### 🔧 [Homelab Toolkit](https://github.com/MetehanQF/homelab-toolkit)

Four independent, reversible fixes for problems a Raspberry Pi home lab really
runs into: USB Wi-Fi that drops under load, swap thrash, an RDP surface nobody
meant to expose, and a health monitor for the failures other tools miss.

No framework. Each tool is a directory you can read in five minutes, install
with one script, and undo with the recovery notes beside it.

`Bash` · `systemd` · `Linux`

---

### 🤖 [MetehanTech Smart Home](https://github.com/MetehanQF/metehantech-smart-home)

Home Assistant automation **generated from Python** instead of hand-written in
YAML, plus a no-listener file bridge that lets Home Assistant see infrastructure
it has no integration for.

Two ideas hold it together. **A person always outranks the house** — any light
you touch is locked to your choice until you change the mode on purpose. And
**the camera is off while you are home**, tied to a device you actually carry
rather than to a mode someone might forget to change.

`Python` · `Home Assistant` · `Frigate` · `MQTT` · 59 tests

---

### 📱 [MetehanTech Tablet Dashboard](https://github.com/MetehanQF/metehantech-tablet-dashboard)

A Home Assistant dashboard for a wall-mounted tablet, also generated from
Python. Five views, grouped lighting, host monitoring, and a purple gradient
theme that stays consistent because the cards and the theme are emitted from
one palette.

The generator it grew out of wrote straight into a live dashboard on every run.
This one **writes to a staging directory by default** and refuses a production
destination unless you pass `--deploy`.

`Python` · `Lovelace` · `Kiosk` · 87 tests + a kiosk-scoping suite

---

## How they fit together

```
  Homelab Toolkit      standalone fixes — useful on any Raspberry Pi
         │
  MetehanTech Homelab  DNS · MQTT · Home Assistant — the infrastructure
         │
  MetehanTech Status   monitors it, alerts on it, backs it up and verifies that
         │
  Smart Home           automation on top, generated rather than hand-written
         │
  Tablet Dashboard     what it all looks like on the wall
```

Each repository stands alone. You can take the toolkit without the rest, or the
dashboard generator without my DNS setup.

---

## How I work on these

- **Generated over hand-maintained.** Where a config is thousands of repetitive
  lines, the source is a program and the YAML is output. You edit the generator.
- **Staging before production.** Nothing writes into a live system by default.
  Deployment is an explicit, reviewable step.
- **Unknown is never healthy.** A missing reading is reported as unknown, never
  coerced to a value that reads as fine.
- **Nothing knows which house it runs in.** Every entity id, address and path
  comes from a gitignored config file; the source ships no fallback to a real
  installation, and a CI privacy gate fails the build if one appears.
- **Reversible.** Every change that touches a running system has recovery notes
  written before it is applied.

---

<sub>Most of the write-ups inside these repositories are in Turkish; the READMEs,
code and configuration are in English.</sub>
