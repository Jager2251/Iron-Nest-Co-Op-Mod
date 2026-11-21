# Iron Nest Co-Op Mod

A peer-to-peer co-op mod for **IRON NEST: Heavy Turret Simulator**. Play
together over Steam. One player hosts a lobby, the others join with a
short lobby code. Up to **5 players**.

> ⬇️ **Download:** [**NexusMods**](https://www.nexusmods.com/ironnest/mods/20)

> 🐛 **This repository is the issue tracker.** Found a bug or have a suggestion?
> Please [open an issue](https://github.com/Jager2251/Iron-Nest-Co-Op-Mod/issues). The mod's source code is not
> published here. This repo is used for issues and documentation only.

**Requirement:** IRON NEST: Heavy Turret Simulator installed via Steam.

> ⚠️ **Every player must run the same mod version, the same game version (build)
> and the same Steam app.** If someone joins with a different one, the mod refuses
> the connection and shows a note in the panel.

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
build. Built and tested against **`6.0.0-be.788`** (`be.785` also works).

- **BepInEx 5 does _not_ work.** BepInEx 5 only supports Mono games; the game is
  a Unity IL2CPP game, so a BepInEx 5 install will simply not load this mod.
- It must be the **IL2CPP, win-x64** build of BepInEx 6.
- Where to get it:
  - Official bleeding-edge builds: <https://builds.bepinex.dev> (pick
    *BepInEx-Unity.IL2CPP-win-x64*, ideally build `6.0.0-be.788` or newer).
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

**Other panel buttons**
- **Re-sync all players** reloads the host's complete game state for everyone, so
  everything matches again. Your own notepad is kept.
- **Unstick guns** (host only) resets both guns if one gets stuck.
- **Options** (host only, guests can see the values): see "Options" below.
- If a newer mod version exists, the panel shows **Update available**.

**Host moderation (host only).** Next to every other player the host has two
buttons:
- **Kick** removes the player and blocks them for *this* lobby session (they can
  rejoin after you create a new lobby).
- **Ban** removes the player and blocks them *permanently*. The ban is saved to
  `BepInEx\config\IronNestCoop_options.cfg` and also applies to your future
  lobbies. Remove the entry from the `[bans]` section of that file to lift it.

---

## What is synchronised

**Mission**
- When the host starts a mission, every guest loads the same one and spawns in.
  Everyone waits until all players have finished loading; the game shows who is
  still loading. Ending a mission returns everyone to the menu.
- You can also **join a mission that is already running**. The game pauses
  briefly for everyone while the new player loads the host's exact game state,
  so nothing has to be replayed. Players who reconnect during a mission are
  brought back the same way.
- **Saved games** work in co-op: if the host continues a saved mission, all
  players load the saved state.

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
- By default the computer's inputs are shared as well, so you can work on the
  same console together. The host can turn this off ("Sync artillery computer").

**Map table**
- Drawings and markings are shared. The host can turn this off ("Sync map
  drawings") if players prefer their own local drawings.
- The settings of table tools such as the iris tool are shared ("Sync map item
  dials").
- Other players' soldiers are hidden at the map table by default so they do not
  stand in the way ("Hide players at map table").

**Record player**
- Records and the record player are shared, so everyone hears the same music
  ("Sync record player"). The volume knob always stays personal.

**Coffee machine**
- The coffee machine and the cups are shared. Cups and the coffee can can be
  moved and put into the machine. Whoever pulls the lever brews; everyone sees
  the lever, the knobs and the gauges move and gets the same cup. When someone
  drinks a cup, the others see it and the cup is empty for everyone.

**Cats**
- Every player brings their own cat. You see the cats of the others walk, rest
  and play. Picking up, putting down, petting and shooing are shown to everyone,
  and you can pick up, pet or shoo another player's cat too. When someone
  dresses up their cat at the customization table, everyone sees the new look
  and name.

**Options (host only)**
- The host controls the sync options in the Options panel. Guests see the
  values but cannot change them. The options are: "Sync map drawings",
  "Sync artillery computer", "Sync record player", "Sync map item dials" and
  "Hide players at map table".

**Supply console**
- Ammunition (per gun, left/right), powder charges and requisition points.
- Repositioning the Iron Nest; reconnaissance plane.
- Purchases take effect for everyone, no matter who buys.

**Players**
- Soldier avatar (steel helmet + gas mask) with a name tag.
- Up to 5 players per lobby.

---

## What is NOT synchronised (on purpose)

- **The music volume** stays local, so each player can decide for themselves how
  loud they want the music. The record player's music itself is shared (see
  "Sync record player").
- **Your own notepad** stays your own.

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

## Troubleshooting

### BepInEx shows a red error while downloading the Unity base libraries

On the first launch, BepInEx downloads the Unity base libraries for the game's Unity version
(`6000.3.21`) from `unity.bepinex.dev`. The black console window shows
`Downloading unity base libraries from https://unity.bepinex.dev/libraries/6000.3.21.zip`,
followed by a red error. This is part of BepInEx, not of this mod. It usually means that the
download server cannot be reached from your network (firewall, antivirus, DNS, or your
country/provider blocking it).

You can fix it by downloading the file manually:

1. Close the game.
2. Open <https://unity.bepinex.dev/libraries/6000.3.21.zip> in your web browser and save the
   file. If the link does not open for you, try another network, a VPN or a different DNS
   server.
3. Open the game folder (Steam → right-click the game → Manage → Browse local files).
4. Put the downloaded **`6000.3.21.zip`** into the folder `BepInEx\unity-libs`.
   Create the folder if it does not exist yet. **Do not extract the ZIP.**
5. Start the game again. BepInEx finds the ZIP and no longer tries to download it.

If your console names a different version than `6000.3.21`, download the ZIP with that
version number instead.

---

Have fun, and see you in the Iron Nest!
Glory to Castile ! ! !
