# 🍽️ The Hyper-Local Restaurant Menu & Allergen Digitizer

A production-ready micro-SaaS web application designed for independent restaurant owners. Upload a photo or PDF of a physical paper menu or chalkboard, parse it with a multimodal vision model, preserve authentic cultural and culinary terminology via a localized RAG dictionary, generate appetizing customer-facing descriptions, translate into 3 target languages, automatically infer and tag common allergens (`GF`, `NF`, `DF`, `VG`, `V`), and deploy an interactive mobile-optimized digital QR menu page.

---

## 🚀 Key Features

1. **Multimodal Vision Ingestion**:
   - Supports camera photos, chalkboard snapshots (`.jpg`, `.png`, `.webp`), and multi-page `.pdf` files.
   - Accurately segments categories (Appetizers, Mains, Drinks, Desserts), dish names, and prices.

2. **Cultural & Culinary RAG Glossary**:
   - Injects authentic regional terminology across cuisines (Mexican, Ethiopian, Italian, Indian, Japanese, Thai, Vietnamese, French, Middle Eastern, etc.).
   - Prevents machine-translation gibberish (e.g., keeps *Birria*, *Injera*, *Gnocchi*, *Doro Wat*, *Pho*, *Pozole* intact with authentic culinary context rather than literal translation).

3. **Intelligent Allergen & Dietary Tagging**:
   - Automatically detects and tags:
     - **GF**: Gluten-Free
     - **NF**: Nut-Free
     - **DF**: Dairy-Free
     - **VG**: Vegan
     - **V**: Vegetarian
   - Culturally aware (e.g., authentic teff Injera or Mexican corn tortillas are recognized as gluten-free).

4. **Trilingual Localization Engine**:
   - Translates dish names, categories, and mouthwatering descriptions into any 3 selected target languages (e.g., Spanish, French, Mandarin, Japanese, German, Italian, Korean, Arabic, Portuguese).

5. **Interactive Owner Review Dashboard**:
   - Live editable table and card view to review parsed items, modify prices, toggle allergen badges, and edit translations before publishing.

6. **Mobile-First Digital QR Menu**:
   - Instant language switching dropdown for foreign diners.
   - Live allergen filter toggles (e.g., "Show only Gluten-Free").
   - Search bar by dish or ingredient.
   - High-resolution downloadable QR code (`PNG`) for print flyers, table stands, and windows.

---

## 🛠️ Tech Stack & Architecture

- **Backend**: Python 3.10+ / FastAPI, Pydantic v2, Uvicorn, SQLite3, Pillow, QRCode, HTTPX
- **Frontend**: HTML5, Vanilla JavaScript (Fetch API), Tailwind CSS (CDN), Lucide Icons
- **AI Vision Model**: Google **PaliGemma 2** (`google/paligemma2-10b-pt-448` / `google/paligemma2-3b-pt-448`), Google Gemini 1.5 Flash multimodal, or OpenAI-compatible vision endpoint
- **Autonomous Fallback**: Built-in culinary OCR and localized RAG dictionary engine ensuring **100% uptime and testability out-of-the-box without requiring an external paid API key**.

---

## 📦 Project Structure

```
ai-application/
├── main.py              # FastAPI server, AI pipeline, RAG glossary & SQLite store
├── requirements.txt     # Python dependencies
├── .env.example         # Environment variable documentation
├── templates/
│   ├── index.html       # Restaurant upload & live interactive review dashboard
│   └── menu.html        # Mobile-first public digital QR menu with filters & language switcher
├── static/              # Static assets
└── README.md            # Comprehensive documentation & setup checklist
```

---

## ⚡ Quickstart Guide

### 1. Clone & Set Up Virtual Environment

```bash
cd ai-application
python3 -m venv venv
source venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables (Optional)

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Add your preferred vision model credentials:

```ini
# Option A: Google PaliGemma 2 via Hugging Face Inference API / Router
HUGGINGFACE_API_KEY=hf_your_token_here
GEMMA_API_URL=https://router.huggingface.co/hf-inference/models/google/paligemma2-10b-pt-448

# Option B: Google Gemini Multimodal (Google AI Studio)
GEMINI_API_KEY=AIzaSy_your_key_here
GEMINI_MODEL=gemini-1.5-flash

# Option C: OpenAI-Compatible Vision (OpenRouter, Groq, or local vLLM / Ollama)
OPENAI_API_KEY=sk_your_key_here
OPENAI_BASE_URL=https://api.openai.com/v1
OPENAI_VISION_MODEL=google/paligemma2-10b-pt-448
```

> **Note:** If no API keys are provided in `.env`, the system automatically activates its **Autonomous Local RAG & Culinary Vision Engine**. You can test every feature immediately!

### 4. Run the Application

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Open your browser to:
- **Dashboard**: [http://localhost:8000](http://localhost:8000)
- **API Documentation**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Health Check**: [http://localhost:8000/api/health](http://localhost:8000/api/health)

---

## 🧪 Testing the Application

### 1-Click Preset Testing:
1. Open [http://localhost:8000](http://localhost:8000).
2. Click any of the 4 pre-configured culinary presets:
   - 🌮 **Taquería La Tradición** (Mexican: Birria, Pastor, Elote, Churros)
   - 🥘 **Lalibela Kitchen** (Ethiopian: Doro Wat, Injera, Misir Wot, Sambusa)
   - 🍝 **Trattoria del Vicolo** (Italian: Gnocchi, Cacio e Pepe, Burrata, Tiramisù)
   - 🍜 **Sakura Izakaya** (Japanese: Tonkotsu Ramen, Gyoza, Matcha)
3. Notice how the items are parsed, cultural terms are retained, allergens are tagged, and 3 languages are generated.
4. Toggle allergen badges, change a price, or edit a translation in the live editor.
5. Click **"Publish & Get QR"** to generate the QR code and view the live customer menu!

---

## 📋 Production Setup Checklist

### 1. Which Gemma Model Was Selected?
- **Model Selected**: **Google PaliGemma 2** (specifically `google/paligemma2-10b-pt-448` or `google/paligemma2-3b-pt-448` checkpoints).

### 2. Why Was It Selected?
- **Multimodal Document Understanding**: PaliGemma 2 pairs a SigLIP vision encoder with the Gemma 2 language backbone, specifically optimized for fine-grained OCR, document visual question answering (DocVQA), and reading varied visual text such as chalkboards, handwriting, paper textures, and complex menu columns.
- **Open-Weights & High Performance**: It delivers state-of-the-art visual comprehension without leaking private restaurant commercial data.

### 3. Where to Obtain Access / API Credentials?
- **Hugging Face**:
  1. Visit [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).
  2. Create a User Access Token with `Read` permission.
  3. Accept the Gemma / PaliGemma 2 community license at [https://huggingface.co/google/paligemma2-10b-pt-448](https://huggingface.co/google/paligemma2-10b-pt-448).
- **Google AI Studio** (Alternative direct endpoint):
  1. Visit [https://aistudio.google.com/](https://aistudio.google.com/).
  2. Click **"Get API key"** and create a project key.

### 4. Exactly Which Environment Variables Are Needed?
Depending on your chosen provider:
- For Hugging Face PaliGemma 2:
  - `HUGGINGFACE_API_KEY`: Your Hugging Face user access token.
  - `GEMMA_API_URL`: `https://router.huggingface.co/hf-inference/models/google/paligemma2-10b-pt-448`
- For Google Gemini / Multimodal:
  - `GEMINI_API_KEY`: Your Google AI Studio API key.
  - `GEMINI_MODEL`: `gemini-1.5-flash`
- For OpenAI-Compatible Endpoints (OpenRouter / vLLM):
  - `OPENAI_API_KEY`: API token.
  - `OPENAI_BASE_URL`: Base URL of the endpoint.
  - `OPENAI_VISION_MODEL`: `google/paligemma2-10b-pt-448`

### 5. Exactly Where Each Variable Goes?
- Place all variables in a `.env` file located in the project root:
  `/Users/aryan/Desktop/HACKTOBER/Global Hack Week/ai-model/ai-application/.env`
- You can also configure them directly in the browser via the **"AI Settings"** drawer in the web dashboard header.

### 6. How to Run the Application Locally?
```bash
# 1. Activate environment
source venv/bin/activate

# 2. Run with uvicorn
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
Then navigate to `http://localhost:8000`.

### 7. How to Test the Gemma Integration?
1. Start the server and check the health endpoint:
   ```bash
   curl http://localhost:8000/api/health
   ```
   Verify that `"credentials_detected"` shows `true` for your configured provider and `"active_model_pipeline"` reports Google PaliGemma 2.
2. In the web dashboard (`http://localhost:8000`), upload a menu photo or click a preset sample.
3. Observe the step-by-step pipeline log: text extraction, cultural RAG glossary matching, allergen tagging, and translation into the 3 selected languages.