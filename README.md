# learn

Personal AI learning setup for [pi](https://github.com/earendil-works/pi), based on
[amosblomqvist/learn](https://github.com/amosblomqvist/learn), customised for Cambridge
Engineering Tripos Part IA plus personal learning.

## Layout

- `.pi/` — project pi config: `teach` and `visualize` skills, quiz / ask-user-question /
  md-log / visual-tools extensions, researcher and diagram-maker agents.
- `Tripos IA/<paper>/Specifications/` — CUED syllabus PDFs (the exam spec) per paper.
- `Tripos IA/<paper>/Lecture notes/` — lecture notes per paper.
- `viz/` — diagrams generated during lessons.
- `pi-global/` — backup of pieces installed globally in `~/.pi/agent/` (not loaded from here).

## Restore on a new machine

```bash
brew install tmux
npm install -g @earendil-works/pi-coding-agent
git clone https://github.com/tr129x/learn ~/Desktop/Obsidian/vault/π/learn
cd ~/Desktop/Obsidian/vault/π/learn
(cd .pi/extensions/visual-tools && npm install)
pi install https://github.com/amosblomqvist/pi-interactive-subagents
mkdir -p ~/.pi/agent/skills ~/.pi/agent/extensions
cp -R pi-global/skills/pdf-reader ~/.pi/agent/skills/
cp -R pi-global/extensions/web-search pi-global/extensions/web-fetch ~/.pi/agent/extensions/
(cd ~/.pi/agent/extensions/web-fetch && npm install)
python3 -m venv ~/.pi/agent/skills/pdf-reader/.venv
~/.pi/agent/skills/pdf-reader/.venv/bin/pip install -r ~/.pi/agent/skills/pdf-reader/requirements.txt
cp pi-global/tmux.conf ~/.tmux.conf
```

Then add a Tavily key to `~/.pi/agent/extensions/web-search/auth.json` (see
`auth.example.json`), sign in with `pi auth`, and start with:

```bash
tmux new -A -s learn -c ~/Desktop/Obsidian/vault/π/learn pi
```

`.pi/extensions/visual-tools/package.json` points its dev dependency at the global pi
install under `/opt/homebrew`; adjust if pi lives elsewhere.
