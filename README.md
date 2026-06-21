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
2. Import the repo at vercel.com/new (or finish the CLI prompts). No environment variables or config needed — that's it.

## Using it

On first load, paste your Groq API key (from console.groq.com/keys) into the **Setup** panel. It's saved in your browser's local storage and sent to `api/humanize.js` on each request, which forwards it to Groq server-side — so it's never exposed directly to Groq from the browser, which avoids the CORS error you'd get calling Groq straight from client-side JS.

If you'd rather not type the key in every browser you use, you can still set a `GROQ_API_KEY` environment variable in Vercel as a fallback — the function uses whatever key you typed in the UI first, and only falls back to the env var if that field is empty.

## Local testing

```
vercel dev
```

Run that from inside this folder, then open the local URL it prints, and paste your API key into the Setup panel same as on the live site.

## Customizing the tone

All the humanization rules (slang, fillers, pacing, density) live in the `SYSTEM_PROMPT` constant at the top of `api/humanize.js`. Edit that text directly to dial the voice up, down, or in a different direction — no other code needs to change.

## If a Groq model gets deprecated

Open the **Setup** panel in the UI and type a current model name (check console.groq.com/docs/models), or change the default value in `index.html`'s model `<input>`.
