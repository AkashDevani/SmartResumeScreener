# AI Resume & JD Analyzer

Version: 1.0
Author: Your Name
Date: 2025-10-15

---

## 1. Project Overview

The AI Resume & JD Analyzer is a web application that compares a candidate’s Resume against a Job Description (JD) using Google Gemini API.

Key Features:

* Upload Resume (PDF) and JD (PDF)
* Extract JD requirements: skills, experience, education
* Generate a match score (1–10)
* Provide a detailed justification for the match
* Responsive UI built with Tailwind CSS
* Handles API errors and rate limits

---

## 2. Architecture

```
 +------------------+        +--------------------+        +---------------------+
 |  User Interface  |        |  JavaScript Logic  |        |   Google Gemini     |
 |  (index.html)    |        |  (analyze.js)      |        |   LLM API           |
 |                  |        |                    |        |                     |
 |  - File Upload   | -----> | - Read PDFs        | -----> | - Process Resume    |
 |  - Display UI    |        | - Convert to Base64|        |   and JD            |
 |  - Results Panel |        | - Construct Prompt |        | - Extract JD        |
 |                  |        | - Call API         | <----> |   Requirements      |
 |                  |        | - Parse JSON       |        | - Compute Match     |
 |                  |        | - Render Results   |        | - Generate Justif.  |
 +------------------+        +--------------------+        +---------------------+
```

Flow Description:

1. User uploads Resume and JD PDFs.
2. JS reads files and converts them to Base64.
3. JS constructs LLM prompt and sends it to Gemini API.
4. Gemini returns JSON containing:

   * `jdRequirements` (skills, experience, education)
   * `matchScore` (1–10)
   * `justification` (text)
5. JS parses JSON and updates the UI dynamically.

---

## 3. LLM Prompts

### System Instruction

```
You are a world-class HR Analyst. 
Analyze a candidate's Resume against a Job Description (JD). 
1. Extract key JD requirements (skills, experience, education). 
2. Compare Resume content to JD. 
3. Generate a match score from 1 (poor) to 10 (perfect). 
Output MUST strictly follow the JSON schema provided.
```

### User Query

```
Analyze the provided Resume (first PDF) against the Job Description (second PDF).
1. Extract the required skills, experience, and education from the JD.
2. Score the Resume's match against the JD requirements (1-10).
3. Provide a detailed justification for the score.
```

### Expected JSON Schema

```
{
  "jdRequirements": {
    "skills": ["Skill1", "Skill2"],
    "experience": "Required experience summary",
    "education": "Required education summary"
  },
  "matchScore": 1-10,
  "justification": "Explanation for the match score"
}
```

---

## 4. Setup Instructions

1. Clone the repo:

```
git clone https://github.com/yourusername/ai-resume-jd-analyzer.git
cd ai-resume-jd-analyzer
```

2. Get your Google Gemini API Key from [Google AI Studio](https://makersuite.google.com/app/apikey).

3. Open `index.html` and set the API key:

```javascript
const apiKey = "YOUR_GEMINI_API_KEY";
```

4. Open `index.html` in a browser.

---

## 5. File Structure

```
ai-resume-jd-analyzer/
│
├─ index.html          # Main frontend UI
├─ README.txt          # This file
├─ style.css           # Optional custom CSS
└─ assets/             # Icons or images
```

---

## 6. Notes & Limitations

* Only PDF files are supported.
* API Key is exposed on the client; consider backend proxy for production.
* Large PDFs may exceed model input size.
* UI is fully client-side and mobile-responsive.

---

## 7. License

MIT License — free for personal and commercial use.
