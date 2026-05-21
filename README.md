# 🛡️ SENTRY-NLP Intents

> **Production-Grade Intent Datasets for SENTRY-NLP & AskElgen**

A centralized, JSON-based training dataset for multi-domain intent classification. Powers the SENTRY-NLP chatbot, supporting academic research, portfolio integration, and professional applications.

---

## 📋 Features

- **12+ Intent Categories**: Covering portfolio, academics, fitness, technical expertise, and career availability
- **Production-Ready**: Structured JSON with metadata and semantic descriptions
- **Portfolio-Integrated**: Designed for seamless integration with the [AskElgen](https://elgendev.vercel.app) production chatbot
- **Extensible**: Easy to add new intents or modify existing ones
- **Versioned**: Semantic versioning for stable API contracts

---

## 📂 Repository Structure

```
sentry-nlp-intents/
├── README.md                    # This file
├── USAGE.md                     # Integration guide
├── LICENSE                      # MIT License
├── intents.json                 # Intent categories & samples
└── responses.json               # Response mappings
```

---

## 🚀 Quick Start

### Option 1: Fetch from GitHub (Recommended for Production)
```python
import requests
import json

url = "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json"
intents = requests.get(url).json()
print(intents["metadata"]["description"])
```

### Option 2: Local Usage (For Development)
```python
import json

with open("intents.json", "r") as f:
    intents = json.load(f)

# Access a specific intent
greeting_samples = intents["intents"]["greeting"]["samples"]
print(greeting_samples)
```

---

## 📊 Dataset Overview

| Intent | Samples | Category | Use Case |
| :--- | :---: | :--- | :--- |
| `greeting` | 10 | Conversational | Chat initialization |
| `portfolio` | 13 | Professional | Project & work inquiries |
| `achievements` | 9 | Academic | Awards & certifications |
| `fitness` | 12 | Personal | Health & running stats |
| `stack_technical` | 13 | Technical | Tech stack questions |
| `freelance_work` | 9 | Career | Freelance experience |
| `thesis_ai` | 12 | Academic | AI/ML research |
| `leadership_gdg` | 9 | Leadership | GDG & community roles |
| `philosophy_execution` | 10 | Personal | Work philosophy |
| `availability` | 9 | Career | Hiring & opportunities |
| `weather` | 7 | Utility | General weather |
| `goodbye` | 9 | Conversational | Session termination |

**Total Training Samples**: 122 | **Intent Coverage**: 12 domains

---

## 🔄 Integration Points

### NLP Class Assignment
- **Notebook**: [Chatbot_Individual_Project.ipynb](https://github.com/Elgen69/NLP-Final-Deliverable/tree/main/Individual-Assignment-Chatbot)
- **Fetches**: Remote JSON for training and evaluation

### Portfolio Website
- **Component**: [AskElgen.tsx](https://github.com/Elgen69/portfolio/blob/main/src/components/chat/AskElgen.tsx)
- **Status**: Integration pending (Post-assignment)
- **Connection**: Will fetch intents.json via GitHub raw URL

### Academic Research
- **Course**: CS5101 (Natural Language Processing)
- **Project**: SENTRY-Individual (Intent Classification Chatbot)
- **Submission**: May 22, 2026

---

## 💡 Intent Schema

Each intent contains:
- **`samples`** (array): Training examples for the intent
- **`description`** (string): Semantic meaning of the intent

Example:
```json
{
  "portfolio": {
    "samples": [
      "tell me about your apps",
      "what have you built",
      "show me your projects"
    ],
    "description": "Queries about portfolio projects and GitHub work"
  }
}
```

---

## 🔐 Safety & Filtering

- **Level 1 Safety Filter**: Implemented in notebook for academic compliance
- **Zero-Filtered API**: Production version (Gemini) operates without restrictions
- **Fallback Mechanism**: If GitHub fetch fails, notebook reverts to local hard-coded intents

---

## 📝 Contributing

To add new intents or modify existing ones:

1. Edit `intents.json` to add new intent categories
2. Update `responses.json` with corresponding responses
3. Increment version in metadata
4. Commit and push to `main`

Example (adding a new intent):
```json
{
  "newintent": {
    "samples": ["sample1", "sample2", "sample3"],
    "description": "Description of the new intent"
  }
}
```

---

## 📜 License

MIT License — See LICENSE file for details

---

## 👤 Author

**Elgen Mar Arinasa**  
- 🎓 4th Year BS Computer Science @ University of San Carlos
- 💼 Data Science Officer @ GDG on Campus - USC
- 🚀 Founder of Axio Labs
- 📧 elgen.arinasa.business@gmail.com
- 🔗 [Portfolio](https://elgendev.vercel.app) | [GitHub](https://github.com/Elgen69) | [LinkedIn](https://linkedin.com)

---

## 🎯 Roadmap

- [ ] v1.1: Add 50+ new intent samples
- [ ] v2.0: Multi-language support
- [ ] v2.0: Semantic similarity scoring
- [ ] v3.0: Webhook integration for auto-updates
- [ ] v3.0: Admin dashboard for live edits

---

**Last Updated**: May 21, 2026  
**Status**: Production Ready
