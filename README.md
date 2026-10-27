\# BharatVoice 🇮🇳



_>&#x20;_**\*\*भारतवॉइस\*\***_&#x20;(Hindi: "conversation") - Self-hosted voice AI platform for local Indian businesses_



[![Python 3.12+]\(https\://img.shields.io/badge/python-3.12+-blue.svg)]\(https\://www\.python.org/downloads/)

[![FastAPI]\(https\://img.shields.io/badge/FastAPI-0.115+-green.svg)]\(https\://fastapi.tiangolo.com/)

[![License: MIT]\(https\://img.shields.io/badge/License-MIT-yellow\.svg)]\(https\://opensource.org/licenses/MIT)

[![Release]\(https\://img.shields.io/badge/release-v0.3-brightgreen.svg)]\(https\://github.com/AmalBajpayee09/BharatVoice/releases)



A production-ready voice bot that handles phone calls autonomously with native **\*\*Hindi-English-Hinglish\*\*** support. Built for restaurants, clinics, and local businesses that need affordable, high-quality voice AI.



\## ✨ Features



\- **\*\*🎙️ Real-time Voice Pipeline\*\***: Deepgram STT → Groq LLM → Piper TTS (< 500ms P50)

\- **\*\*🇮🇳 Native Hindi Support\*\***: Seamless code-switching between Hindi, English, and Hinglish

\- **\*\*📞 Telephony Ready\*\***: Plivo integration for inbound calls (WebSocket audio streaming)

\- **\*\*🍽️ Restaurant Demo\*\***: Table reservations, menu queries, hours - fully functional

\- **\*\*🧠 Knowledge Base (RAG)\*\***: ChromaDB-powered retrieval for menu items, FAQs, policies

\- **\*\*🏢 Multi-Business\*\***: Support multiple businesses with phone-based routing

\- **\*\*🤖 AI-Powered QA\*\***: CrewAI agents analyze transcripts for quality issues and improvements

\- **\*\*🎯 Low Latency\*\***: P50 < 500ms processing, per-step timeouts, optimized for real conversations

\- **\*\*🔒 Privacy First\*\***: Phone encryption (AES-256-GCM), PII masking, safe routing

\- **\*\*💰 Cost Effective\*\***: \~$16-27/month operational cost



\## 🆕 What's New in v0.3



\- **\*\*CrewAI Transcript Analysis\*\***: Multi-agent QA system reviews call transcripts automatically

  - QA Reviewer agent identifies issues and rates call quality (1-5)

  - Issue Classifier categorizes problems (knowledge gap, STT error, UX issue, etc.)

  - Improvement Suggester generates actionable fixes with priorities

\- **\*\*React Admin Frontend\*\***: Modern TypeScript frontend with Orval-generated API client

\- **\*\*Transcript Reviews API\*\***: View quality scores, issues, and suggestions per call

\- **\*\*Latency Metrics\*\***: Accurate percentile calculations with linear interpolation

\- **\*\*Concurrency Safety\*\***: Unique constraints prevent duplicate reviews under load

\- **\*\*ChromaDB Reliability\*\***: Proper commit ordering prevents orphaned embeddings



\## 📋 Previous Releases



\<details>

\<summary>v0.2 - Multi-Business & Knowledge Base\</summary>



\- **\*\*Multi-Business Support\*\***: Route calls to different businesses based on phone number

\- **\*\*Knowledge Base System\*\***: RAG-powered retrieval with ChromaDB for dynamic menu/FAQ responses

\- **\*\*Admin UI Editors\*\***: Menu editor, FAQ editor, and knowledge test pages

\- **\*\*Security Hardening\*\***: Safe phone routing fallback, capacity limits, per-step timeouts

\- **\*\*Data Integrity\*\***: Transactional consistency between DB and vector store

\- **\*\*Prometheus Metrics\*\***: RAG latency and hit rate observability

\</details>



\## 🏗️ Architecture



\`\`\`

┌─────────────┐     ┌──────────────┐     ┌─────────────┐

│   Browser   │────▶│   FastAPI    │────▶│  Deepgram   │

│  (WebRTC)   │◀────│  WebSocket   │◀────│    STT      │

└─────────────┘     └──────┬───────┘     └─────────────┘

                          │

                          ▼

┌─────────────┐     ┌──────────────┐     ┌─────────────┐

│  ChromaDB   │────▶│   Groq LLM   │◀────│   SQLite    │

│    (RAG)    │     │ (llama-3.3)  │     │  (Business) │

└─────────────┘     └──────┬───────┘     └─────────────┘

                          │

                          ▼

┌─────────────┐     ┌──────────────┐     ┌─────────────┐

│   Plivo     │◀───▶│  Piper TTS   │     │   CrewAI    │

│ (Telephony) │     │   (Hindi)    │     │  (QA Agents)│

└─────────────┘     └──────────────┘     └─────────────┘

\`\`\`



\## 🚀 Quick Start



\### Prerequisites



\- Python 3.12+

\- [uv]\(https\://github.com/astral-sh/uv) (recommended) or pip

\- API keys: [Deepgram]\(https\://deepgram.com), [Groq]\(https\://groq.com)



\### 1. Clone & Install



\`\`\`bash

git clone https\://github.com/AmalBajpayee09/BharatVoice.git

cd BharatVoice



*# Install dependencies*

uv sync --all-extras

\`\`\`



\### 2. Configure Environment



\`\`\`bash

*# Copy example env file*

cp .env.example .env



*# Edit with your API keys*

nano .env

\`\`\`



**\*\*Required API Keys:\*\***

\| Service | Purpose | Get Key |

\|---------|---------|---------|

\| \`GROQ_API_KEY\` | LLM (conversation) | [console.groq.com]\(https\://console.groq.com) |

\| \`DEEPGRAM_API_KEY\` | Speech-to-text | [deepgram.com]\(https\://deepgram.com) |



**\*\*Optional (for telephony):\*\***

\| Service | Purpose | Get Key |

\|---------|---------|---------|

\| \`PLIVO_AUTH_ID\` | Phone calls | [plivo.com]\(https\://plivo.com) |

\| \`PLIVO_AUTH_TOKEN\` | Phone calls | [plivo.com]\(https\://plivo.com) |



\### 3. Generate Security Keys



\`\`\`bash

*# Generate encryption keys*

python scripts/generate_keys.py

\`\`\`



\### 4. Run the Server



\`\`\`bash

*# Start API server*

uv run uvicorn src.main:app --host 0.0.0.0 --port 8000



*# Or with hot reload (development)*

uv run uvicorn src.main:app --reload

\`\`\`



\### 5. Test Voice Bot



Open in browser: **\*\*http\://localhost:8000/voice\*\***



1\. Click **\*\*"Start Call"\*\***

2\. Speak naturally in Hindi/English

3\. Bot responds automatically

4\. Click **\*\*"End Call"\*\*** when done



\## 📁 Project Structure



\`\`\`

bharatvoice/

├── src/

│   ├── api/                 # FastAPI routes & WebSocket handlers

│   │   ├── routes/          # REST endpoints (Plivo webhooks, CRUD, reviews)

│   │   ├── websocket/       # Audio streaming with capacity limits

│   │   └── static/          # Voice test UI

│   ├── core/                # Business logic

│   │   ├── pipeline.py      # Voice pipeline with per-step timeouts

│   │   ├── session.py       # Call session management

│   │   └── context.py       # Business context builder

│   ├── services/            # External service integrations

│   │   ├── stt/             # Speech-to-text (Deepgram)

│   │   ├── llm/             # Language model (Groq) with RAG injection

│   │   ├── tts/             # Text-to-speech (Piper)

│   │   ├── telephony/       # Phone (Plivo)

│   │   ├── knowledge/       # RAG retrieval (ChromaDB + embeddings)

│   │   └── analysis/        # CrewAI transcript QA agents

│   ├── db/                  # Database models & repositories

│   └── observability/       # Prometheus metrics

├── web/                     # React admin frontend (TypeScript + Vite)

│   └── src/api/             # Orval-generated API client

├── admin/                   # Streamlit admin dashboard

│   └── pages/               # Menu editor, FAQ editor, knowledge test

├── config/                  # Business configuration (YAML)

├── migrations/              # Alembic database migrations

├── schemas/                 # JSON Schema (source of truth)

├── tests/                   # Test suite

└── scripts/                 # Utility scripts

\`\`\`



\## 🎯 Demo: Himalayan Kitchen



The default configuration is a demo restaurant bot for "Himalayan Kitchen":



**\*\*Try saying:\*\***

\- "Table book karna hai" (I want to book a table)

\- "4 log, kal shaam 7 baje" (4 people, tomorrow 7 PM)

\- "Menu mein kya hai?" (What's on the menu?)

\- "Timing kya hai?" (What are the hours?)



\## 🔧 Configuration



\### Environment Variables



See [.env.example]\(.env.example) for all options.



**\*\*Key Settings:\*\***

\`\`\`bash

*# LLM*

GROQ_API_KEY=gsk_xxxx              *# Required*



*# Speech-to-Text*

DEEPGRAM_API_KEY=xxxx              *# Required*



*# TTS (optional - defaults to gTTS)*

PIPER_VOICE=hi_IN-priyamvada-medium

EDGE_TTS_ENABLED=false



*# Conversation*

GREETING_TEXT=Namaste! ...

BARGE_IN_ENABLED=true              *# Interrupt bot while speaking*

\`\`\`



\### Business Configuration



Edit \`config/business/himalayan_kitchen.yaml\`:



\`\`\`yaml

name: "Himalayan Kitchen"

hours:

  monday: closed

  tuesday: "11:00-22:30"

  *# ...*

reservation:

  max_party_size: 10

  advance_days: 30

\`\`\`



\## 🧪 Testing



\`\`\`bash

*# Run all tests*

uv run pytest



*# Run with coverage*

uv run pytest --cov=src



*# Test specific module*

uv run pytest tests/test_core/

\`\`\`



\### Manual Testing Scripts



\`\`\`bash

*# Test TTS voice quality*

uv run python scripts/test_tts.py



*# Test LLM responses*

uv run python scripts/test_llm.py



*# Text-based conversation test*

uv run python scripts/chat_cli.py

\`\`\`



\## 🛠️ Development



\### Code Quality



\`\`\`bash

*# Lint*

uv run ruff check .



*# Format*

uv run ruff format .



*# Type check*

uv run mypy src/

\`\`\`



\### Database Migrations



\`\`\`bash

*# Create migration*

uv run alembic revision --autogenerate -m "description"



*# Apply migrations*

uv run alembic upgrade head

\`\`\`



\## 📊 Admin Dashboard



\`\`\`bash

*# Start admin UI*

uv run streamlit run admin/app.py

\`\`\`



Access at: **\*\*http\://localhost:8501\*\***



Features:

\- Call logs & transcripts (with PII masking)

\- Reservation management

\- Analytics dashboard

\- **\*\*Menu Editor\*\*** - Add/edit menu items with Hindi translations

\- **\*\*FAQ Editor\*\*** - Manage FAQs, policies, and announcements

\- **\*\*Knowledge Test\*\*** - Test RAG retrieval before going live

\- Configuration editor



\## 🚢 Deployment



\### Docker



\`\`\`bash

docker-compose up -d

\`\`\`



\### Manual



1\. Set \`ENVIRONMENT=production\` in \`.env\`

2\. Use a process manager (systemd, supervisor)

3\. Put behind reverse proxy (Caddy, nginx)

4\. Configure SSL certificates



\## 📈 Performance Targets



\| Metric | Target | Actual |

\|--------|--------|--------|

\| STT Latency (P50) | < 300ms | \~250ms |

\| LLM Latency (P50) | < 500ms | \~350ms |

\| TTS Latency (P50) | < 200ms | \~150ms |

\| End-to-end (P95) | < 1.2s | \~1.0s |



\## 🤝 Contributing



Contributions welcome! Please:



1\. Fork the repository

2\. Create a feature branch (\`git checkout -b feature/amazing\`)

3\. Commit changes (\`git commit -m 'Add amazing feature'\`)

4\. Push to branch (\`git push origin feature/amazing\`)

5\. Open a Pull Request



\## 📄 License



MIT License - see [LICENSE]\(LICENSE) for details.



\## 🙏 Acknowledgments



\- [Deepgram]\(https\://deepgram.com) - Speech-to-text

\- [Groq]\(https\://groq.com) - Fast LLM inference

\- [Piper]\(https\://github.com/rhasspy/piper) - Offline Hindi TTS

\- [ChromaDB]\(https\://trychroma.com) - Vector database for RAG

\- [CrewAI]\(https\://crewai.com) - Multi-agent orchestration for QA

\- [FastAPI]\(https\://fastapi.tiangolo.com) - Web framework

\- [Streamlit]\(https\://streamlit.io) - Admin dashboard



\---



**\*\*Built with ❤️ by Amal Bajpayee for local Indian businesses\*\***



*\*Built by [Amal Bajpayee](https://github.com/AmalBajpayee09). Questions or suggestions? Open an issue!\**
