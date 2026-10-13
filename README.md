# MenuMitra

**A private menu translation studio for independent restaurants.** MenuMitra translates menu copy with an open-weight model served by Ollama. It keeps dish names, prices, quantities, and existing allergen notes visible for a human review.

## Run it locally

Install [Ollama](https://ollama.com), then pull and start a model:

```powershell
ollama pull gemma3:4b
ollama serve
```

In another terminal, from this folder:

```powershell
python app.py
```

Open http://localhost:8000. Choose another installed Ollama model with `OLLAMA_MODEL=your-model python app.py` (PowerShell: `$env:OLLAMA_MODEL="your-model"; python app.py`).

No Python packages are required. The browser stores only the in-progress source draft in local storage; MenuMitra does not save submitted menus. Local Ollama inference keeps the text on your machine. Review all translations, especially allergen information, before publishing.

## Deploy on Render

Render hosts the MenuMitra web app; it does not run the language model for you. Set `OLLAMA_BASE_URL` to an Ollama server URL that Render can reach, and set `OLLAMA_MODEL` to a model already available there. For a private kitchen, run the app and Ollama locally instead of exposing a model server publicly.

Create a **Web Service** from this repository. Render reads `render.yaml`; set `OLLAMA_BASE_URL` in the service environment. After the service exists, trigger a deploy with the Render CLI:

```bash
render deploys create <your-render-service-id> --wait
```

## Stack

- Python standard library HTTP server
- Ollama `/api/chat` API
- Gemma 3 4B by default (swap for any model installed in Ollama)
- Plain HTML, CSS, and JavaScript; no database, tracking, or frontend build step

## Why open models?

Independent restaurants can run translations without a per-request API bill and keep menu drafts inside their own environment. The model is replaceable, and the prompt can be adapted for regional dishes or house terminology. Open weights make that kind of control practical; a hosted closed API would add a third-party data path and variable usage costs.

## Possible pricing

Offer a one-time setup for a restaurant's preferred model and house glossary, then charge a small monthly fee for updates and support. Validate this with an actual restaurant before treating it as proven demand.

## License

MIT. See [LICENSE](LICENSE).
