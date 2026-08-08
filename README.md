# Iron Nest Co-Op Mod

A peer-to-peer co-op mod for **IRON NEST: Heavy Turret Simulator**. Play
together over Steam. One player hosts a lobby, the others join with a
short lobby code. Up to **5 players**.

> ⬇️ **Download:** [**NexusMods**](https://www.nexusmods.com/ironnest/mods/20)

> 🐛 **This repository is the issue tracker.** Found a bug or have a suggestion?
> Please [open an issue](https://github.com/Jager2251/Iron-Nest-Co-Op-Mod/issues). The mod's source code is not
> published here. This repo is used for issues and documentation only.

**Requirement:** IRON NEST: Heavy Turret Simulator installed via Steam.

> ⚠️ **Every player must run the same mod version.** If someone joins with a
> different version, the mod refuses the connection and shows a note in the panel.

---

## Installation: choose one option

### Option A: Standalone package (recommended, everything included)

This download already contains **BepInEx** (the mod loader) *and* the mod itself.
You do not need to install anything else.

1. Open the game folder: in Steam, right-click **IRON NEST: Heavy Turret Simulator → Manage →
   Browse local files**. (Typically `…\steamapps\common\Iron Nest Heavy Turret
   Simulator\`.)
2. Copy the **complete contents** of the package into that folder. Afterwards
   `winhttp.dll` and the `BepInEx` folder must sit right next to
   `Iron Nest Heavy Turret Simulator.exe`.
3. Start the game normally through Steam. **On the first launch, wait a few
   minutes**. A black console window shows the progress while BepInEx generates
   its files once. After that the game starts normally every time.

**Uninstall:** delete `winhttp.dll` from the game folder (this disables
everything), or additionally delete the `BepInEx` and `dotnet` folders.

### Option B: DLL only (you already have BepInEx)

Use this if you already have a working BepInEx setup for the game. This download
contains only the mod itself: `IronNestCoop.Core.dll`.

**Required loader:** BepInEx 6 for **IL2CPP** (64-bit), a bleeding-edge (BE)
build. Built and tested against **`6.0.0-be.785`**.

- **BepInEx 5 does _not_ work.** BepInEx 5 only supports Mono games; the demo is
  a Unity IL2CPP game, so a BepInEx 5 install will simply not load this mod.
- It must be the **IL2CPP, win-x64** build of BepInEx 6.
- Where to get it:
  - Official bleeding-edge builds: <https://builds.bepinex.dev> (pick
    *BepInEx-Unity.IL2CPP-win-x64*, ideally build `6.0.0-be.785`).
  - Or the community build on Nexus (IRON NEST → "BepInEx 6.0.0").

**Install:**
1. Make sure BepInEx 6 is installed and has been started at least once, so the
   `BepInEx` folders already exist in the game directory.
2. Copy `IronNestCoop.Core.dll` into `…\BepInEx\plugins\`.
3. Start the game. The mod panel appears at the top-left.

**Uninstall:** delete `IronNestCoop.Core.dll` from `BepInEx\plugins\`.

---

## How to play

In-game a small panel appears at the **top-left** ("IronNest Coop"). Everything
is done from that panel. **There are no hotkeys.**

**Hosting a lobby**
1. Click **Create Lobby**.
2. The panel then shows `ID (Hex): <code>`. That is your lobby code.
3. Share that short code with the players who want to join.

**Joining a lobby**
1. Type the host's lobby code into the **Lobby ID (Hex)** field (digits `0-9`
   and letters `A-F`).
2. Click **Join ID** (or press Enter).
3. Once connected, you appear in the player list and the panel shows you as a
   connected guest.

As a guest you can move around the menu right away; the game itself takes over
control once a mission starts. To leave, click **Leave Lobby**.

**Host moderation (host only).** Next to every other player the host has two
buttons:
- **Kick** removes the player and blocks them for *this* lobby session (they can
  rejoin after you create a new lobby).
- **Ban** removes the player and blocks them *permanently*. The ban is saved to
  `BepInEx\config\IronNestCoop_bans.txt` and also applies to your future
  lobbies. Delete that file (or the single line) to lift it.

---

## What is synchronised

**Mission**
- When the host starts a mission, every guest loads the same one and spawns in.
  Ending a mission returns everyone to the menu.
- **Join _before_ the host starts a mission.** Joining while a mission is already
  running is **not supported**: it is technically possible, but the late joiner
  will end up with parts of the game state out of sync.

**Turret / guns**
- Aiming (rotation + elevation) both ways; levers and handles move along.
- Station actions: change magazine, load shell, powder charges, reload lever.
- Firing is host-authoritative: the host distributes the exact firing values
  (angle, elevation, charge, shell) so impacts are identical for everyone.
- Doors, firing stand and hatches are synchronised.
- Paint applied to a shell before loading is shown to the other players.

**Artillery computer / clipboard**
- Calculated fire-mission cards appear for all players with identical data
  (distance, bearing, elevation, charge, shell, target-type image).
- Any player can calculate cards; checking a card off is synchronised (deleting
  is intentionally not).

**Map-table drawings and markings**
- The host can turn this off in the Options panel ("Sync map drawings") if players
  prefer to work on their own local drawings. Clients can see the setting but
  cannot change it.

**Supply console**
- Ammunition (per gun, left/right), powder charges and requisition points.
- Repositioning the Iron Nest; reconnaissance plane.
- Purchases take effect for everyone, no matter who buys.

**Players**
- Soldier avatar (steel helmet + gas mask) with a name tag.
- Up to 5 players per lobby.

---

## What is NOT synchronised (on purpose)

- **Music** is intentionally not synced, so each player can decide for themselves
  whether they want to listen to music.
- **Artillery computer inputs** stay local. Only the *generated cards* are
  synced, so several players can work at the same time, independently of one
  another.

---

## Known limitations

- The typewriter texts from **"High Command"** and **"Field Reports"** are sent
  by the host, so they appear in the **host's language** for every player.

---

## Reporting issues

Please [open an issue](https://github.com/Jager2251/Iron-Nest-Co-Op-Mod/issues) and include:

- the **mod version** (shown in the top-left panel),
- whether you were **host or guest**, and how many players were in the lobby,
- which package you use (**standalone** or **DLL-only**; for DLL-only, your
  BepInEx version),
- **steps to reproduce**, what you expected, and what actually happened,
- your **log file** `BepInEx\IronNestCoop_ts.log`
  (drag-and-drop it into the issue; from both host and guest(s) if possible).
  If the mod did not load at all or crashed at startup, attach `BepInEx\LogOutput.log` and `BepInEx\ErrorLog.log`
  instead, since the timestamped log may not exist in that case.

---

## Third-party credits

The standalone package includes **BepInEx** (<https://github.com/BepInEx/BepInEx>),
licensed under the [GNU Lesser General Public License v2.1 (LGPL-2.1)](https://github.com/BepInEx/BepInEx/blob/master/LICENSE).
BepInEx is not modified. Source code is available at the link above.

---

## License

Copyright © 2026 **Jager2251**. Licensed under
**[CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)**
(Creative Commons Attribution-NonCommercial-NoDerivatives). See [LICENSE](LICENSE) for the full text.

- ✅ Include the **unmodified** mod in a **non-commercial** modpack, as long as
  you **credit "Jager2251" and link back to this repository**.
- ✅ Modify the mod for your **own private use**.
- ⛔ Do **not** publish or distribute **modified** versions.
- ⛔ **No commercial use** without explicit prior permission.

Commercial licensing or any other permission request: contact **Jager2251 on
Discord**.

---

Have fun, and see you in the Iron Nest!
Glory to Castile ! ! !
