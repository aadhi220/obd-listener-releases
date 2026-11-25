# OBD Listener releases

Downloads for **OBD Listener**, an OBD-II toolkit for cheap ELM327 Bluetooth adapters:

- **Windows:** a PC dashboard, an engine simulator and adapter diagnostic tools.
- **Android:** a dashboard app made for car head units.

This repository holds only the release files; the source code is kept elsewhere. Get the files from
[Releases](../../releases).

| File | What it is |
|---|---|
| `obd-listener-<version>-windows-x64.exe` | Windows 10/11 program: dashboard, simulator, adapter tools. Nothing to install. |
| `obd-dash-<version>.apk` | Android app (Android 5.0+) for head units and phones |
| `SHA256SUMS.txt` | checksums to verify the downloads |

## Windows: obd-listener.exe

**Double-click it** to start a demo:

- The built-in engine simulator and the dashboard start, and your browser opens the dashboard and the simulator's
  controls.
- In the simulator, press **Start**, use the pedal (↑/↓ keys), and turn on **Sound** for engine noise.
- Close the console window to stop.

**Windows SmartScreen:** the exe isn't code-signed, so Windows may show "Windows protected your PC". Click
**More info → Run anyway**. You can check the file against `SHA256SUMS.txt` first:

```powershell
Get-FileHash .\obd-listener-0.4.0-windows-x64.exe -Algorithm SHA256
```

**With a real adapter**, open a terminal in the download folder:

```powershell
.\obd-listener-0.4.0-windows-x64.exe listen scan
```
```powershell
.\obd-listener-0.4.0-windows-x64.exe dash --ble AA:BB:CC:DD:EE:FF
```

Then open http://127.0.0.1:8780.

- **Other adapters:**
  - Bluetooth Classic or USB: `dash --port COM5`; pair it in Windows first (PIN 1234 or 0000).
  - Wi-Fi: `dash --tcp 192.168.0.10:35000`.
- **Adapter report:** `listen probe --ble <address>` writes a report of what your adapter and car support.
- **All options:** run with `--help` (for example `dash --help`).

**Replay a drive** with **▶ Replay** in the dashboard: a timeline shows the drive's speed and RPM with your MARK
presses. Drag it to jump to the part you want to show; Space plays/pauses, `[` `]` skip 10 s, `M` goes to the next MARK.

**Drives from your phone:** click **⇄ Sync → Pair a phone** and scan the QR code with the Android app in Phone mode. At home,
opening the app on the phone (same Wi-Fi) sends the drives it collected in the car to this PC. Allow the app on
private networks if Windows asks.

**Your data** goes to `Documents\OBD Listener`: probe reports, dashboard recordings, uploads from the head-unit
app, and your edited layouts. Nothing is sent anywhere.

## Android: obd-dash.apk

1. **Install:** copy the APK to the device and open it. Allow "install unknown apps" for your file manager when
   asked.
2. **Choose the mode:** on first launch, pick **Head unit** or **Phone**.
3. **Head unit mode:** the dashboard talks to the BLE adapter directly and records every drive. Tap the dot at the
   top right for settings: adapter, layout, recording, and the unusable strip at the bottom of the screen (30 % by
   default, for units whose lower screen doesn't respond).
4. **Replay:** Settings → **Replay a drive** plays a recorded drive with a timeline (seek, ±10 s, next MARK,
   speed). ✕ goes back to live data.
5. **Phone mode:** install the same APK on your phone and pick **Phone**. On the head unit: Settings → **Pair a
   phone**, then point the phone's camera at the QR code and tap the link. From then on, opening the app on the
   phone (with the head unit on its hotspot) copies new drives to the phone; sending them on to the laptop is
   handled by the PC app's **⇄ Sync** (see above).
6. **Phone as a full app:** the phone screen's **Your car** section has a live dashboard (connects to the adapter
   and records), replay and trouble codes.

## Safety

The tools only read from the car, except **Clear codes**, which always asks for confirmation. Don't use the
dashboard in a way that takes your attention off the road.

Not affiliated with any vehicle or adapter manufacturer.
