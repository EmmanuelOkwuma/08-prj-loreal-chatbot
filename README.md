# Project 8: L'Oréal Chatbot

L’Oréal is exploring the power of AI, and your job is to showcase what's possible. Your task is to build a chatbot that helps users discover and understand L’Oréal’s extensive range of products—makeup, skincare, haircare, and fragrances—as well as provide personalized routines and recommendations.

## 🚀 Launch via GitHub Codespaces

1. In the GitHub repo, click the **Code** button and select **Open with Codespaces → New codespace**.
2. Once your codespace is ready, open the `index.html` file via the live preview.

## ☁️ Cloudflare Note

When deploying through Cloudflare, make sure your API request body (in `script.js`) includes a `messages` array and handle the response by extracting `data.choices[0].message.content`.

Enjoy building your L’Oréal beauty assistant! 💄

## Work locally on a Mac

Open this folder in Visual Studio Code. In its terminal run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit http://localhost:8000. No Codespaces or JavaScript packages are needed.

## Connect your own Cloudflare Worker

1. Sign in to Cloudflare and create a Worker. This repository's helper uses classic Service Worker syntax, not module syntax. Use the dashboard's Service Worker format when replacing its code with `RESOURCE_cloudflare-worker.js`.
2. In Worker settings, add a **Secret** named `OPENAI_API_KEY`. Enter the value directly in Cloudflare, never in chat or a project file.
3. Add a text variable named `ALLOWED_ORIGIN` with value `http://localhost:8000` for local testing. Redeploy after changing settings.
4. Copy the public HTTPS Worker address into `WORKER_URL` at the top of `script.js`.
5. Reload the local site. Ask about a L’Oréal routine, then ask a follow-up. Ask an unrelated question to verify redirection.

The server supplies its own system prompt and ignores system instructions from the browser. Prompt-based topic filtering is best-effort and must be tested with live responses. Conversation history stays in memory and clears on reload or New chat. API requests send recent successful turns to OpenAI.

## Deploy the frontend with GitHub Pages

Create your own GitHub repository and push this project there; the classroom starter remote is not your personal repository. Enable Pages from the main branch, root folder. Only the HTML, CSS, script and image files are needed for the website; the Worker helper contains no credentials.

Change `ALLOWED_ORIGIN` in Cloudflare to your Pages origin, e.g. `https://your-name.github.io` (no repository path or trailing slash). Redeploy the Worker and verify the public site, follow-up questions, off-topic redirection, phone layout and failure message.

Origin checking restricts browser access but is not authentication: external clients can forge an Origin header. Before leaving a paid endpoint publicly available, configure Cloudflare rate limiting and an OpenAI project budget alert; use stronger access controls if needed.

## Voice input

Click the microphone beside Send and allow microphone access. Speak a question, then pause or click the microphone again to stop. The transcription appears in the input field; review and edit it before clicking Send. Dictation appends to an existing draft and never submits automatically. New chat cancels dictation and clears the draft.

This uses the browser's SpeechRecognition or webkitSpeechRecognition service, not a separate OpenAI audio endpoint. Support varies by browser, and the browser may use an online speech service. If unavailable or permission is denied, typing still works. Test on the HTTPS Pages site with a real microphone: allow permission, dictate, edit, send, deny permission, and cancel with New chat.

Voice input also requests up to five alternative transcriptions and supplies beauty-brand phrase hints when the browser supports them. Actual recognition accuracy and available alternatives depend on the browser's speech engine. After dictation, users can choose an alternative or select a misheard word in the draft and insert the correct spelling from a beauty-brand menu. No brand replacements or submissions happen automatically.
