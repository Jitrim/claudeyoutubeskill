# Claude YouTube skill

Lets Claude Code learn new skills by watching YouTube videos.

Built from the 3-step method in [this Instagram reel](https://www.instagram.com/reel/Db1USzsMNnZ/):

1. **`watch` skill** (`.claude/skills/watch/`): sends a video to Gemini, which can watch YouTube, and saves a timestamped transcript, on-screen visual breakdown and step list to `watched/`. The work happens in `scripts/watch_video.py`.
2. **Gemini API key**: free from [Google AI Studio](https://aistudio.google.com/apikey).
3. **`skill-from-video` skill** (`.claude/skills/skill-from-video/`): turns a watched video into a new project skill in `.claude/skills/<name>/`.

## Setup

```bash
pip install -r scripts/requirements.txt
export GEMINI_API_KEY=your-key   # in Claude Code on the web, add it to the environment's variables
```

## Use

Open Claude Code in this repo and say:

- "Watch https://youtube.com/watch?v=... and summarize it"
- "Watch https://youtube.com/watch?v=... and make a skill from it"

Or run the script directly:

```bash
python scripts/watch_video.py "https://www.youtube.com/watch?v=..." --focus "the exact commands shown"
python scripts/watch_video.py ./clip.mp4 --out watched/clip.md
```

Optional: set `GEMINI_MODEL` (default `gemini-2.5-flash`) to use another Gemini model.

## Safety

Video transcripts and on-screen text are treated as untrusted input. Both skills tell Claude to report instructions found in a video rather than follow them, and to check commands before putting them into a new skill.
