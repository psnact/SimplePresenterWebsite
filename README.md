# SimplePresenter Website

This is a simple static website (no build step) for the **SimplePresenter** app.

## Update the download link

The Windows download button points to:

`https://github.com/psnact/SimplePresenter/releases/latest/download/SimplePresenter-Setup.exe`

The macOS download button points to:

`/downloads/SimplePresenterSetup.dmg`

To make downloads work:

1. Create a folder named `downloads` next to `index.html`
2. (Optional) If you prefer hosting the Windows installer yourself instead of GitHub Releases, update `index.html` and put the EXE in `downloads/`.

For macOS:

3. Copy your macOS installer into the same `downloads` folder and name it **`SimplePresenterSetup.dmg`**
   - If your installer is a `.pkg` instead, update the link in `index.html` to match the file name.

If you prefer hosting the installer somewhere else (GitHub Releases, Google Drive, etc.), edit `index.html` and replace the download link.

## Run locally

Open `index.html` directly in your browser, or use a simple local server.

The documentation page is available at `docs.html` (source text in `index.md`).

If you have Python installed:

```bash
python -m http.server 5173
```

Then open:

`http://localhost:5173`


Create the Release here
https://github.com/psnact/SimplePresenter/releases
