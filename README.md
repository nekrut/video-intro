# video-intro

A CLI tool to add a title screen image to the beginning of a video. Perfect for adding branded intro screens to screencasts, tutorials, and presentations.

## Features

- Prepends a static image as an intro to any video
- Automatically matches the intro to the video's resolution, frame rate, and pixel format
- Handles videos with or without audio tracks
- Scales and pads images to fit the video dimensions while preserving aspect ratio

## Requirements

- Python 3.10+
- FFmpeg (with libx264 support)

### Installing FFmpeg

**macOS:**
```bash
brew install ffmpeg
```

**Ubuntu/Debian:**
```bash
sudo apt install ffmpeg
```

**Windows:**
Download from https://ffmpeg.org/download.html

## Installation

Clone the repository and make the script executable:

```bash
git clone https://github.com/nekrut/video-intro.git
cd video-intro
chmod +x video-intro
```

Optionally, add to your PATH:

```bash
ln -s $(pwd)/video-intro /usr/local/bin/video-intro
```

## Usage

```bash
video-intro -i <image> -v <video> -d <duration> -o <output>
```

### Arguments

| Argument | Description |
|----------|-------------|
| `-i, --image` | Path to the title screen image (PNG, JPG, etc.) |
| `-v, --video` | Path to the input video (MP4) |
| `-d, --duration` | Duration of the title screen in seconds |
| `-o, --output` | Path for the output video |

### Examples

Add a 5-second intro:
```bash
video-intro -i title.png -v screencast.mp4 -d 5 -o final.mp4
```

Add a 3-second intro with full paths:
```bash
video-intro --image ~/designs/logo.png --video ~/recordings/demo.mp4 --duration 3 --output ~/output/demo_with_intro.mp4
```

## How It Works

1. Analyzes the input video to extract resolution, frame rate, and pixel format
2. Scales the input image to match the video dimensions (with padding if aspect ratios differ)
3. Creates a video segment from the image with matching properties
4. If the original video has audio, adds a silent audio track to the intro
5. Concatenates the intro and original video using FFmpeg's filter_complex

## Output Quality

The tool uses the following encoding settings:
- Video codec: H.264 (libx264)
- Preset: fast
- CRF: 18 (high quality)
- Audio codec: AAC at 192kbps (if audio present)

## License

MIT
