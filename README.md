# yt-dlp_video_downloader_CLI

## Installation

```bash
uv sync
```

## Usage

```bash
yt-dlp 'URL'
```

## Project structure

```plaintext
.
├─ .venv/
├─ videos/
├─ .gitignore
├─ .python-version
├─ pyproject.toml
├─ README.md
└─ uv.lock
```

## Shorten the output filename

```bash
# The output filename will be the video ID and the file extension
yt-dlp -o "%(id)s.%(ext)s" "<URL>"

# The output filename will be the first 50 characters of the video title, followed by the video ID and the file extension
yt-dlp -o "%(title).50s-%(id)s.%(ext)s" "<URL>"
```
