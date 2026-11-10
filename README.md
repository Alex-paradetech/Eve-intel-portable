EVE Character Intel HUD

Paste a character name OR a solar system name and get, from public zKillboard + ESI data:

SOLAR SYSTEM check (paste e.g. "Tama" or "HED-GP"): looks at the last hour of kills in the
system and flags a probable gate camp in RED. A camp is scored from four signals:
  - several SHIPS killed recently (pods, structures and NPC kills are not counted)
  - the same corp/alliance on most of those kills (a group that stays on grid)
  - kills made by gangs (2+ pilots), not lone ships
  - kills close to a stargate (victim position within 80 km of a gate)
RED = camp likely and still active (last kill under 30 min ago); ORANGE = camp pattern but the
last kill is older, or only some signals; grey/green = some activity / quiet. It is a
heuristic: zKillboard only shows kills that already happened, a camp that has not killed
anything yet is invisible, and killmails can lag. The result refreshes every 90 s while shown.

Character scan:
  - corp / alliance, security status, character age
  - solo vs fleet kill ratio
  - average number of attackers on their kills, last kill date
  - their 3 most used ships (from recent killmails; capsules and structures such as
    mobile warp disruptors are skipped), each with a link to the
    killmail page (the fit) of that ship's latest loss, only if that loss is under
    a year old; left-click opens it, right-click copies it
  - a CYNO signal (see "How the cyno check works")

It never touches the EVE client or the screen. It only reads your clipboard when
YOU paste into its box, and it only calls public web APIs.
zKillboard asks every API user to identify themselves in the User-Agent and to be
polite with request volume. Pass --contact (email, site or Discord name) or set the
EVE_HUD_CONTACT environment variable. Requests to zKillboard are spaced >= 1.2 s
apart, results are cached for an hour on disk, and a 403/429 stops the scan instead
of retrying (retrying while blocked is how IPs get banned).

Clipboard watch (on by default, checkbox in the window): copy a character name anywhere
(local chat, a browser, ...) and the HUD scans it automatically. PRIVACY: it looks at
your clipboard text locally and only acts on text that looks like an EVE character name
(3-37 chars, letters/digits/space/'/-, at most 3 words, at least one letter, not a
password-looking token such as one long word mixed with digits). Anything else is ignored
and never stored or sent. A name-shaped string IS sent to CCP's ESI to look it up, so
untick the box (or close the HUD) before copying anything sensitive that could look like a
name. Text that is already in the clipboard when you start or re-enable the watch is
skipped. Names with unusual characters can still be pasted into the box by hand.

Keys:  Enter = scan the box    Ctrl+V in the box = replace contents and scan
       Esc = clear and focus the box        Ctrl+Up / Ctrl+Down = opacity

How the cyno check works
  Killmails list the modules on the VICTIM only, so the check looks at the
  character's recent LOSSES (up to 25) for any "... Cynosural Field Generator".
  YES      = at least one recent loss had a cyno module fitted
  NO       = losses were checked and none had one (a cyno alt that never lost a
             cyno ship will still show NO)
  UNKNOWN  = no recent losses to check
  It is a heuristic, not proof.

Sample sizes: solo/fleet ratio uses the latest <= 1000 PvP kills zKillboard returns
(newest first); ship usage and fleet size use the latest 50 kills + 25 losses.
EVE Char Intel v1.2: what's new
November 2026. Replaces v1.1. Just swap the .exe: your settings and cache stay in the EVE-Char-Intel-data folder next to it.
New
Pilot + Ship: see the fit. Paste Pilot Name - Ship (for example Aiko Bianchi - Loki) to get the fit from that pilot's latest loss of that ship. Handy when what he flies now is not in his top 3. It shows slots, loaded charges and drones, with a Copy EFT button for the in-game fitting window or Pyfa.
Separators: | ; , : / > -> =>, a spaced dash, or brackets: Pilot (Ship). The order can be swapped. Use the ship's exact in-game name.
The clipboard watch auto-scans it when the separator has spaces around it (Pilot - Ship).
Fits older than a year are not shown.
Tray icon and global hotkey (Windows). Left-click the tray icon to show or hide the HUD; right-click for a menu. The minimize button and a new Tray button send it to the tray. Ctrl+Alt+F10 brings the HUD above all windows and focuses the name box; press it again to hide it. Change or disable it in eve_char_intel_config.json: {"hotkey": "ctrl+shift+f9", "tray": true, "minimize_to_tray": true} ("hotkey": "" turns it off).
Good to know
Pick a hotkey EVE does not use: a global hotkey is taken before the game sees it. If another program already owns the combination, the status line says so.
To see the HUD over EVE, run the game in Fixed window or borderless mode; Windows cannot draw over exclusive fullscreen.
This build is unsigned. Windows SmartScreen may warn and some antivirus engines may give a false alarm. 
