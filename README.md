# Cognitive Orthotic — Webhook Backend

## Setup (5 steps)

### 1. Install
```bash
pip install -r requirements.txt
```

### 2. Set environment variables
```bash
export GITLAB_TOKEN="your_gitlab_personal_access_token"   # scope: api
export ANTHROPIC_API_KEY="sk-ant-..."
export WEBHOOK_SECRET="pick_any_random_string"
export GITLAB_URL="https://gitlab.com"
```

### 3. Run locally (for testing)
```bash
python app.py
# → running on http://0.0.0.0:5000
```

### 4. Expose locally with ngrok (for GitLab to reach you)
```bash
ngrok http 5000
# → copy the https URL, e.g. https://abc123.ngrok.io
```

### 5. Add webhook in GitLab
- Settings → Webhooks → Add new
- URL: `https://abc123.ngrok.io/webhook`
- Secret token: same as WEBHOOK_SECRET
- Trigger: check **"Work item events"** (and optionally "Issue events")
- Save → Test → "Issue events"

## Deploy to Cloud Run (for submission)
```bash
gcloud run deploy cognitive-orthotic \
  --source . \
  --set-env-vars GITLAB_TOKEN=xxx,ANTHROPIC_API_KEY=xxx,WEBHOOK_SECRET=xxx \
  --allow-unauthenticated \
  --region us-central1
```
Replace the ngrok URL in GitLab webhook with the Cloud Run URL.
