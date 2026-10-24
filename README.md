# MSCW Buff Tracker

A Windows desktop companion for MapleStory Classic World that notifies you when selected buffs disappear.

MSCW Buff Tracker recognizes buff icons from the visible game screen and alerts you with a popup, a sound, or a spoken notification such as **“Haste buff ended.”**

## **DO NOT BLOCK OR COVER THE BUFF ICONS IN THE TOP-RIGHT CORNER OF THE GAME SCREEN.**

## Download

Get the Windows app from [GitHub Releases](https://github.com/Song-HyunSeok/MSCW-Buff-Tracker/releases).

Download the **windows-x64 ZIP**, extract the entire archive, and run **MSCWBuffTracker.exe** inside the extracted folder.

Keep the executable, `_internal`, `assets`, `skills.json`, `updates.json`, and the included license notices together. Do not run the app directly from inside the ZIP.

## Features

- Automatically detects the MapleStory window.
- Watches an **800 × 60 pixel area** at the top-right of the game client, following the window when it moves or resizes.
- Tracks **21 distinct buff skills**, with individual notification toggles.
- Offers sound, popup, or combined notifications.
- Includes five notification tones, plus **Female Voice** and **Male Voice**.
- Provides a notification-volume slider with mute at 0%.
- Shows compact, movable popups with the skill name and reference icon.
- Supports light/dark mode, window transparency, and Always on top.
- Checks GitHub Releases for updates manually or optionally at startup.

## Getting started

1. Open MapleStory in windowed or borderless mode, keeping the top-right buff row visible.
2. Launch **MSCWBuffTracker.exe**.
3. In **Skills**, check the buffs you want alerts for.
4. Open **Settings** to choose your notification mode, sound, and volume. Use **Test Notification** to preview an alert.
5. Press **Start** and return to the game.

Press **Pause** to stop tracking or change Settings. Settings is disabled while tracking runs. Minimize uses the normal Windows taskbar; closing the app exits it.

A buff must first be recognized on two consecutive scans before its disappearance can trigger an alert. A buff that has never been recognized will not generate a missing-buff notification.

## Settings

| Setting | What it does |
| --- | --- |
| Mode | Select Light or Dark appearance. |
| Transparency | Adjust the main window from 0% to 80% transparency. |
| Always on top | Keep the tracker above other windows. |
| Check for updates on startup | Check GitHub Releases when the app opens. Off by default. |
| Notification | Choose Sound +Popup, Sound only, or Popup only. |
| Sound | Choose Chime, Double beep, Rising tones, Falling tones, Low pulse, Female Voice, or Male Voice. |
| Volume | Adjust notification audio from 0% to 100%, without changing other applications’ volume. |
| Test Notification | Preview the selected notification mode using Haste. Test popups show **[Testing]**. |
| Move Popup | Open a preview that you can drag to your preferred location. Its position is saved. |
| Check for Updates | Display the latest release information within Settings. |
| Download Update | Open the release page when a newer version is available. |

Normal popups show **Ended**, the skill name, and its icon. Their background is 70% transparent with a thin black border; text and icons remain opaque. The popup background is separate from the main window’s Transparency setting.

Spoken alerts work offline and use the same Volume setting as notification tones. When several alerts arrive together, their audio plays sequentially.

## Supported buffs

### Party Buffs

| Skill | Class |
| --- | --- |
| Rage | Fighter |
| Meditation | 2nd Job Wizard |
| Bless | Cleric |
| Haste | 2nd Job Rogue |

### Self Buffs

| Skill | Class |
| --- | --- |
| Iron Body | Warrior |
| Sword Booster | Fighter, Page |
| Axe Booster | Fighter |
| Blunt Weapon Booster | Page |
| Spear Booster | Spearman |
| Polearm Booster | Spearman |
| Iron Will | Spearman |
| Magic Guard | Magician |
| Magic Armor | Magician |
| Invincible | Cleric |
| Focus | Bowman |
| Bow Booster | Hunter |
| Crossbow Booster | Crossbowman |
| Soul Arrow | 2nd Job Bowman |
| Claw Booster | Assassin |
| Dagger Booster | Bandit |

## How tracking works

Detection runs locally on visible screen pixels. The application does not use a game API, read game memory, sniff packets, or automate game input. Normal tracking does not save screenshots. Update checks contact GitHub; captured game images are not sent with those requests.

| Status | Meaning |
| --- | --- |
| Off | Notifications for this skill are disabled. |
| Not detected | The skill has not been confirmed yet. |
| Confirming | The icon was recognized and is awaiting another matching scan. |
| Active | The buff has been confirmed. |
| Confirming loss | The previously active icon is no longer recognized; disappearance is being checked. |
| Expired | The disappearance was confirmed and an alert was triggered. |
| Paused | Capture is temporarily unavailable. |

## Limitations and troubleshooting

- Keep the buff row visible. A minimized game, an overlapping window, or unavailable capture can pause tracking.
- The fixed capture area assumes a single buff row at the top-right. Wrapped rows, letterboxing, unusual UI scaling, or icons taller than the capture area may not work correctly.
- Countdown text, shading, animations, and similar-looking icons can affect recognition. Recognition has been tested against supplied gameplay samples, but accuracy is not guaranteed across every class or display setup.
- Pause tracking during loading screens or menus that hide the buffs to avoid false expiration alerts.
- After a long capture interruption, a game-window change, or a resolution/DPI change, buffs must be recognized again. Brief interruptions preserve confirmed buffs for up to five seconds.
- Exclusive fullscreen or capture restrictions may require switching to windowed or borderless mode.

## Updates and saved settings

Updates are checked against this repository’s published, stable GitHub Releases. Version tags use the format `v0.1.1`. A repository without an accessible published release cannot offer an update yet.

Update results, release notes, and the download button appear **inside Settings**, without an update popup. The app does not automatically download, install, or replace files.

To update, close the app, extract the newer Windows release, and run its executable. Preferences are stored separately in:

```text
%LOCALAPPDATA%\MSCWBuffTracker\settings.json
```


The complete portable application is written to `dist/MSCWBuffTracker`. ZIP that entire folder for a Windows release. Generated files such as `preview.png` are not required for distribution.

### Update reference images

Reference icons remain external in `assets/icons`, with their paths and detection settings defined in `skills.json`. Replace the relevant PNGs and restart the app to load them; the tracking code does not need to be rebuilt for an image-only replacement.

Keep existing skill IDs unchanged to preserve user selections. New skills need corresponding voice files in `assets/sounds/voice-female` and `assets/sounds/voice-male` if they should support spoken alerts. The update source is configured in `updates.json`.

## Attribution and license

**The project’s source-code license is pending.** No MIT or other project license has been selected.

Dependency licenses are included in `licenses/`; see [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt) for component and asset attribution. Those dependency licenses are separate from this project’s license.

Skill artwork was supplied through reference material citing MeowDB / MapleStory Classic World and belongs to its respective owners. Voice recordings were generated locally using Microsoft Zira and Microsoft David; the female variant uses a higher pitch. This project does not claim ownership of those third-party assets.

## Feedback

Report bugs or request features through [GitHub Issues](https://github.com/Song-HyunSeok/MSCW-Buff-Tracker/issues). For recognition problems, include the app version, game resolution, display scaling, affected skill, and a cropped image of the buff row when possible. Remove personal information before sharing screenshots.
