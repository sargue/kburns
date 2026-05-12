# AGENTS.md

## Project Shape

This repository is a Ruby/FFmpeg slideshow generator. The active entry point is
`./kburns.rb`; the old upstream `kburns.rb` script was replaced by the extended
implementation that used to live in `kburns2.rb`.

`kburns.rb`:
- accepts still images, video clips, audio files, and audio playlists
- renders still images into temporary Ken Burns videos
- preserves audio from video clips
- builds background audio for still-image sections
- supports subtitle descriptor files and generated title slides
- writes and reuses `temp-kburns*` intermediate files unless
  `--delete-temp-files` is provided

## Runtime Dependencies

- Ruby
- `ffmpeg` and `ffprobe`
- Ruby gems: `fastimage` and `thread/pool`
- `Inter-ExtraBold.otf` in the repository root for title slide rendering

There is no Gemfile yet, so dependency setup is currently manual.

## Files To Know

- `kburns.rb`: main script and current source of truth
- `README.md`: user-facing overview and examples
- `Makefile`: smoke/test invocations for image slideshow rendering
- `tests/`: sample images and expected/debug assets from earlier testing

## Development Notes

- Preserve the executable bit on `kburns.rb`; the Makefile invokes it directly.
- Keep changes scoped. This is a small script repo with no formal test harness.
- Prefer syntax checks such as `ruby -c kburns.rb` before running expensive
  FFmpeg jobs.
- Full Makefile tests can generate many media files and require local FFmpeg,
  Ruby gems, and working sample inputs.
- The current Makefile includes an older `tests/10x15.jpg` reference; that
  fixture is not present in the repository as of this note.
- Generated media and temporary files should stay out of commits unless the user
  asks for fixture updates.
