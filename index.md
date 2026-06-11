# SimplePresenter Documentation

SimplePresenter is a lightweight presentation app designed for churches. It lets you quickly project:

- Bible passages
- Song lyrics
- Background images and videos
- Media items (files)
- (Optional) YouTube items
- PowerPoint slides

It supports a "service order" workflow with playlists, and it can provide an OBS-friendly browser overlay.

---

## Download & Install

### Windows (recommended)

1. Download the installer from your website or from GitHub Releases.
2. Run `SimplePresenter-Setup.exe`.
3. Finish the installer.
4. Launch **SimplePresenter** from the Start Menu.

### macOS

1. Download the latest `.dmg` from GitHub Releases or website.
2. If using a `.dmg`, open it and drag **SimplePresenter.app** to **Applications**.
3. Launch **SimplePresenter** from **Applications**.

---

## System Requirements

### Windows

- Windows 10/11
- 64-bit CPU
- A second display or projector is recommended

### macOS

- macOS (64-bit)
- A second display or projector is recommended

### Notes on background video playback

For best results:

- Use H.264 encoded video backgrounds.
- Prefer 1080p backgrounds (or test higher resolutions first).

---

## First Launch Checklist

1. Open **SimplePresenter**.
2. Go to **Tools -> Settings**.
3. Configure:
   - Projection text appearance (font, size, colors)
   - Default backgrounds
4. Test output:
   - Project a Bible verse
   - Project a song section
   - Try an image/video background

---

## The Main Window (Operator View)

The main window is designed for the operator (the person controlling the service). It contains:

- A **content area** with tabs (Bible, Songs, and additional content tabs)
- A **playlist panel** (service order)
- **Preview canvases** showing what will appear on outputs

---

## Outputs (What People See)

SimplePresenter can render content to output canvases.

- **Projection output**: the main congregation-facing output.
- **Secondary output**: an additional output that can be used for livestream, confidence, or alternative formatting.

If you use a projector / second screen:

- The projection output is intended to be full-screen on the external display.
- You can also toggle fullscreen with `F11` (if enabled in your build).

---

## Bible Projection

### Where Bible files go

SimplePresenter loads Bible translations from the application Bible folder.

- **Preferred (cross-platform):** your system AppData folder
  - Windows example:
    - `%LOCALAPPDATA%\SimplePresenter\SimplePresenter\Bible`
  - macOS example:
    - `~/Library/Application Support/SimplePresenter/Bible`

- **Windows legacy fallback (supported):**
  - `C:\SimplePresenter\Bible`

If no Bible XML files exist yet, SimplePresenter can copy built-in default Bibles into the Bible folder.

### Supported Bible XML formats

SimplePresenter supports both:

- A newer `XMLBIBLE` format
- An older `bible/book/chapter/verse` format

Example (`XMLBIBLE` format):

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<XMLBIBLE biblename="KJV">
  <BIBLEBOOK bname="John">
    <CHAPTER cnumber="3">
      <VERS vnumber="16">For God so loved the world...</VERS>
    </CHAPTER>
  </BIBLEBOOK>
</XMLBIBLE>
```

Example (older format):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bible translation="KJV">
  <book name="John">
    <chapter number="3">
      <verse number="16">For God so loved the world...</verse>
    </chapter>
  </book>
</bible>
```

### Quick reference lookup

1. Open the **Bible** tab.
2. Type a reference:
   - `John 3:16`
   - `John 3:16-18`
   - `Psalm 23`
3. Press Enter.
4. Click **Project**.

### Search by text

1. Open the **Bible** tab.
2. Type a keyword (example: `love`).
3. Click a result.
4. Click **Project**.

### Navigate verses

Use **Previous** and **Next** to step through a passage verse-by-verse.

---

## Songs (Lyrics)

### Where songs go

Songs are loaded from the `data/songs/` folder.

- In a standard install, this folder is located next to the application (inside the install directory).

### Supported song formats

- `.txt`
- `.xml`

### Simple `.txt` format (recommended)

- Each song is a text file.
- Blank lines separate sections.
- The filename becomes the song title.

Example: `Amazing_Grace.txt`

```text
Amazing grace how sweet the sound
That saved a wretch like me

I once was lost but now am found
Was blind but now I see
```

### How to add songs

1. Create a `.txt` file inside `data/songs/`.
2. Put lyrics in the file.
3. In the Songs panel, click **Refresh** (if available).

### Projecting a song

1. Open the **Songs** tab.
2. Select a song.
3. Select a section.
4. Click **Project Section**.

---

## Media (Images and Videos)

SimplePresenter supports background and media playback.

### Supported formats

- Images: PNG, JPG, JPEG, BMP
- Videos: MP4, WebM, AVI, MOV

### Tips

- For consistent results, keep backgrounds at 1080p.
- For videos, prefer H.264 encoded MP4.

---

## YouTube (Optional)

Some builds of SimplePresenter include an embedded browser (Qt WebEngine) that enables YouTube items.

If your build includes this feature:

- You can add YouTube items to the playlist.
- You can control playback via the media controls.

If your build does not include WebEngine, YouTube features will not be available.

---

## PowerPoint

SimplePresenter includes a PowerPoint workflow for projecting slides.

- Import a PowerPoint presentation in the PowerPoint panel.
- The app may generate slide images temporarily while the presentation is in use.

Temporary files used for PowerPoint are cleaned up automatically when the app exits.

---

## Playlist (Order of Service)

Playlists let you prepare the full order of service and then step through it live.

### Create a new playlist

- Use **File -> New Playlist** (`Ctrl+N`).

### Add items

Depending on your build, playlists can include:

- Bible references
- Songs
- Media files
- YouTube items

### Reorder items

- Drag-and-drop (if enabled), or use Move Up / Move Down.

### Save and load

- Save: **File -> Save Playlist** (`Ctrl+S`)
- Load: **File -> Open Playlist** (`Ctrl+O`)

Playlists are stored as `.service` files (JSON).

---

## Notes (Operator Notes)

SimplePresenter includes an operator notes area for service notes.

- Notes are designed for the operator.
- Notes are not intended to appear on the projection output (unless you choose to display them via overlays / OBS).

---

## OBS Browser Overlay (Livestream)

SimplePresenter includes a built-in **OBS Browser Overlay** so your livestream can automatically show the currently projected:

- Bible text + reference
- Media (image/video) preview card
- (Optional) YouTube preview card
- (Optional) Notes overlay image

### How it works

- SimplePresenter starts a local HTTP server for the overlay page.
- It also starts a WebSocket server used for **media / YouTube playback sync**.

### URLs and ports

- **Overlay page (OBS Browser Source)**
  - `http://localhost:8080/overlay`
  - (`http://localhost:8080/` also works)

- **WebSocket (sync channel)**
  - `ws://localhost:8081`

### OBS setup (recommended)

1. Open OBS.
2. In **Sources**, click `+`.
3. Choose **Browser**.
4. Set **URL** to:
   - `http://localhost:8080/overlay`
5. Set **Width** and **Height** to match your OBS canvas (recommended):
   - `1920` x `1080`
6. Click **OK**.

The overlay page has a transparent background, so you can place it above your camera/game capture.

### Important notes

- The overlay server is intended to run on the **same computer as OBS**.
  - The overlay page hard-codes `ws://localhost:8081` for sync, which will not work if OBS is on another PC.
- If another app is already using port `8080`, the overlay server will fail to start.

---

## File Locations

### Bible translations

- Preferred:
  - `%LOCALAPPDATA%\SimplePresenter\SimplePresenter\Bible`
  - `~/Library/Application Support/SimplePresenter/Bible`

- Windows legacy fallback:
  - `C:\SimplePresenter\Bible`

### Songs

- `data/songs/`

### Saved playlists

- `data/services/`

### Backgrounds

- `data/backgrounds/`

---

## Keyboard Shortcuts

Common shortcuts:

- `Ctrl+N`: New playlist
- `Ctrl+O`: Open playlist
- `Ctrl+S`: Save playlist
- `Esc`: Clear overlays

(Some builds may include additional shortcuts.)

---

## Troubleshooting

### "Missing DLL" on Windows

If SimplePresenter fails to start due to missing DLLs, reinstall using the latest installer and ensure you are using the official release build.

### Bible translations not appearing

- Confirm you placed `.xml` Bible files in the Bible folder.
- Restart the app.
- Ensure the XML file is valid UTF-8.

### Songs not appearing

- Confirm songs are in `data/songs/`.
- Confirm the file extension is `.txt` or `.xml`.
- Use the Songs panel refresh button if available.

### Video background stutters

- Use a lower-resolution video.
- Re-encode to H.264.
- Test on the target machine and projector resolution.

### OBS overlay not working

- Confirm SimplePresenter is running (it starts the overlay server on launch).
- Confirm you can open this in a normal browser on the same PC:
  - `http://localhost:8080/overlay`
- Ensure **port `8080`** is not already in use (overlay page).
- Ensure **port `8081`** is not blocked (WebSocket sync).
- If the overlay loads but doesn’t update:
  - Remove and re-add the OBS Browser Source.
  - In the Browser Source properties, use **Refresh cache of current page**.

---

## Updates

### Windows

Windows builds can support in-app update checks. The updater reads a simple `update.json` feed and downloads the installer.

### macOS

macOS updates are manual:

1. Open **Help -> Check for Updates...**
2. Download the latest macOS build.
3. Quit SimplePresenter.
4. Replace `SimplePresenter.app` in `/Applications`.

---

## Support

- Issues / bug reports:
  - https://github.com/psnact/SimplePresenter/issues

If you want, tell me what support contact you want on the website (email, Discord, etc.) and I’ll add it here.
