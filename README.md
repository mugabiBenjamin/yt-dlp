# yt-dlp Video Downloader CLI

A command-line video downloader powered by yt-dlp. This project provides a simple way to download videos and playlists from supported websites directly from your terminal.

## Features

- Download videos from supported websites.
- Download entire playlists.
- Customize output filenames.
- Include video IDs in filenames to avoid naming conflicts.
- Manage dependencies using uv.
- Use an isolated Python virtual environment.

## Prerequisites

Before installing the project, ensure you have the following:

- **Python 3.14 or later**
- **uv** – Python package and project manager.
- **Git** – For cloning the repository.
- **FFmpeg** (recommended) – For merging separate video and audio streams and post-processing downloads.

### Verify your installations

```bash
python3 --version
uv --version
git --version
ffmpeg -version
```

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/mugabiBenjamin/yt-dlp.git
```

### 2. Navigate into the project directory

```bash
cd yt-dlp
```

### 3. Install dependencies

```bash
uv sync
```

This command automatically:

- Creates a virtual environment (`.venv`) if one does not exist.
- Installs the Python version specified in `.python-version` when needed and available.
- Installs project dependencies defined in `pyproject.toml`.
- Updates the environment using `uv.lock`.

### 4. Activate the virtual environment

```bash
source .venv/bin/activate
```

Once activated, you can execute yt-dlp directly from your terminal.

Verify the installation:

```bash
python --version
yt-dlp --version
```

Alternatively, you can run commands without manually activating the virtual environment by using `uv run`.

## Usage

The basic syntax is:

```bash
yt-dlp "URL"
```

For example:

```bash
yt-dlp "https://www.youtube.com/watch?v=VIDEO_ID"
```

You can also use `uv run`:

```bash
uv run yt-dlp "URL"
```

### Download a playlist

```bash
yt-dlp "PLAYLIST_URL"
```

### Download to a specific directory

```bash
yt-dlp -P "videos" "URL"
```

By default, downloads are saved to the current working directory unless another output path is specified.

## Customize Output Filenames

yt-dlp supports output templates that allow you to control how downloaded files are named.

### 1. Use the video ID as the filename

The downloaded file will use the video ID followed by its file extension.

```bash
yt-dlp -o "%(id)s.%(ext)s" "URL"
```

Example:

```text
NQ6jbKqkJ0s.mp4
```

### 2. Use the first 50 characters of the title and the video ID

```bash
yt-dlp -o "%(title).50s-%(id)s.%(ext)s" "URL"
```

Example:

```text
Introduction-to-Python-Programming-NQ6jbKqkJ0s.mp4
```

### 3. Save downloads inside the videos directory

```bash
yt-dlp -P "videos" -o "%(title).50s-%(id)s.%(ext)s" "URL"
```

## Useful yt-dlp Options

| Option              | Description                                                                 |
| ------------------- | --------------------------------------------------------------------------- |
| `-F`                | List available video and audio formats.                                     |
| `-f`                | Select a specific download format.                                          |
| `-o`                | Customize the output filename.                                              |
| `-P`                | Specify the download directory.                                             |
| `--playlist-items`  | Download specific playlist items.                                           |
| `--no-playlist`     | Download only the specified video, even when its URL belongs to a playlist. |
| `--write-thumbnail` | Download the video thumbnail.                                               |
| `--embed-thumbnail` | Embed the thumbnail into supported media files.                             |
| `--embed-metadata`  | Embed metadata into the downloaded file.                                    |

For a complete list of available options:

```bash
yt-dlp --help
```

Official documentation: [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)

## Project Structure

```text
yt-dlp/
├── .venv/              # Project virtual environment (generated)
├── videos/             # Downloaded videos
├── .gitignore          # Git exclusion rules
├── .python-version     # Required Python version
├── pyproject.toml      # Project configuration and dependencies
├── uv.lock             # Locked dependency versions
└── README.md           # Project documentation
```

## Dependency Management

This project uses uv to manage Python dependencies.

Install or synchronize dependencies:

```bash
uv sync
```

Reinstall dependencies if the environment encounters installation problems:

```bash
uv sync --reinstall
```

Add a new dependency:

```bash
uv add PACKAGE_NAME
```

Remove a dependency:

```bash
uv remove PACKAGE_NAME
```

## Troubleshooting

### 1. yt-dlp: command not found

Ensure that the virtual environment is activated:

```bash
source .venv/bin/activate
```

Alternatively, execute yt-dlp through uv:

```bash
uv run yt-dlp --version
```

If the executable is missing, synchronize dependencies again:

```bash
uv sync --reinstall
```

### 2. Python version mismatch

Check the configured Python version:

```bash
cat .python-version
```

Check the active Python interpreter:

```bash
python --version
```

If necessary, recreate the virtual environment:

```bash
uv venv --python 3.14 --clear
uv sync
```

### 3. FFmpeg not found

Install FFmpeg if you need audio/video merging or post-processing.

On Ubuntu:

```bash
sudo apt update
sudo apt install ffmpeg
```

Verify:

```bash
ffmpeg -version
```

## Development Environment

This project can be used on Linux, macOS, and Windows.

For Windows users working with WSL, it is recommended to keep the project inside the Ubuntu filesystem (for example, `~/Projects/yt-dlp`) rather than the mounted Windows filesystem (`/mnt/c/`).

This generally provides better filesystem performance and compatibility with Linux development tools.

## Notes

- Download availability depends on the source website and its restrictions.
- Some websites may require authentication or additional configuration.
- Respect copyright laws, website terms of service, and content ownership when downloading videos.
- The `.venv/` directory and downloaded videos are excluded from version control.

## License

This project is intended for personal and educational use. Refer to the licensing terms of yt-dlp and the applicable content providers when using the downloader.

[Back to Top](#yt-dlp-video-downloader-cli)
