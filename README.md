![Apps-reForged-Logo](Apps-reForged.png)

# transcriptForged

A simple, reliable Python script to download English transcripts from YouTube playlists or single videos and save them as clean, paragraph-grouped Markdown files.

## Overview

YouTube aggressively blocks repeated caption requests, even from residential IPs. transcriptForged bypasses these IP blocks using Webshare rotating residential proxies—the method recommended to reliably pull transcripts at scale.

The application groups standard caption lines into readable paragraphs instead of outputting massive blocks of unformatted text or hard-to-read one-liners. It automatically flags transcripts with overly long, unbroken sections (often found in Q&A or monologue videos) so you can review them. Be aware that the final transcript will only be as good as the original automated YouTube transcript.

## Features

- **Playlist or Single-Video Fetching**: Operate in batch or pinpoint exactly what you need.
- **Run-on Detection & Report**: Automatically flags generated markdown files that contain very long, unbroken paragraphs (defaults to 1200 characters).
- **Transient Error Resilience**: Automatically retries on proxy issues or IP blocks to ensure your fetch completes.
- **Smart Pacing & Skipping**: Introduces configurable delays between pulls and skips existing files to prevent overwriting perfectly good transcripts.
- **Safe Credential Handling**: Prompts for Webshare credentials once and saves them locally so you aren't hardcoding secrets.

## Requirements

- Python 3.8+
- `youtube-transcript-api` : Required for accessing YouTube's closed captioning API.
- `yt-dlp` : Required to efficiently extract video IDs from full playlists.
- Webshare Proxy Account : A free tier or paid account is required to access residential rotating proxies.

## Installation

1. Download the script to your local machine. You can clone the repository or download the latest release: `git clone https://github.com/oldmanumby/transcriptForged.git`
2. Change into the project directory: `cd transcriptForged`
3. Install dependencies: `pip install youtube-transcript-api yt-dlp`

## Configuration

When you first run transcriptForged, you'll be prompted to configure your proxy settings. You must set up a Webshare Rotating Residential proxy before proceeding:

1. Go to https://www.webshare.io/ and sign up (the free trial provides enough data for testing).
2. Select **Rotating Residential** proxies (datacenter/static proxies will be blocked by YouTube).
3. From your Webshare dashboard, locate your **Proxy Username** and **Proxy Password**.

When prompted by the script, enter these credentials. All settings are automatically saved to `transcriptForged.conf` in the same directory as the script for future use.

## Usage

You can execute the script from your terminal or command prompt. It will process each video, fetching the transcript via Webshare, and save it as a numbered Markdown file in the `transcripts/` folder.

**Playlist Mode (Default)** Fetch an entire playlist at once: `python3 transcriptForged.py`

**Single Video Mode** Fetch one video at a time using the `--single` flag: `python3 transcriptForged.py --single`

### Example Workflow

1. Run the script and confirm your configuration prompts.
2. Select your delay pacing (e.g., 30 seconds).
3. Paste the URL of your playlist or video.
4. Let the application run. It will pause between videos to prevent rapid rate-limiting.
5. Check your `transcripts/` output destination to verify the results.
6. Review the Run-on Report at the end of the script to see if you need to manually break up any long paragraphs.

## Sample Prompts

The script uses interactive prompts for easy navigation. Here's what you can expect during a typical run:

```
Webshare username:
> my_username

Webshare password:
> my_password

Choose delay between videos (seconds):
  1) 15
  2) 30 (default)
  3) 60
  4) 90
  5) 120
Enter number (1–5) or press Enter for 30:
> 2

Enter playlist URL (or Enter to quit):
> [https://youtube.com/playlist?list=YOUR_PLAYLIST_ID](https://youtube.com/playlist?list=YOUR_PLAYLIST_ID)

Process another? (y/n):
> n
```

## Troubleshooting

- **Error: Max retries exceeded** : Your current proxy IP was likely blocked by YouTube. Ensure you are using "Rotating Residential" proxies in Webshare, not static ones.
- **Issue: No captions available** : The video might not have an English track available, or captions are disabled entirely. The script will save a placeholder file noting this.
- **Issue: File has very long paragraphs** : Auto-captions may contain typos, filler words ("um", "uh"), or lack punctuation. You can change `RUN_ON_THRESHOLD = 1200` in the script to adjust detection sensitivity.

## License

This project is licensed under the GNU General Public License v3.0 (GPL-3.0) . You are free to use, modify, and distribute this software, provided that you:

- Disclose the source code of any modifications you make.
- License your modified versions under the same GPL-3.0 license.
- Preserve the original copyright notices and disclaimers.

See the LICENSE file for the complete text of the GPL-3.0 license.