# 📖 USAGE Guide: SENTRY-NLP Intents

How to integrate and use the SENTRY-NLP intent dataset in your projects.

---

## 🐍 Python Integration

### Method 1: Fetch from GitHub (Recommended)

```python
import requests
import json

# Fetch the latest intents from GitHub
INTENTS_URL = "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json"
RESPONSES_URL = "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/responses.json"

try:
    intents = requests.get(INTENTS_URL).json()
    responses = requests.get(RESPONSES_URL).json()
    print("✅ Successfully loaded intents from GitHub")
except Exception as e:
    print(f"⚠️ Failed to fetch from GitHub: {e}")
    # Fallback to local files
    with open("intents.json", "r") as f:
        intents = json.load(f)
```

### Method 2: Load from Local File

```python
import json

# Load from local file
with open("data/intents.json", "r") as f:
    intents = json.load(f)

with open("data/responses.json", "r") as f:
    responses = json.load(f)

print(f"Loaded {len(intents['intents'])} intent categories")
```

---

## 🧠 Using with spaCy (NLP Class Example)

```python
import spacy
import json

# Load spaCy model
nlp = spacy.load("en_core_web_md")

# Load intents
with open("intents.json", "r") as f:
    intents = json.load(f)

def resolve_intent(user_text):
    """Resolve intent using spaCy similarity matching"""
    doc = nlp(user_text.lower())
    best_score = 0
    best_intent = "unknown"
    
    for intent_name, intent_data in intents["intents"].items():
        for sample in intent_data["samples"]:
            score = doc.similarity(nlp(sample))
            if score > best_score:
                best_score = score
                best_intent = intent_name
    
    return best_intent, best_score

# Test
query = "Show me your projects"
intent, confidence = resolve_intent(query)
print(f"Query: {query}")
print(f"Intent: {intent} (confidence: {confidence:.4f})")
```

---

## 🔄 Using with Pandas (Data Analysis)

```python
import pandas as pd
import json

# Load intents
with open("intents.json", "r") as f:
    intents = json.load(f)

# Create a DataFrame for analysis
intent_list = []
for intent_name, intent_data in intents["intents"].items():
    for sample in intent_data["samples"]:
        intent_list.append({
            "intent": intent_name,
            "sample": sample,
            "description": intent_data["description"]
        })

df = pd.DataFrame(intent_list)

# Analysis
print(f"Total samples: {len(df)}")
print(f"\nSamples per intent:")
print(df["intent"].value_counts())
```

---

## 🌐 TypeScript/JavaScript Integration (Portfolio)

### React Component Example

```typescript
// AskElgen.tsx integration
import { useEffect, useState } from 'react';

interface Intent {
  samples: string[];
  description: string;
}

interface IntentsData {
  metadata: Record<string, unknown>;
  intents: Record<string, Intent>;
}

export function AskElgen() {
  const [intents, setIntents] = useState<IntentsData | null>(null);

  useEffect(() => {
    // Fetch intents from GitHub
    const INTENTS_URL = "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json";
    
    fetch(INTENTS_URL)
      .then(res => res.json())
      .then(data => setIntents(data))
      .catch(err => {
        console.error("Failed to fetch intents:", err);
        // Fallback to hardcoded intents
      });
  }, []);

  // Use intents for chatbot logic...
  if (!intents) return <div>Loading...</div>;

  return (
    <div>
      <p>Loaded {Object.keys(intents.intents).length} intents</p>
      {/* Chatbot UI */}
    </div>
  );
}
```

---

## 📊 Jupyter Notebook Example

```python
# In Chatbot_Individual_Project.ipynb

import json
import requests

# Option 1: Fetch from GitHub
try:
    response = requests.get("https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json")
    INTENT_DATA = response.json()["intents"]
except:
    # Fallback: Load from local
    with open("data/intents.json") as f:
        INTENT_DATA = json.load(f)["intents"]

# Convert to the format your notebook expects
intents_dict = {
    name: data["samples"]
    for name, data in INTENT_DATA.items()
}

print(f"✅ Loaded {len(intents_dict)} intent categories")
```

---

## 🔐 Environment Variables (Optional)

For production security, store the GitHub URL in an environment variable:

```python
import os

INTENTS_URL = os.getenv(
    "SENTRY_INTENTS_URL",
    "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json"
)

intents = requests.get(INTENTS_URL).json()
```

---

## 🚨 Error Handling

```python
import json
import requests

def load_intents(github_url, fallback_path):
    """Load intents with fallback mechanism"""
    try:
        # Try GitHub first
        response = requests.get(github_url, timeout=5)
        response.raise_for_status()
        return response.json()
    except Exception as e:
        print(f"⚠️ GitHub fetch failed: {e}")
        print("📂 Falling back to local file...")
        
        try:
            with open(fallback_path, "r") as f:
                return json.load(f)
        except Exception as local_err:
            print(f"❌ Failed to load local file: {local_err}")
            return None

intents = load_intents(
    "https://raw.githubusercontent.com/Elgen69/sentry-nlp-intents/main/intents.json",
    "data/intents.json"
)
```

---

## 📈 Data Validation

```python
import json

def validate_intents(intents_data):
    """Validate intents JSON structure"""
    required_keys = {"metadata", "intents"}
    
    if not isinstance(intents_data, dict):
        raise ValueError("Root must be a dictionary")
    
    if not required_keys.issubset(intents_data.keys()):
        raise ValueError(f"Missing keys: {required_keys - intents_data.keys()}")
    
    for intent_name, intent_data in intents_data["intents"].items():
        if "samples" not in intent_data or "description" not in intent_data:
            raise ValueError(f"Intent '{intent_name}' missing required fields")
        
        if not isinstance(intent_data["samples"], list):
            raise ValueError(f"Intent '{intent_name}' samples must be a list")
    
    print("✅ Intents validation passed")

# Test
with open("intents.json") as f:
    intents = json.load(f)
    validate_intents(intents)
```

---

## 🔄 Versioning & Updates

When updating intents:

1. **Modify** `intents.json` or `responses.json`
2. **Update** the `version` field in metadata
3. **Commit** with a meaningful message: `git commit -m "Add fitness intent samples"`
4. **Push** to main: `git push origin main`
5. **Verify** by fetching: `requests.get(INTENTS_URL).json()`

---

## 📞 Support

For issues or questions:
- Create an issue on [GitHub](https://github.com/Elgen69/sentry-nlp-intents/issues)
- Email: elgen.arinasa.business@gmail.com

---

**Last Updated**: May 21, 2026
