# transcriptForged Changelog

All notable changes to this project will be documented in this file. The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [Unreleased]

## [v1.0.1] - 2026-06-07

### Updated

- Proper filename for --single mode.


## [v1.0.0] - 2026-05-22

### Added

- Initial Release: Core functionality to download and format transcripts from YouTube.
- Support for extracting videos from entire playlists or handling single-video links.
- Integration with Webshare proxy to bypass YouTube residential IP blocks.
- Smart Markdown generation that groups transcript lines into readable paragraphs based on punctuation and length limits.
- Run-on text detection & report at the end of execution to flag unbroken monologue blocks.
- Robust transient error handling and automatic retry mechanics for `youtube-transcript-api`.
- Safe credential handling via `transcriptForged.conf` to prevent hard-coding secrets.
- Configurable delays between requests to balance speed and stealth.