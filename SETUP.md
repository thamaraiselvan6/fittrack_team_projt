# AI FitTrack - Corrected Setup

## 1. Install

```powershell
npm install
```

## 2. Configure `.env`

Replace the placeholders in `.env`:

```env
PORT=5001
MONGO_URI=mongodb+srv://USERNAME:PASSWORD@YOUR_CLUSTER.mongodb.net/fittrack?retryWrites=true&w=majority
JWT_SECRET=replace_with_a_long_random_secret
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
GEMINI_MODEL=gemini-3.8-flash
```

Do not share `.env` publicly.

## 3. MongoDB Atlas

Make sure:
- Your Atlas database user exists.
- The password is correct.
- Your current IP is allowed in Network Access.
- The cluster is running.

For temporary local development only, Atlas can be configured with `0.0.0.0/0`; restrict this afterward.

## 4. Start

```powershell
npm run dev
```

Expected:

```text
Gemini API key loaded: true
MongoDB Connected: ...
Server running in development mode on port 5001
```

## 5. Test authentication

### Register

POST

`http://localhost:5001/api/auth/register`

```json
{
  "name": "Thamarai Selvan",
  "email": "thamarai@example.com",
  "password": "123456"
}
```

Copy the returned `token`.

### Login

POST

`http://localhost:5001/api/auth/login`

```json
{
  "email": "thamarai@example.com",
  "password": "123456"
}
```

## 6. Test AI

POST

`http://localhost:5001/api/ai/workout-recommendation`

Authorization:

```text
Bearer YOUR_JWT_TOKEN
```

Body:

```json
{
  "age": 22,
  "fitnessGoal": "Weight Loss",
  "experience": "Beginner"
}
```

## 7. Common errors

### EADDRINUSE

Find and stop the process using port 5001:

```powershell
netstat -ano | findstr :5001
taskkill /PID YOUR_PID /F
```

### Not authorized, no token provided

Add:

```text
Authorization: Bearer YOUR_JWT_TOKEN
```

### Endpoint Not Found

Use lowercase:

```text
/api/ai/workout-recommendation
```

and use POST, not GET.

### Gemini model error

Change `GEMINI_MODEL` to a model available to your Gemini API key. The current value is based on the model name reported by the error you encountered.
