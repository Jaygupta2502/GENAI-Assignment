# 💊 MediInfo AI – Medicine Information Lookup

### AI-Powered Medicine Information & Patient-Friendly Clinical Explanations

**Academic Mini-Project | Problem Statement 58 | Generative AI**

MediInfo AI is an intelligent, user-friendly medicine information lookup application developed using **Python, Streamlit, Pandas, and Google Gemini API**.

The application allows users to search for medicines, retrieve structured information from a curated pharmaceutical dataset, and understand complex medical terminology through simple, AI-generated explanations.

Unlike conventional AI chatbots, MediInfo AI follows a **retrieval-grounded approach**, where Gemini is instructed to explain only the information available in the retrieved medicine record, reducing the risk of fabricated medical information.

---

## 📌 Problem Statement

Pharmaceutical leaflets and clinical databases often contain complex medical terminology that can be difficult for patients to understand.

Patients may rely on unverified websites or general-purpose AI chatbots, potentially encountering inaccurate medicine information, unsafe dosage suggestions, or misleading medical advice.

**MediInfo AI addresses this problem by providing:**

- Structured medicine information from a curated dataset.
- Simple explanations of complex pharmaceutical terminology.
- AI-assisted descriptions grounded in retrieved records.
- Safety restrictions against dosage recommendations and medical diagnosis.
- A clean, accessible healthcare dashboard.

## 🎯 Project Objectives

1. Develop a beginner-friendly medicine information lookup application.
2. Implement accurate medicine searching using Pandas.
3. Support both brand-name and generic-name searches.
4. Integrate Google Gemini for plain-English explanations.
5. Prevent unsupported medical claims through prompt engineering.
6. Handle missing information and API failures gracefully.
7. Design a professional and responsive Streamlit dashboard.

## ✨ Key Features

### 🔎 Intelligent Medicine Search
- Search medicines using brand names or generic names.
- Case-insensitive and whitespace-normalized queries.
- Exact-match prioritization over partial matches.
- Multiple matching results for ambiguous queries.
- Helpful suggestions when a medicine is not found.

### 📋 Structured Medicine Information
Displays six essential medicine attributes:

| Attribute | Description |
|---|---|
| Medicine Name | Common or brand name |
| Generic Name | Active pharmaceutical ingredient |
| Description | General medicine information |
| Uses | Common therapeutic applications |
| Side Effects | Documented potential adverse effects |
| Precautions | Important safety considerations |

### 🤖 Gemini-Powered Explanations

Google Gemini transforms technical medicine descriptions into simple, patient-friendly English.

Explanations are organized into five sections:

1. Purpose & What It Does
2. Why It Is Prescribed
3. Side Effects to Know
4. Safety Precautions
5. Medical Terms Simplified

### 🛡️ Medical Safety Guardrails
- No dosage recommendations.
- No medical diagnosis.
- No instructions to start, stop, or modify treatment.
- No intentional fabrication of unlisted medical facts.
- Missing information is clearly identified.
- AI explanations are grounded in the selected dataset record.

**Note:** Prompt-based guardrails reduce risk but cannot guarantee medical accuracy or completely eliminate hallucinations.

### 🎨 Professional Healthcare Dashboard
- White and light-blue healthcare theme.
- Responsive Streamlit interface.
- Quick-search medicine shortcuts.
- Structured medicine information cards.
- Dedicated AI explanation panel.
- Medicine statistics and information counters.
- Clear medical disclaimers.

### ⚡ Error Handling
- Invalid and empty search handling.
- Missing dataset field detection.
- Graceful API error messages.
- Gemini model fallback mechanism.
- Secure environment-variable configuration.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python 3.12 | Core application development |
| Streamlit | Interactive web interface |
| Pandas | CSV processing and medicine lookup |
| Google Gemini API | AI-generated medicine explanations |
| Google GenAI SDK | Official Gemini API integration |
| python-dotenv | Environment-variable management |
| CSV | Structured pharmaceutical dataset |
| Pytest | Automated application testing |
| HTML & CSS | Dashboard styling |

## 🏗️ System Architecture

```text
                 USER
                   |
                   v
       Streamlit Web Dashboard
                app.py
                   |
                   v
       Input Sanitization
            data_handler.py
                   |
                   v
       Pandas Medicine Lookup
                   |
                   v
          medicine_data.csv
                   |
                   v
       Retrieve Medicine Record
                   |
          +--------+--------+
          |                 |
          v                 v
   Structured Facts    Grounding Prompt
          |                 |
          |                 v
          |            Gemini API
          |               llm.py
          |                 |
          |                 v
          |          AI Explanation
          |                 |
          +--------+--------+
                   |
                   v
       Streamlit Results Dashboard
```

### Application Workflow

**Step 1 – Medicine Search**

The user enters a medicine name or selects a quick-search option.

**Step 2 – Input Normalization**

The application removes unnecessary spaces and normalizes character casing.

**Step 3 – Dataset Lookup**

Pandas searches both `medicine_name` and `generic_name`, prioritizing exact matches.

**Step 4 – Fact Retrieval**

The matching medicine record is extracted from the CSV dataset.

**Step 5 – AI Explanation**

The retrieved information is passed to Gemini with strict grounding and medical safety instructions.

**Step 6 – Results Display**

The application displays the original dataset facts alongside the AI-generated explanation.

---

## 📁 Project Structure

```text
MediInfo-AI/
│
├── app.py
│   └── Streamlit dashboard and UI
│
├── data_handler.py
│   └── CSV loading and search logic
│
├── llm.py
│   └── Gemini API integration
│
├── medicine_data.csv
│   └── Curated medicine dataset
│
├── test_mediinfo.py
│   └── Automated test cases
│
├── requirements.txt
│   └── Python dependencies
│
├── .env
│   └── Local Gemini API key (not committed)
│
├── .gitignore
│   └── Excluded files and secrets
│
└── README.md
    └── Project documentation
```

## 🚀 Installation & Setup

### Prerequisites

Ensure the following are installed:

- Python 3.12 or compatible version
- pip package manager
- Git
- Google Gemini API key
- Internet connection for AI explanations

### Step 1: Clone the Repository

```bash
git clone https://github.com/Jaygupta2502/GENAI-Assignment.git
cd GENAI-Assignment
```

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment.

**Windows PowerShell:**

```powershell
.\venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
python -m pip install -r requirements.txt
```

The application requires the following core packages:

```text
streamlit
pandas
google-genai
python-dotenv
pytest
```

### Step 4: Configure Gemini API Key

Obtain a Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey).

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

**Security:** Never upload `.env` or actual API credentials to GitHub.

Add the following entries to `.gitignore`:

```gitignore
.env
venv/
.venv/
__pycache__/
.pytest_cache/
*.pyc
```

### Step 5: Run the Application

```bash
python -m streamlit run app.py
```

Open the local address displayed in your terminal, typically:

```text
http://localhost:8501
```

---

## 🧠 Gemini API Integration

MediInfo AI uses the official Google GenAI Python SDK.

```python
from google import genai
```

The application uses a configurable model fallback strategy to improve resilience when a selected Gemini model is unavailable or experiencing high demand.

### Grounded Prompt Engineering

The Gemini model receives the selected medicine's dataset record, including:

- Medicine name
- Generic name
- Description
- Uses
- Side effects
- Precautions

The model is instructed to translate these facts into accessible language without introducing unsupported medical information.

### Prompt Safety Constraints

```text
You are MediInfo AI, a patient-friendly
medicine education assistant.

STRICT RULES:

1. Use only the supplied medicine information.
2. Do not invent medical facts.
3. Never recommend medication dosages.
4. Never provide medical diagnoses.
5. Never recommend treatment alterations.
6. Explain medical terminology simply.
7. Clearly identify unavailable information.
8. Present the response in five sections.
```

This approach combines **deterministic data retrieval with generative AI explanations**.

---

## 📊 Medicine Dataset

The application uses a curated CSV dataset containing **24 essential medicines** across common pharmaceutical categories.

Categories include:

- Analgesics and antipyretics
- Antibiotics
- Antidiabetic medicines
- Antihistamines
- Statins
- Proton pump inhibitors
- Bronchodilators

### CSV Schema

```csv
medicine_name,generic_name,uses,description,side_effects,precautions
```

The dataset follows RFC 4180-compatible CSV formatting to handle commas within medical descriptions correctly.

Missing or empty fields are explicitly displayed as:

```text
Information not available in dataset
```

The application does not generate replacement facts for missing dataset values.

---

## 🧪 Testing & Validation

The project report documents **16 automated Pytest cases**, covering seven primary evaluation scenarios, with additional API and security checks.

| Test Scenario | Expected Result |
|---|---|
| Valid medicine search | Correct medicine retrieved |
| Case-insensitive search | Same results regardless of case |
| Whitespace handling | Extra spaces removed |
| Unknown medicine | Graceful error and suggestions |
| Empty search | Appropriate input message |
| Missing dataset fields | Explicit unavailable-information label |
| Multiple matches | User can select the correct medicine |
| API errors | Fallback or graceful failure |
| API key handling | Secrets remain outside client-facing output |

### Run Automated Tests

```bash
python -m pytest test_mediinfo.py -v
```

According to the project verification report, all 16 automated tests passed.

---

## ⚙️ Technical Challenges & Solutions

### 1. Gemini Model Availability

**Challenge:** Certain Gemini models returned 404 errors or temporary 503 service-unavailable responses.

**Solution:** Implemented model fallback handling and request timeouts to reduce disruption.

### 2. CSV Parsing Errors

**Challenge:** Commas within medicine descriptions caused inconsistent field parsing.

**Solution:** Standardized CSV generation using `csv.DictWriter` and `csv.QUOTE_ALL`.

### 3. Streamlit HTML Rendering

**Challenge:** Indented multiline HTML was occasionally displayed as raw code blocks.

**Solution:** Refactored HTML templates to avoid unintended Markdown code formatting.

### 4. Windows PATH Configuration

**Challenge:** The `streamlit` command was not recognized in some PowerShell environments.

**Solution:** Used direct Python module execution:

```bash
python -m streamlit run app.py
```

---

## 🔒 Privacy, Security & Medical Ethics

MediInfo AI is designed for educational medicine information lookup, not clinical decision-making.

Security measures include environment-based API key storage, input normalization, restricted AI instructions, and controlled dataset retrieval.

The system does not require users to provide personal medical records for a standard medicine lookup.

### Medical Disclaimer

**MediInfo AI is an educational application and is not a substitute for professional medical advice, diagnosis, or treatment.**

Medicine information should be verified against authoritative clinical references and reviewed by qualified healthcare professionals before real-world use.

Users should consult a licensed doctor or pharmacist for questions regarding dosage, interactions, contraindications, or treatment decisions.

---

## ⚠️ Current Limitations

1. The medicine catalog is limited to 24 locally stored records.
2. AI explanations require an active internet connection.
3. The application does not provide personalized medical advice.
4. The system does not support clinical diagnosis or prescription generation.
5. Dataset updates require maintenance and verification.
6. LLM output may still contain inaccuracies despite grounding instructions.

## 🔮 Future Enhancements

### Real-Time Pharmaceutical APIs
Integrate authoritative sources such as OpenFDA and RxNorm for broader medicine coverage and standardized drug terminology.

### Multilingual Support
Provide medicine explanations in Hindi, Marathi, Tamil, and other regional Indian languages.

### Offline AI Assistance
Explore lightweight Small Language Models for environments with limited internet connectivity.

### Enhanced Search
Introduce spelling correction, autocomplete, and improved medicine-name matching.

### Source Transparency
Display reference sources, verification dates, and provenance for individual medicine records.

---

## 🎓 Academic Project Details

| Field | Details |
|---|---|
| Project Title | MediInfo AI – Medicine Information Lookup |
| Problem Statement | PS 58 |
| Student Name | Jay Gupta |
| Roll Number | 58 |
| Student ID | ADT23SOCB0474 |
| Class / Division | LY CORE 04 |
| Project Type | Academic Mini-Project |
| Domain | Generative AI / Healthcare Informatics |
| Primary Language | Python |
| Framework | Streamlit |
| AI Integration | Google Gemini API |

## 👨‍💻 Developer

**Jay Gupta**

B.Tech – Computer Science and Engineering  
MIT Art, Design and Technology University, Pune

**GitHub Repository:**  
https://github.com/Jaygupta2502/GENAI-Assignment

---

## 📄 Conclusion

MediInfo AI demonstrates how **structured pharmaceutical data, deterministic search, prompt engineering, and generative AI** can be combined to improve the accessibility of medicine information.

By separating factual data retrieval from AI-generated explanations, the application provides a practical example of retrieval-grounded generation, responsible AI design, and modular Python application development.

The project also demonstrates important software engineering practices, including secure API integration, automated testing, exception handling, and responsive web interface development.

---

**Developed as an academic Generative AI mini-project | PS 58**

*Making medicine information simpler, clearer, and more accessible.*
