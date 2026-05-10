# 📦 Meli-Action

**A GitHub Actions-based tool to bypass internet censorship — download files from direct links, YouTube, Telegram, Google Play, and archive web pages, all through GitHub's unfiltered servers.**

> Originally created by [Kurdeus](https://github.com/Kurdeus/Meli-Action). This is a fork maintained by [iliasoli13](https://github.com/iliasoli13/Meli-Action).

---

## 🌐 How It Works

GitHub Actions run on GitHub's own servers, which are **not blocked** by Iran's national internet filtering (filtering/censorship). This project exploits that fact:

- **For file downloads:** The workflow uses `wget` to fetch the file inside GitHub's runner environment, then `git push`es it directly into your repository — ready for you to download from GitHub normally.
- **For web archiving:** A headless Chromium browser (via `pyppeteer`) fully renders the filtered page, saves it as an MHTML archive, zips it, and pushes it to the repository.
- **For YouTube/Telegram/Google Play:** Dedicated workflows use `yt-dlp` and platform-specific tooling to fetch media and apps, then commit them to the `downloads/` folder.

No software installation on your device is required. Everything runs in the cloud.

---

## ✨ Features

| Feature | Details |
|---|---|
| 📥 **Direct link download** | Downloads any file from a direct URL. Files larger than 99 MB are automatically split into 95 MB chunks (due to GitHub's file size limit) before being committed. |
| 🎬 **YouTube downloader** | Downloads YouTube videos at your chosen quality. Includes a `google_service.json` config for browsing/searching YouTube through a v2ray proxy (note: only search and thumbnails load with this config, not video playback). |
| 📱 **Telegram downloader** | Downloads files from public Telegram channels. |
| 🛍️ **Google Play downloader** | Downloads installable APK files from Google Play. |
| 🌐 **Web page archiver** | Saves filtered/blocked web pages as MHTML archives using a headless browser, then zips them for download. |
| 🔞 **Adult content downloader** | Supports downloading from a certain well-known adult platform — just provide the page URL. (May occasionally error; retry if so.) |
| 🎵 **Spotify & SoundCloud downloader** | Downloads tracks and playlists from Spotify and SoundCloud. |

---

## 🚀 Getting Started

### Step 1 — Fork the Repository

Click the **Fork** button at the top-right of the page to copy this repository into your own GitHub account.

### Step 2 — Enable Actions Write Permissions

The workflows need permission to commit downloaded files back to your repository:

1. Go to **Settings** ⚙️ in your forked repository.
2. In the left sidebar, navigate to **Actions → General**.
3. Under **"Workflow permissions"**, select **"Read and write permissions"**.
4. Click **Save**.

> **Also**, under **"Actions permissions"**, make sure **"Allow all actions and reusable workflows"** is selected.

> 💡 **Security note:** Since you own this fork, granting write permissions to your own workflows is safe.

### Step 3 — Run a Workflow

1. Go to the **Actions** tab in your forked repository.
2. Select the workflow you want to use from the left-hand list (e.g., "Download from URL", "YouTube Downloader", etc.).
3. Click **Run workflow**.
4. Fill in the required parameters (e.g., the URL, video quality, output folder).
5. Click the green **Run workflow** button.

Once the run completes, the downloaded file will appear in the designated folder inside your repository. You can then download it directly from GitHub.

---

## 📁 Repository Structure

```
Meli-Action/
├── .github/
│   └── workflows/          # GitHub Actions workflow definitions
│       ├── download.yml        # Direct URL downloader
│       ├── youtube.yml         # YouTube downloader
│       ├── telegram.yml        # Telegram file downloader
│       ├── googleplay.yml      # Google Play APK downloader
│       ├── mhtml.yml           # Web page archiver
│       └── ...
├── downloads/              # Output folder — downloaded files land here
├── save_as_mhtml.py        # Python script for headless web page archiving
├── google_service.json     # v2ray config for YouTube browsing via proxy
└── README.md
```

---

## ⚙️ Technical Details

### Direct Downloader
Uses `wget` inside the GitHub Actions runner. If the resulting file exceeds GitHub's 100 MB single-file limit, it is automatically split into ≤95 MB parts using a split utility, and each part is pushed separately.

### Web Page Archiver (`save_as_mhtml.py`)
Uses `pyppeteer` (a Python port of Puppeteer) to launch a headless Chromium instance, navigate to the target URL, wait for the page to fully load, and capture it in MHTML format. The resulting archive is then zipped and committed to the repository.

### YouTube Downloader
Powered by `yt-dlp`, supporting quality selection (e.g., 720p, 1080p, audio-only). The `google_service.json` file can be imported into v2ray to enable YouTube search and thumbnail browsing within a proxy setup.

### Telegram Downloader
Targets **public** Telegram channels only. Downloads files attached to messages using Telegram's public API.

### Google Play Downloader
Fetches APK files from the Google Play Store using automation tooling.

---

## 🔄 Updating to the Latest Version

To sync your fork with the latest changes from the upstream repository, click the **Sync fork** button on your repository's main page on GitHub.

---

## 🤝 Contributing

Have an idea for a new downloader or feature? Open an [Issue](https://github.com/iliasoli13/Meli-Action/issues) to suggest it. No promises, but useful ideas that benefit the community will be considered.

---

## ⚠️ Disclaimer

This project is intended for personal use to access content in restrictive network environments. Users are responsible for complying with the terms of service of any platform they interact with, as well as all applicable laws in their jurisdiction.

---

## ⭐ Support

If this tool helped you, please consider starring ⭐ the repository — it helps others find it!

<a href="https://star-history.com/#Kurdeus/Meli-Action&Date">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=Kurdeus/Meli-Action&type=Date&theme=dark" />
    <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=Kurdeus/Meli-Action&type=Date" />
    <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=Kurdeus/Meli-Action&type=Date" />
  </picture>
</a>

---

## 👥 Credits

Thanks to everyone who has contributed to this project!

<a href="https://github.com/Kurdeus/Meli-Action/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Kurdeus/Meli-Action" alt="Meli-Action contributors" width="200"/>
</a>
