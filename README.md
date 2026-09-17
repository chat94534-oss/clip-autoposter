# Clip reposter with generated commentary

Pulls top public clips, writes original commentary copy, speaks it with edge-tts over the clip with the source audio ducked, reframes to vertical with a facecam split when one is detected, then uploads on a schedule. Runs entirely on GitHub Actions.

## How it runs
One generation run per day builds every slot at once and hands each video to the
platform's own scheduler, so a missed cron costs nothing — later runs measure the
gap from what actually posted and fill only what is missing.

## Configuration
Credentials are supplied as repository secrets and are never committed. Copy the
OAuth client into place and run `youtube_authorize.py` once to mint a token.

## Local use
    python make_clip.py --no-upload     # build only, keeps its output for inspection
    python make_clip.py --fill-day      # build and schedule the day

Logs are redacted in CI (`REDACT_LOGS=1`) because Actions logs are public.
