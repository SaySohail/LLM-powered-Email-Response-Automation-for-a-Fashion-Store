
# 📬 LLM-powered Email Response Automation for a Fashion Store

## 📌 Project Overview

This project automates the classification and handling of customer emails in a fashion retail setting using Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG). It intelligently distinguishes between *product inquiries* and *order requests*, responds professionally, checks stock availability, and provides recommendations using semantic search over a product catalog.

---

## 🧠 Description

The goal is to build a production-grade system that processes customer emails at scale:

- **Classifies emails** as "order request" or "product inquiry" using LLM-based zero-shot classification.
- **Handles order requests** by extracting products and quantities using LLM, checking availability, updating stock, and sending professional confirmation or fallback emails.
- **Responds to product inquiries** using semantic RAG search across a vectorized catalog of 100k+ products.
- **Extracts customer names** from email bodies using LLM, personalizing responses.
- **Generates response emails** using LLMs with consistent, standardized templates.

---

## 🏗️ Architecture

```mermaid
graph TD;
    A[📧 Incoming Email] --> B[🤖 LLM Classification];
    B -->|Order Request| C[🛍️ Order Extraction (LLM)];
    B -->|Product Inquiry| F[RAG Search + Inquiry Response];
    C --> D[📦 Stock Check];
    D --> E[✅ Generate Response or ❌ Recommend];
    F --> G[✉️ Inquiry Response Generation];
    E --> H[📝 Save to Excel];
    G --> H
```

---

## ✨ Improvements Made

- Replaced regex with LLM-based structured extraction for robust product and name parsing.
- Implemented RAG (FAISS + OpenAI Embeddings) for scalable inquiry handling without token overload.
- Added fallback recommendations for vague requests.
- Personalizes emails using extracted customer names.
- Modular and production-ready response templates.
- Stock management integrated with product lookup.

---

## 🤖 LLM and RAG Usage

- **LLM**: Used via LangChain for classification, extraction, and response generation.
- **RAG**: FAISS vector store + OpenAI embeddings for semantic search on product descriptions and metadata.
- Prompts are template-driven to ensure consistency, clarity, and control.

---

## 🚀 Getting Started

### 📦 Dependencies

```bash
pip install langchain openai pandas faiss-cpu ipython openpyxl
```

---

### 🔽 Data

- Product and Email data are fetched from **Google Sheets** using public CSV export.
- Customize the document ID in `read_data_frame(document_id, sheet_name)`.

---

### 🏃 Executing the Program

```bash
# 1. Ensure API keys are set for OpenAI
export OPENAI_API_KEY=your_key_here

# 2. Clone the repo or open in Colab
# 3. Run the notebook cells sequentially
```

---

## 📂 Output

The results are saved to `output.xlsx` with the following sheets:

- `email-classification`
- `order-status`
- `order-response`
- `inquiry-response`

---

## 📌 Example Email

```text
Subject: I'd like to place an order

Body: Hey, can I buy 2 of the Infinity Scarves and 1 Leather Wallet? Thanks, Sarah.
```

Will result in:

✅ Email classified as "order request"  
✅ Extracted customer name: Sarah  
✅ Stock checked & order confirmed  
✅ Personalized response email generated  
✅ Result saved to spreadsheet

