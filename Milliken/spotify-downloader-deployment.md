# Spotify Downloader (spotDL) Deployment Guide

## Prerequisites

1. Python 3.7 or higher
2. pip (Python package manager)
3. FFmpeg
4. Poetry (Python dependency management tool)

## Installation Steps

### 1. System Requirements

```bash
# Install Python and pip if not already installed
sudo apt-get update
sudo apt-get install python3 python3-pip

# Install FFmpeg
sudo apt-get install ffmpeg

# Install Poetry
pip3 install poetry
```

### 2. Clone the Repository

```bash
git clone https://github.com/spotDL/spotify-downloader.git
cd spotify-downloader
```

### 3. Install Dependencies

```bash
# Install project dependencies using Poetry
poetry install
```

### 4. Configure the Environment

The spotify-downloader requires a Spotify API client ID and client secret. You need to:

1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard)
2. Create a new application
3. Get the client ID and client secret
4. Set up the environment variables:
   ```bash
   export SPOTIFY_CLIENT_ID='your_client_id'
   export SPOTIFY_CLIENT_SECRET='your_client_secret'
   ```

### 5. Usage

Basic usage examples:

```bash
# Activate the poetry environment
poetry shell

# Download a song
spotdl [spotify_link]

# Download multiple songs
spotdl [spotify_playlist_link]

# Download with specific options
spotdl --output "{artist} - {title}.{ext}" [spotify_link]
```

## Common Issues and Troubleshooting

1. FFmpeg Installation Issues:
   - If FFmpeg installation fails through apt, you can download it directly from the official website
   - Alternative installation through snap: `sudo snap install ffmpeg`

2. Poetry Environment Issues:
   - Make sure to run commands within the poetry shell
   - If poetry shell fails, try using `poetry run spotdl` instead

3. Download Issues:
   - Ensure you have a stable internet connection
   - Verify that the Spotify link is valid and accessible
   - Check if you have sufficient disk space

## Additional Resources

- Official Documentation: [https://github.com/spotDL/spotify-downloader/wiki](https://github.com/spotDL/spotify-downloader/wiki)
- Issue Tracker: [https://github.com/spotDL/spotify-downloader/issues](https://github.com/spotDL/spotify-downloader/issues)
- Project License: MIT

Note: This guide was created based on the deployment attempt on June 3, 2025. The actual installation process might vary depending on your system configuration and the project's current state.