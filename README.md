# Simple Internet Connection Monitor

A small desktop app that shows, at a glance, whether your internet connection is working, and makes
it impossible to miss when it drops.

- A green / amber / red light in the window and the system tray.
- When the connection goes: a notification, a sound, the window flashes red and comes to the front.
  Each of these can be turned off.
- Says where the fault is: **your side** (Wi-Fi, cable, router) or **beyond your router** (your ISP).
- Spots hotel and guest Wi-Fi sign-in pages.
- Keeps a log of every outage, with start, end and how long it lasted.

No installer, no account, no admin rights, nothing sent anywhere. One file.

## Download

From the [latest release](../../releases/latest):

| System | File | |
|---|---|---|
| Windows 10 / 11 (64-bit) | `sicm.exe` | Download and run. Windows SmartScreen may warn about an unknown app the first time: *More info → Run anyway*. |
| Linux x86-64 (glibc 2.35+: Ubuntu 22.04, Debian 12, Fedora 36 or later) | `sicm-linux-x86_64` | `chmod +x sicm-linux-x86_64` and run. The tray icon needs a desktop with a system tray (KDE, Cinnamon, XFCE; GNOME with the AppIndicator extension). |
| macOS 11 or later (Apple silicon and Intel) | `sicm-macos.zip` | Unzip and drag *Simple Internet Connection Monitor* to Applications. Not yet signed by Apple, so the first open needs one extra step: see below. |

Each release lists the SHA-256 of every file.

### Opening it on a Mac the first time

The Mac app is not yet notarised by Apple, so macOS will not open it straight away:

1. Double-click it. macOS says it cannot check the app for malicious software. Press **Done**.
2. Open **System Settings → Privacy & Security** and scroll down. Next to the message about
   *Simple Internet Connection Monitor*, press **Open Anyway**, then confirm.

After that it opens normally. (On macOS 15 and later, right-click → Open no longer skips this.)

## How it checks

Every 3 seconds it tries, at once:

| Check | How |
|---|---|
| Router | connects to your router |
| Internet | connects to three independent public servers (1.1.1.1, 8.8.8.8, 9.9.9.9) |
| DNS | looks up a name |
| Login page | fetches a page that should be empty; anything else means a sign-in page is in the way |

- **Online**: the internet servers answer and names resolve.
- **Degraded** (amber): some checks fail, or responses are slow (over 500 ms).
- **Offline** (red): no internet server answers for 3 checks in a row (about 9 s). One bad check never
  raises an alarm. It goes back to Online after 2 good checks.

No ping is used (that needs admin rights on some systems); plain connections work everywhere.

## Using it

- Closing the window hides it to the tray; it keeps watching. Click the tray icon to bring it back.
  Right-click for Pause, Open log and Quit.
- **Settings** (bottom right): check interval, sound, flash, bring to front, keep on top.
- Settings (`settings.json`) and the outage log (`outages.csv`) live in your user config folder:
  `%APPDATA%\sicm` on Windows, `~/.config/sicm` on Linux. The addresses it checks can be changed in
  `settings.json`.

## Licence

MIT. Free to use and share.
