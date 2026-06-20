# Script Humanizer

Paste a clean, AI-written short-form script and get back a take that sounds like a real creator talking — slang, fillers, pacing, the works — without changing the info, steps, offer, or CTA.

## Structure

```
script-humanizer/
├── index.html        → frontend (the UI you see in the browser)
├── api/
│   └── humanize.js   → serverless function — calls Groq server-side, keeps your API key off the client
├── package.json
└── .gitignore
```

## Deploy on Vercel

1. Push this folder to a GitHub/GitLab/Bitbucket repo, **or** just run `vercel` from inside this folder with the Vercel CLI.
2. Import the repo at vercel.com/new (or finish the CLI prompts).
3. In the Vercel project: **Settings → Environment Variables** → add
   - `GROQ_API_KEY` = your key from console.groq.com/keys
4. Redeploy. (If the project is linked to git, adding the env var and pushing again will trigger this automatically.)

That's it — no build step, no framework config needed.

## Local testing

The API key lives in a serverless function, so double-clicking `index.html` won't work — there's no server behind it that way. Use the Vercel CLI instead:

```
npm i -g vercel
vercel dev
```

Run that from inside this folder, then open the local URL it prints.

## Customizing the tone

All the humanization rules (slang, fillers, pacing, density) live in the `SYSTEM_PROMPT` constant at the top of `api/humanize.js`. Edit that text directly to dial the voice up, down, or in a different direction — no other code needs to change.

## If a Groq model gets deprecated

Open the **Setup** panel in the UI and type a current model name (check console.groq.com/docs/models), or change the default value in `index.html`'s model `<input>`.
