# Resume chatbot (Python: LangChain + Gradio + OpenRouter)

Visitors chat with an assistant that answers **only** from `resume.json`.

## Run locally
1. Install Python 3.10+
2. In this folder:
   ```
   python -m venv .venv
   source .venv/bin/activate      # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   cp .env.example .env           # Windows: copy .env.example .env
   ```
3. Put your OpenRouter key in `.env` (get one at https://openrouter.ai/keys)
4. Edit `resume.json` with your real details
5. `python app.py` → open http://localhost:7860

## Deploy free on Hugging Face Spaces (easiest)
1. Create an account at huggingface.co → New Space → SDK: **Gradio**
2. Upload `app.py`, `requirements.txt`, `resume.json` (do NOT upload `.env`)
3. Space → Settings → **Variables and secrets** → add secret `OPENROUTER_API_KEY`
   (optionally `OPENROUTER_MODEL`)
4. It builds and gives you a public URL like `https://huggingface.co/spaces/you/resume-bot`

(Render, Railway or any host that runs `python app.py` also works; set the same env vars.)

## Putting it on LinkedIn
LinkedIn doesn't allow embedded apps or iframes in profiles, so share the link:
- **Featured** section → Add → Link → paste your Space URL
- Contact info → Website, and mention it in **About**
- A launch post

## Notes
- Set a spending limit on your OpenRouter account (Settings → Credits/Limits).
- Per-visitor limits are in `.env` (`MAX_PER_MINUTE`, `MAX_PER_DAY`).
- Edit `resume.json` anytime and restart/redeploy to update answers.
- Chats are not stored.

## Deploy on Render
1. Push this folder to a GitHub repo (`.env` is git-ignored, so your key stays private).
2. Render dashboard → New → **Blueprint** → select the repo (it reads `render.yaml`).
3. Paste your `OPENROUTER_API_KEY` when prompted → Apply.
4. After the build you get a URL like `https://resume-chatbot.onrender.com`.
Free instances sleep when idle, so the first visit can take ~30-60 seconds.
