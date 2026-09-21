--- a/README.md
+++ b/README.md
@@ -1 +1,71 @@
-# Repository
+# FastAPI Qwen Backend
+
+A minimal, production-conscious FastAPI backend designed to interact with the Qwen LLM via its OpenAI-compatible API. Provider logic is isolated to allow easy swapping for OpenAI, Anthropic, etc., in the future.
+
+## Setup
+
+1. **Clone the repository**
+   ```bash
+   git clone <repository-url>
+   cd <repository-name>
+   ```
+
+2. **Create and activate a virtual environment**
+   ```bash
+   python -m venv .venv
+   source .venv/bin/activate  # On Windows use: .venv\Scripts\activate
+   ```
+
+3. **Install dependencies**
+   ```bash
+   pip install -e ".[dev]"
+   ```
+
+## Configuration (.env)
+
+1. Copy the example environment file:
+   ```bash
+   cp .env.example .env
+   ```
+2. Edit `.env` and add your Qwen credentials:
+   ```env
+   QWEN_API_KEY=sk-your-actual-api-key
+   QWEN_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
+   QWEN_MODEL=qwen-plus
+   ```
+   *Note: Never commit your `.env` file. It is excluded via `.gitignore`.*
+
+## Run Commands
+
+**Start the development server:**
+```bash
+uvicorn app.main:app --reload
+```
+
+**Run tests:**
+```bash
+pytest
+```
+
+## API Endpoints & Curl Examples
+
+### Health Check
+```bash
+curl http://127.0.0.1:8000/health
+```
+*Response:* `{"status":"ok"}`
+
+### Chat Completion
+```bash
+curl -X POST http://127.0.0.1:8000/chat \
+     -H "Content-Type: application/json" \
+     -d '{
+           "message": "Write a haiku about programming.",
+           "system_prompt": "You are a helpful AI assistant."
+         }'
+```
+*Response:* `{"reply":"...","model":"qwen-plus"}`
+
+### Validation Error Example
+```bash
+curl -X POST http://127.0.0.1:8000/chat \
+     -H "Content-Type: application/json" \
+     -d '{"message": ""}'
+```
+*Response:* `422 Unprocessable Entity`
