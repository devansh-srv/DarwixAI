# **The Empathetic Code Reviewer**  
**Darwix AI Hackathon – Mission 1**  
Transforming raw, critical code review comments into **empathetic**, **constructive**, and **educational** feedback using OSS LLMs.

---

## **📜 Project Description**  
This project solves the **Mission 1** challenge of the Darwix AI Hackathon:  
> Build an AI that rewrites blunt, technical code review comments into empathetic, constructive guidance, helping developers improve without feeling discouraged.

The solution uses **two large language models**:  
1. **Technical Critique** → Detects code issues and gives precise, improvement-focused feedback.  
2. **Empathy Rewrite** → Transforms that critique into supportive, mentor-like language with the “why” and helpful resource links.  

---

## **🚀 Approach**
### **Pipeline Overview**
1. **Input**: JSON containing:
   ```json
   {
     "code_snippet": "...",
     "review_comments": ["comment 1", "comment 2"]
   }
   ```
2. **Step 1 – Technical Critique**  
   - Model: `openai/gpt-oss-120b:groq`  
   - Produces structured, issue-focused critique without tone adjustments.  

3. **Step 2 – Empathy Rewrite**  
   - Model: `meta-llama/Meta-Llama-3-8B-Instruct:groq`  
   - Preserves all technical details while softening tone, adding explanations, and linking resources.  

4. **Output**: A Markdown-formatted review with:
   - **Positive Rephrasing**
   - **The Why**
   - **Suggested Improvement (Code Example)**
   - **Relevant Resource Links**
   - **Holistic Summary**

---

## **🛠️ Tech Stack**
- **Google Colab** for development & execution.
- **HuggingFace Inference API** with **Groq** provider for ultra-fast inference.
- **Python** with:
  - `huggingface_hub`
  - `openai` (OpenAI-compatible API calls)
  - `pydantic` (data validation)
  - `black` (optional formatting)

---

## **🔑 API Keys**
- **HF_TOKEN** → HuggingFace API token (required).  
  - Set it in Colab:
    ```python
    %env HF_TOKEN=your-huggingface-token
    ```
- Groq is accessed automatically via HuggingFace Router for the models used.

---

## **📦 Installation & Setup**
### **Run in Google Colab**
1. Open the provided `.ipynb` notebook in Colab.
2. Install dependencies:
   ```python
   !pip -q install huggingface_hub openai pydantic black==24.4.2
   ```
3. Set HuggingFace token:
   ```python
   %env HF_TOKEN=your-huggingface-token
   ```
4. Run all cells.

---

## **▶️ Usage**
### **Example Input**
```python
example = {
    "code_snippet": "def add(a,b):\n    return a-b",
    "review_comments": [
        "Function name suggests addition but subtracts instead.",
        "Consider adding type hints."
    ]
}
output = review_code(example)
from IPython.display import Markdown
Markdown(to_markdown_block(output.model_dump()))
```

### **Example Output (Markdown)**
```
### Analysis of Comment: "Function name suggests addition but subtracts instead."
* **Positive Rephrasing:** Great start! Let's ensure the function's behavior matches its name.
* **The 'Why':** Mismatched function behavior can cause logical errors in usage.
* **Suggested Improvement:**
```python
def add(a: int, b: int) -> int:
    return a + b
```
* **Resource:** [PEP 8 – Naming Conventions](https://peps.python.org/pep-0008/#naming-conventions)
---
**Holistic Summary:** Overall, your function is concise and clean. By correcting the operation and adding type hints, you'll improve clarity and maintainability.
```

## 🔐 Getting and Setting Your HuggingFace Token (`HF_TOKEN`)

This project requires a **HuggingFace API token** to access the models.  
Follow these steps to obtain and configure it:

### 1️⃣ Create / Log in to Your HuggingFace Account
- Go to [https://huggingface.co/join](https://huggingface.co/join) and create a free account or log in.

### 2️⃣ Generate a New Access Token
- Navigate to [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
- Click **New token**, give it a name (e.g., `darwix-hackathon`), and choose **Read** access.
- Copy the generated token.

### 3️⃣ Set the Token in Google Colab
Run this in a cell **before using the models**:
```python
%env HF_TOKEN=your-huggingface-token

---

## **📋 Final Submission Checklist**
- [x] **Public GitHub Repo** with notebook and README  
- [x] **README.md** includes:
  - Setup instructions
  - Problem approach
  - API key details  
- [x] **ZIP** of repo for submission  
- [x] **Files named and organized**  
- [x] **Submitted via Google Form**

---

## **📄 License**
MIT License – feel free to use and adapt.
