# AI FitTrack Corrected Project

This folder contains a corrected, runnable backend based on the API structure documented in the supplied project.

Important:
- `.env` contains placeholders only. Put your real MongoDB Atlas URI and Gemini API key there.
- The server defaults to port 5001 to match your currently working setup.
- AI routes require a JWT Bearer token.
- The AI endpoint is POST `/api/ai/workout-recommendation`.
- The Gemini model is configurable through `GEMINI_MODEL`.

Run:
```powershell
npm install
npm run dev
```

Then follow SETUP.md.
